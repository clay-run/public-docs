---
title: Google Sheets integration
description: Cloud-based spreadsheet for real-time collaboration. Covers using
  Google Sheets as a Clay table source (including dedup fields and import
  history) as well as enrichment actions.
last_synced: 2026-04-26T01:40:04.431Z
---

# Google Sheets integration

Cloud-based spreadsheet for real-time collaboration.

Google Sheets in Clay enables seamless integration between your Clay tables and Google Sheets, allowing you to easily sync and manage data across both platforms.

## Using Google Sheets as a source

You can pull rows from a Google Sheet directly into a Clay table as a source. Each time the source runs, Clay reads rows from the spreadsheet and adds or updates rows in your table.

### Setting up a Google Sheets source

1.  In a Clay table, click `Tools` → `Import` (or `Actions` → `Import`, depending on your account).
2.  Search for `Google Sheets` and select the source option.
3.  Connect your Google account and select your spreadsheet.
4.  Choose the **Sheet ID** (tab) to import from.
5.  Select **Fields to deduplicate by** — one or more columns that together uniquely identify each row (see below).
6.  Optionally, set a **Lookup column** and **Lookup value** to filter which rows are imported (only rows where that column matches the lookup value will be included).

### Fields to deduplicate by

**Fields to deduplicate by** is a required setting. Clay uses the values of these column(s) to compute a unique ID for each row. This ID is what Clay uses to track which rows have already been imported and to match incoming rows against existing ones on re-runs.

**Choosing the right dedup fields is critical for predictable imports:**

-   **Use a single, truly unique field** — such as an email address, LinkedIn URL, or a custom record ID. This ensures every row gets a distinct ID, so Clay can accurately track and update individual records.
-   **Avoid using non-unique fields** — such as Company Name. If multiple rows in your sheet share the same value for the dedup field (for example, five contacts all at the same company), Clay assigns those rows the same unique ID and treats them as the same record. All five rows will collapse into a single row in the table.
-   **Avoid selecting many fields at once** — deduplicating across a large number of fields means a row is only recognized as "already imported" when *all* of those field values match exactly. Minor differences in any one field create a new unique ID, which can cause unexpected duplicate rows on re-runs.

### Why the source says "X rows found" but fewer rows appear in the table

If your source reports finding more rows than actually appear in your table, the cause is almost always the **Fields to deduplicate by** configuration:

-   Rows that share the same values for the dedup fields get the same unique ID. Clay collapses them into a single record — even if other columns differ.
-   Rows whose unique ID matches a row already in the table are updated in place rather than creating new rows.

**Example:** If **Company** is your only dedup field and five rows all list `AltiSales` as the company, Clay assigns the same unique ID to all five. The source finds all five rows in the sheet, but only one record is created in your Clay table.

### Why rows I deleted don't reappear when I re-run the source

Clay's Google Sheets source tracks every record it has imported by storing its unique ID (derived from **Fields to deduplicate by**). This import history persists even after you delete rows from the table. When you re-run the source against the same sheet data, Clay recognizes those records as already-seen and skips them — which is why deleted rows don't reappear even though the source "finds" them.

**To re-import previously deleted rows or start fresh:**

-   **Delete and re-add the source:** Click the source column title → `Sources` → the source name → `Delete source`. Then add a new Google Sheets source pointing to the same spreadsheet. A fresh source has no import history, so it will pull all rows in.
-   **Duplicate the table:** Creates a new table with a fresh source definition that has no prior import history.

**Note:** If you want to refresh data in existing rows, enable **Update existing rows** in the source's Run settings (under the source column → `Edit source` → `Run settings`). When enabled, re-running the source will update matching rows with the latest values from the sheet.

## Enriching data with Google Sheets

1.  While in a Clay table, click `Tools` and search for `Google Sheets`.
2.  Under `Enrichments`, select one of the Google Sheets options.
3.  In the modal, you will be asked to `Select Google Sheets account`.
    -   If you haven't already connected your Google Sheets, click `+ Add account` and go through authentication.

### `Action` Add row

Add a row to a Google Sheet via its URL.

**Inputs**

-   **Google Spreadsheet URL**

### `Action` Lookup row

Lookup a row in a Google Sheet using a column and a value.

**Inputs**

-   **Google Spreadsheet URL**

### `Action` Lookup, add, or update row

Lookup a row in a Google Sheet using a column and a value. Optionally, you can add a row if nothing is found, or update a row if something is found.

**Inputs**

-   **Google Spreadsheet URL**

### **Run settings**

-   **Auto-update**
-   **Only run if:** The enrichment will only run if conditions are met. ([Learn more about conditional formulas here!](https://www.clay.com/university/lesson/ai-formulas-conditional-runs-clay-101))
