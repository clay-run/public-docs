---
title: Sources
source_url: https://university.clay.com/docs/sources
description: Every Clay table begins with a source. Sources are the foundation
  of how data gets into your tables.
last_synced: 2026-04-26T01:40:43.486Z
---

# Sources

Every Clay table begins with a source. Sources are the foundation of how data gets into your tables.

Sources are the foundation of Clay and determine how data flows into your table—think of them as the roots of a tree feeding information into your database. Just like a tree needs strong roots to grow and thrive, every Clay table needs well-configured sources to function effectively.

Every Clay table starts with a source. You can import customer data from a CSV file, connect to your CRM system, or receive real-time updates through webhooks. Sources are your gateway to organizing and managing data in Clay.

## Types of sources

-   List builders ([Find Companies](https://www.clay.com/university/guide/find-companies), [Find People](https://www.clay.com/university/guide/find-people-overview))
-   CRM systems ([Hubspot](https://www.clay.com/university/guide/hubspot-integration-overview), [Salesforce](https://www.clay.com/university/guide/salesforce-integration-overview))
-   [Webhooks](https://www.clay.com/university/guide/webhook-integration-guide)
-   [CSV files](https://www.clay.com/university/guide/csv-import-overview)

## Adding sources to table

**Add to a new table:**

1.  Click `+ Add` at the bottom of a workbook to create a new table.
2.  Search for and select your desired data source (such as Salesforce or Find People).
3.  Configure the source settings.
4.  Review the preview and click `Import to new table`.

**Add to an existing table:**

1.  In a table, click `Tools` → `Import`.
2.  Search for and select your desired data source (such as Salesforce or Find People).
3.  Configure the source settings.
4.  Review the preview and click `Import`.

### Importing CSV

**To import a CSV file into a new table:**

1.  Click `+ Add` at the bottom of a workbook to create a new table.
2.  Click `Import from CSV` and select your file.
3.  Click `Complete import`.

**To import to an existing table:**

1.  In a table, click `Tools` → `Import`.
2.  Click `Import from CSV` and select your file.
3.  Select and map columns from your CSV to the Clay table.
4.  Click `Add to table`.

## Exporting table data

To download your table data as a CSV:

1.  **Uncheck all rows.** If any row checkboxes are selected, the toolbar switches to row-level bulk action mode — run, delete, debug — and table-level functions including Export are not shown. Uncheck all rows first.
2.  In the table toolbar, click `Tools` → `Export`.
3.  Click `Download CSV`. Clay processes the export in the background and the file downloads automatically.

**Why can't I see Export?** The most common cause is having one or more rows checked. The toolbar shows different options depending on row selection state: when no rows are selected, you see table-level functions such as Export and Import; when rows are selected, the same button shows bulk row operations instead. Uncheck all rows to restore access to Export.

**Long text or AI column data appears truncated in the export.** If a column stores enrichment or AI-generated output as nested structured data — such as the output of a Use AI, Claygent, or enrichment integration column — the CSV export may show only a short preview ending in "..." rather than the full text value.

To export the complete text, extract the specific field into a dedicated column first:

1.  In your table, click `+ Add column` and add a new column.
2.  Map it to the specific sub-field from the enrichment output (for example, the personalized message text from a Use AI column).
3.  Run the new column to populate it with the full text values.
4.  Export the table — the new column will contain the untruncated text in the CSV download.

## Importing accounts and contacts together

The recommended setup for working with both companies and people in Clay is two linked tables in the same workbook — one for accounts/companies and one for contacts/people.

### Step 1: Create your accounts table

1.  In a new workbook, click `+ Add` at the bottom to create your first table.
2.  Add your company/account data using one of these sources:
    -   **CSV:** Select `Import from CSV` and upload your accounts file.
    -   **Salesforce or HubSpot (live sync):** Search for `Salesforce` or `HubSpot`, select the accounts/companies object, and configure the connection.

### Step 2: Create your contacts table

Click `+ Add` again to add a second table for your contacts/people. The same source options apply:

-   **CSV:** Select `Import from CSV` and upload your contacts file.
-   **Salesforce or HubSpot:** Select the contacts/people object from your CRM.
-   **Find People:** Use the `Find People` source to search Clay's database for contacts matching your criteria.

### Step 3: Link contacts to their accounts

How the link is created depends on which source you used for contacts:

**If you used Find People at These Companies** (launched from your accounts table): A **Company Table Data** column is automatically added to the contacts table, linking each person back to their company row. No additional setup is required to establish this link. **Note:** Company Table Data retrieves basic column types only (text, number, formula, etc.) — enrichment columns are not included. To access company enrichment data in the contacts table, add a **Lookup single row in other table** column instead (see [Lookup Rows](lookup-rows.md)).

**If you imported contacts from CSV or CRM:** Add a **Lookup Rows** action on the contacts table to pull account-level data into each contact row:

1.  In your contacts table, click `+ Add column` and select `Lookup single row in other table`.
2.  Set `Table to search` to your accounts table.
3.  Set `Target column` to your match key in the accounts table (typically **company domain** or **Account ID**).
4.  Set `Row value` to the corresponding column in your contacts table.
5.  Run the lookup.

This gives you account-level attributes (company name, industry, revenue, etc.) directly on each contact row. For more details on configuring lookups, see [Lookup Rows](https://university.clay.com/docs/lookup-rows).

### Tips for CRM imports

-   **Scope your source before the first sync.** When connecting Salesforce or HubSpot, use a pre-filtered list view or segment (e.g., filtered by account stage, owner, or segment) as your source. This ensures you bring in only the records you plan to work with — not your entire CRM.
-   **Sources are additive.** Once records are imported, narrowing your source filter does not remove rows already in the table. See [Will rows already in my table be removed if they no longer match the source filter?](#will-rows-already-in-my-table-be-removed-if-they-no-longer-match-the-source-filter) below.

## Modifying sources

1.  In a table, click the source column title.
2.  Click `Sources` and the name of the source.
3.  Click `Edit source` and adjust the settings as needed.

## Deleting sources

1.  In a table, click the source column title.
2.  Click `Sources` and the name of the source.
3.  Click `Delete source`.

## Scheduled sources

Scheduling source runs is one of the most powerful features, as it keeps your information automatically up to date. To learn more, check out [scheduled sources](https://www.clay.com/university/guide/scheduled-sources).

## FAQs

### Why is the Submit button greyed out when configuring the "Find local businesses using Google Maps" source?

**The Submit button stays disabled until all required fields are filled in — including fields that appear dynamically after you make a selection.**

When you choose a **Search Type** (either **Business types** or **Free text**), a new required field appears directly below it. Because this field loads below the visible area of the dialog, it's easy to miss.

To fix this:

1.  After selecting a search type, **scroll down** inside the source configuration dialog.
2.  Fill in the required field that appeared:
    -   If you selected **Business types**: choose at least one business type from the dropdown.
    -   If you selected **Free text**: enter a search query (for example, "coffee shops" or "HVAC contractors").
3.  Once all required fields are filled, the Submit button will become clickable.

### Why doesn't my Clay table update when I change the source filters?

**Editing the source of a Clay table after it's been run won't retroactively update the results, because Clay doesn't reprocess previously generated data automatically.**

Even if the source preview shows the new filters, the table won't refresh until you explicitly re-run the source. Rows already in the table **stay** — they are not automatically removed if they no longer match the updated filters (for example, companies that were part of a HubSpot list but have since been excluded by a filter change).

To control which rows are in your table after updating source filters, you have two options:

-   **Remove specific rows manually:** Apply a table filter to isolate rows you no longer want, select them, and delete them. This preserves the rest of your table without re-running the source.
-   **Reset the table to match current filters:** Delete all existing rows and re-run the source (or duplicate the table with the updated source). This clears the table and re-imports only records that match the current source filters. **For CRM and database sources (Salesforce, HubSpot, Snowflake):** deleting rows and re-running the same source will not re-add the deleted records — the source permanently tracks every record it has already imported. Duplicate the table (or delete and re-add the source) to get a fresh import history. See [I deleted rows from my table and re-ran the source, but they didn't reappear](#i-deleted-rows-from-my-table-and-re-ran-the-source-but-they-didnt-reappear) for more.

### Will rows already in my table be removed if they no longer match the source filter?

**No. Clay sources are additive only — they add rows (and optionally update them), but they never automatically remove rows from your table.**

If you narrow a source filter — for example, by updating a HubSpot list or segment so that certain contacts or companies no longer qualify — the rows already in your Clay table will stay. They are not deleted automatically.

The **Update existing rows** toggle (available when re-running a source) controls whether Clay refreshes the data in existing rows on re-run. It does not remove rows that are no longer included in the source.

To remove rows that no longer match your filter, you have two options:

-   **Delete them manually** — select the rows in the table and delete them.
-   **Delete and re-run the source** — this re-imports records based on the current filter. You will need to clear any previously imported rows first if you want a clean slate. **For CRM and database sources (Salesforce, HubSpot, Snowflake):** the source tracks previously imported records and will not re-add deleted rows even after re-running. Duplicate the table (or delete and re-add the source) instead.

### I deleted rows from my table and re-ran the source, but they didn't reappear

**For Salesforce, HubSpot, Snowflake, and other CRM or database sources, re-running the same source after deleting rows will not restore those records.** Clay's import source tracks every record it has ever introduced to the table — including rows you've since deleted. When the source runs again, it recognizes and skips any record it has already seen, preventing both duplicate imports and unintentional revival of deleted rows.

When dedup blocks all records on a re-run, that run's **Rows Added** count in Source history shows **0** — not the number of records in your upstream source. The higher counts visible elsewhere in Source history are from earlier runs when those records were first imported. Your table can appear empty while Source history shows non-zero counts from past imports: the records were added in an earlier run and then deleted from the table, but the source still has them logged.

**To restore deleted records or get a fresh import:**

Duplicate the table (or delete and re-add the source). A new source definition starts with a clean record history, allowing the same records to be imported again. Before doing this, enable [auto-dedupe](table-management-settings.md) on a unique identifier column to avoid creating duplicates of rows still present in your table.

**Note:** This tracking behavior applies to CRM and database sources only (Salesforce, HubSpot, Snowflake, and similar). List builder sources such as Find People and Find Companies do not track records this way — deleting rows and re-running will re-import matching records, subject to your table's auto-dedupe settings.

### I am trying to add a source to an existing table, but I get an error

When adding a new source to an existing table, you must have the appropriate columns set up. For example, to add a `Find company` source, you need professional social URLs or Company Domains columns.

### I see "Limit of 20 sources for source field reached" when adding a source

**Each Clay table supports a maximum of 20 sources.** If you try to add a 21st source, Clay shows the error: *"Limit of 20 sources for source field reached. Please create another table to add more sources."*

This limit applies to all source types — CRM imports, Find People/Companies searches, CSV files, webhooks, and other tables feeding rows in via Send Table Data.

**To continue your workflow with a new source:**

1. **Save your current table as a template** to preserve its column structure and enrichment setup.
2. **Create a new table from the template.**
3. **Add your new source to the new table.**

Alternatively, if you no longer need one of the existing sources, you can delete it to free up a slot:

1. Click the source column title in the table.
2. Click **Sources** → the source name.
3. Click **Delete source.**

### **What are the row limits for Clay tables and sources?**

Clay tables have a **50,000-row limit** across all plans. This applies to all sources including CSV files, CRM systems, list builders, webhooks, and signals.

**Source-specific limits:**

-   **Salesforce Reports**: 2,000 records (API restriction) — to import more than 2,000 records, use the [Salesforce SOQL source](salesforce-soql.md) instead (supports up to 50,000 records)
-   **Salesforce List Views**: Up to 50,000 records for SOQL-compatible views; 2,000 records for views that are not SOQL-compatible — to import more than 2,000 records from a non-SOQL-compatible view, use the [Salesforce SOQL source](salesforce-soql.md) instead
-   **Find Companies and Find People sources**: subject to a per-source cumulative limit that varies by billing plan (for example, 100 records on free workspaces, 25,000 on Explorer-tier plans, 50,000 on Pro plans and above). Unlike other source types, these display an explicit error message when the limit is reached — see [Finding companies and people in Clay](finding-companies-and-people-in-clay.md) for the workaround.
-   **All other sources**: 50,000 records

**What happens when you hit the limit?**

For standard source imports (CSV, CRM, list builders), Clay stops importing silently when the limit is reached — no error is displayed. **Find Companies and Find People sources** are an exception: they surface an explicit error — "Your source has exceeded your plan's limit of [N], so future runs will not add new records" — rather than failing silently. For **send table data** actions targeting a full table, a `"Record limit reached"` message appears in the source table's action column.

**Solutions for large datasets:**

-   Split your data using filters or date ranges into multiple tables
-   Create a new import source — for Snowflake, CRM, and other database sources that have hit the limit, adding a new source definition starts at a fresh 0/50,000 record count (see [FAQ below](#my-scheduled-snowflake-or-crm-import-appears-to-have-stopped-importing-new-records))
-   Use [auto-delete](https://university.clay.com/docs/table-management-settings#auto-delete-passthrough-tables) (Enterprise plan) for unlimited rows with compatible source types (webhooks, send table data, signals)
-   Use [bulk enrichment](https://www.clay.com/university/guide/bulk-enrichment) (Enterprise plan) to process millions of records

### Does manually deleting rows free up space toward the 50,000-row limit?

**No.** Manually deleting rows removes them from the table view but does not decrement the underlying source record count. Tables and their data sources are separate entities — the source tracks its own total independently. This means a table can show far fewer than 50,000 visible rows while the source has already accumulated 50,000 records, causing a "Record limit reached" error even when the table appears mostly empty.

To free up source capacity, enable **auto-delete**. For compatible source types (webhooks, send table data, and signal sources), auto-delete removes rows from both the table and the source, keeping the source record count in check. See [auto-delete](auto-delete.md) for setup instructions and source compatibility details.

### My scheduled Snowflake or CRM import appears to have stopped importing new records

**If a scheduled Snowflake, HubSpot, Salesforce, or other database import is running on schedule but no new rows are appearing in your table, the most likely cause is that the import source has accumulated 50,000 records and is now silently discarding all incoming data.**

Clay's scheduled source runs continue to fire normally after the limit is reached — the schedule itself is not broken. But at the point of record insertion, Clay silently discards every incoming record without displaying an error or sending a notification. From the outside, it looks exactly as if the schedule has stopped running.

**Important:** This is the *source record count*, not the table's visible row count. The source tracks every record it has ever introduced to the table, including rows you have since deleted. A table can show far fewer than 50,000 visible rows while the source has already accumulated 50,000 records. Deleting rows from the table does not reset the source record count.

**Auto-delete does not help for these source types.** Auto-delete only resets the source record count for webhooks, send table data, and signal sources. For Snowflake query imports, HubSpot, Salesforce, and other CRM or database connections, auto-delete removes rows from the table view but the source record count keeps accumulating. See [auto-delete](auto-delete.md) for source compatibility details.

**To resolve this:**

1.  **Create a new import source.** Delete the old source definition and add a new one with the same query or connection settings. A new source starts at a fresh 0/50,000 record count. Before adding the new source, enable [auto-dedupe](table-management-settings.md) on a unique identifier column (such as email or company domain) — this automatically removes any duplicate rows if the new source re-imports records already present in your table.

2.  **Set a row count alert.** Use [table alerts](table-alerts.md) to get notified before the next source approaches the limit. The default threshold is 45,000 rows, giving you time to act before importing stops.

For large ongoing Snowflake imports that regularly approach or exceed 50,000 records, consider [Audiences](audiences.md) (currently in beta for Enterprise customers) instead of a standard table. Audiences scales to millions of records without per-source limits.
