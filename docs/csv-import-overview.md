---
title: How to import your CSV into Clay
source_url: https://university.clay.com/docs/csv-import-overview
description: Import your CSV into Clay.
last_synced: 2026-04-26T01:39:49.725Z
---

# How to import your CSV into Clay

Import your CSV into Clay.

Within Clay you can import CSV as a source to an existing or new table.

## Importing a CSV into Clay

1.  Open the source panel:
    -   **For a new table:** From your workspace home, click `+ Create new` and search for `CSV`.
    -   **For an existing table:** Open the table, click `Tools` (or `Actions`, depending on your account), and select `Import`.
2.  Upload your file by clicking `Browse Files` or dragging and dropping your CSV into the upload area.

    > **Note:** If your CSV has more rows than your plan allows in a single table, the upload dialog will either block the import with an error or show an **"Import First N Rows"** button that imports only up to your plan's limit. If you see fewer rows than expected after importing, you've likely hit your plan's row limit — upgrade your plan or contact Clay support to increase it.

3.  Select your destination:
    -   `Add to current table` — appends the CSV rows to your existing table.
    -   `Create new table` — creates a new table populated with your CSV data.
    -   `Replace current table` — overwrites the current table's rows with the CSV data.

    > **Note:** None of these options update existing rows. `Add to current table` always appends each CSV row as a new row — it does not match records by a column value or update rows that already exist in your table. If you need to add a column's values to rows that are already in Clay (for example, a "Keep/Remove" status matched on LinkedIn URL), see [Adding a new column to existing rows](#adding-a-new-column-to-existing-rows) below.

4.  Map your CSV columns to the correct Clay table fields.
5.  Choose how to handle the imported rows:
    -   `Save and run rows in this CSV` — imports the rows and immediately queues all enrichment columns to run on every imported row. If your table has enrichment columns configured (email finders, waterfalls, AI columns, etc.), they will all fire and consume credits.
    -   `Save and don't run` — imports the rows without triggering any enrichments for this batch. This is a one-time skip for the current import only — it does not change your table's [Auto-run](table-management-settings.md) setting.

    > **Tip:** If you're importing into a table that already has enrichment columns and you don't want them to run on the new rows, choose `Save and don't run`. If you want to prevent enrichments from automatically running on all future row additions as well, turn off **Auto-run** in your [table settings](table-management-settings.md) before importing.

## Next steps after importing

Once your data is in Clay, you can enrich rows to pull in additional information.

**If you imported a list of companies and want to find contacts and their email addresses:**

1.  In your table, click **Tools** (or **Actions**, depending on your account), switch to the **Sources** tab, and select **Find People at These Companies** to search for people at each company by job title, seniority, or other criteria. Each match is returned as a separate contact row.
2.  On the resulting contacts table, click **Add enrichment**, search for **Work Email**, and select the waterfall to find and validate a work email address for each contact.

Importing a company list does not automatically add contact rows or email addresses — you need to run these two steps explicitly. For full setup instructions, see [Finding companies and people in Clay](finding-companies-and-people-in-clay.md) and [Work Email waterfall](work-email-waterfall.md).

**If your CSV already has partial data and you want to verify or fill in only what's missing:**

When you import a CSV that already contains some fields — such as email addresses, LinkedIn URLs, or company names — you do not need to re-enrich everything from scratch. Use **run conditions** on each enrichment column to skip rows that already have data, so you only spend credits on rows that actually need it.

-   **To validate emails you already have:** Add a column → `Tool` → search for **Validate Email** → map the input to your existing email column. In **Run settings**, set the condition to `/Email is not empty` (replace `Email` with your actual column name). The tool runs only on rows that have an email; rows without one are skipped and no credits are consumed.

-   **To find emails only where they're missing:** Add a column → `Tool` → search for **Work Email Waterfall** → map the inputs (LinkedIn URL, first name, last name, company). In **Run settings**, set the condition to `/Email is empty`. The waterfall only runs on rows that don't yet have an email, leaving rows that already have one untouched.

-   **The same pattern applies to any field:** to enrich a column only where the current value is blank, set the run condition to `/ColumnName is empty`. Rows where the condition is not met show **"Run condition not met"** and consume no credits — even when you click **Run all rows**.

For a full reference on run condition syntax, see [Conditional runs](conditional-runs.md).

**If you want to add a new column's values to existing rows using a shared identifier:**

CSV import cannot update rows that already exist in Clay — there is no upsert mode. If you have a spreadsheet with new column values to bring into your existing Clay table (for example, a "Keep/Remove" status column matched on LinkedIn Profile URL), use this two-step approach instead:

1.  Import the enriched CSV as a **new** Clay table (choose `Create new table` at step 3 above).
2.  In your original table, click **Add enrichment** and search for **Lookup Single Row in Other Table**.
3.  Set the matching column (e.g., LinkedIn Profile URL) so Clay finds the right row in the new table.
4.  Map the column you want to populate (e.g., "Keep/Remove") as an output.

Each existing Clay row fetches the matching value from the new table without creating duplicates.
