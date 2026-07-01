---
title: Sources
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

**Note:** When importing a source into an existing table, Clay automatically runs enrichments on only the **first 10 imported rows**. The remaining rows are added to the table but do not trigger auto-run. This is intentional behavior to prevent large, unintended credit burns — importing a large source into a table with many enrichment columns could otherwise trigger a significant spend all at once. To process the remaining rows after import, manually run them: select all rows, right-click, and choose **Run [N] rows** — or right-click the first column in your workflow and select **Run column**. This same behavior applies to tables created by duplicating a workbook and then adding a source to the duplicate.

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
3.  Click `Download CSV`. Clay processes the export in the background and the file downloads automatically. The completed export is also saved to the **Exports** tab on your workspace homepage — select **Exports** from the left sidebar of your homepage to view and re-download recent exports.

**Why can't I see Export?** The most common cause is having one or more rows checked. The toolbar shows different options depending on row selection state: when no rows are selected, you see the `Tools` button with table-level functions such as Export and Import; when rows are selected, an `Actions` button appears instead with bulk row operations (Run rows, Debug, Delete rows). Uncheck all rows to restore access to Export.

**Long text or AI column data appears truncated or shows `[object Object]` in the export.** If a column stores enrichment or AI-generated output as nested structured data — such as the output of a Use AI, Claygent, or enrichment integration column — the CSV export may show only a short preview ending in "..." or the text `[object Object]` rather than the full value. Both occur when the export encounters a structured object rather than a plain extracted field.

To export the complete text, extract the specific field into a dedicated column first:

1.  In your table, click `+ Add column` and add a new column.
2.  Map it to the specific sub-field from the enrichment output (for example, the personalized message text from a Use AI column).
3.  Run the new column to populate it with the full text values.
4.  Export the table — the new column will contain the untruncated text in the CSV download.

**Export fails with an unexpected error.** If you encounter an unexpected error while exporting, your session may have expired. Log out of Clay and log back in, then retry the export. For full troubleshooting steps, see [Your session has expired error](workspace-administration-documentation.md#your-session-has-expired-error).

### Exporting a specific subset of contacts

To export only specific contacts from a table — for example, contacts at a particular company or contacts matching a custom condition — first narrow the view to those rows, then export.

**Step 1: Identify the contacts**

Use any of the following to target the rows you want:

-   **View filter:** Click **Filter** in the table toolbar and add conditions (for example, Company Name equals "Acme"). Only rows that match all conditions remain visible. See [Filter rows](table-columns-overview.md#filter-rows) for full syntax.
-   **Checkbox column:** Add a checkbox column (`+ Add column` → **Checkbox**), mark the rows you want, then filter where that column equals `true`.
-   **Formula column:** Add a formula column that evaluates to `true` for qualifying rows (for example, `{{Company Name}} === "Acme"`), then filter where that column is `true`.

**Step 2: Export the filtered contacts**

-   **Download as CSV:** With the filter active, click `Tools` → `Export` → `Download CSV`. The export uses the active view, so only the rows currently visible are included in the download.
-   **Route to another Clay table:** Add a [Send Table Data](send-table-data.md) column and set a run condition that targets the rows to export (for example, where a checkbox column is `true` or a formula column evaluates to `true`). Only matching rows are sent; others show "Run condition not met."
-   **Push to Google Sheets, Airtable, or a CRM:** Add the corresponding integration column with the same run condition. Only matching rows are pushed to the external destination.

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

### Does the "Find local businesses using Google Maps" source charge credits for businesses already in my table when I re-run or schedule it?

**No — the Google Maps source deduplicates results against every business it has previously found, so you are only charged for net-new businesses on each run.**

When you re-run or schedule a "Find local businesses using Google Maps" source, Clay checks each incoming result against the full history of businesses that source has ever imported. Businesses already in that history are skipped — they are not re-added to your table and no credits are charged for them. The success message *"The number of results added may be less than requested, as a result of deduping"* confirms this filtering occurred.

Key details:

-   **Deduplication is cumulative across all runs.** On every re-run (including scheduled runs), the source compares against every business it has ever found — not just the most recent run. A business found in week 1 is still tracked and skipped in week 52.
-   **Deduplication is tied to the source definition.** If you delete and re-add the source, or create a new source with the same search criteria, deduplication starts over. The new source has no history, so all businesses it finds are treated as new and credited accordingly.

### Why doesn't my Clay table update when I change the source filters?

**Editing the source of a Clay table after it's been run won't retroactively update the results, because Clay doesn't reprocess previously generated data automatically.**

Even if the source preview shows the new filters, the table won't refresh until you explicitly re-run the source. Rows already in the table **stay** — they are not automatically removed if they no longer match the updated filters (for example, companies that were part of a HubSpot list but have since been excluded by a filter change).

To control which rows are in your table after updating source filters, you have two options:

-   **Remove specific rows manually:** Apply a table filter to isolate rows you no longer want, select them, and delete them. This preserves the rest of your table without re-running the source.
-   **Reset the table to match current filters:** Delete all existing rows and re-run the source (or duplicate the table with the updated source). This clears the table and re-imports only records that match the current source filters. **For CRM, database, Google Sheets, Google Maps, and Find People sources (Salesforce, HubSpot, Snowflake, Google Sheets, Find local businesses using Google Maps, Find People):** deleting rows and re-running the same source will not re-add the deleted records — the source permanently tracks every record it has already imported. Duplicate the table (or delete and re-add the source) to get a fresh import history. See [I deleted rows from my table and re-ran the source, but they didn't reappear](#i-deleted-rows-from-my-table-and-re-ran-the-source-but-they-didnt-reappear) for more.

### Will rows already in my table be removed if they no longer match the source filter?

**No. Clay sources are additive only — they add rows (and optionally update them), but they never automatically remove rows from your table.**

If you narrow a source filter — for example, by updating a HubSpot list or segment so that certain contacts or companies no longer qualify — the rows already in your Clay table will stay. They are not deleted automatically.

The **Update existing rows** toggle (available when re-running a source) controls whether Clay refreshes the data in existing rows on re-run. It does not remove rows that are no longer included in the source.

To remove rows that no longer match your filter, you have two options:

-   **Delete them manually** — select the rows in the table and delete them.
-   **Delete and re-run the source** — this re-imports records based on the current filter. You will need to clear any previously imported rows first if you want a clean slate. **For CRM, database, Google Sheets, Google Maps, and Find People sources (Salesforce, HubSpot, Snowflake, Google Sheets, Find local businesses using Google Maps, Find People):** the source tracks previously imported records and will not re-add deleted rows even after re-running. Duplicate the table (or delete and re-add the source) instead.

### I deleted rows from my table and re-ran the source, but they didn't reappear

**For Salesforce, HubSpot, Snowflake, Google Sheets, Google Maps searches, Find People, and other CRM or database sources, re-running the same source after deleting rows will not restore those records.** Clay's import source tracks every record it has ever introduced to the table — including rows you've since deleted. When the source runs again, it recognizes and skips any record it has already seen, preventing both duplicate imports and unintentional revival of deleted rows.

When dedup blocks all records on a re-run, that run's **Rows Added** count in Source history shows **0** — not the number of records in your upstream source. The higher counts visible elsewhere in Source history are from earlier runs when those records were first imported. Your table can appear empty while Source history shows non-zero counts from past imports: the records were added in an earlier run and then deleted from the table, but the source still has them logged.

**To restore deleted records or get a fresh import:**

Duplicate the table (or delete and re-add the source). A new source definition starts with a clean record history, allowing the same records to be imported again. Before doing this, enable [auto-dedupe](table-management-settings.md) on a unique identifier column to avoid creating duplicates of rows still present in your table.

**Can I turn off source record tracking?** No — source-level deduplication for CRM and database sources cannot be disabled. The only path to re-import records a source has already seen is a fresh source definition (delete and re-add the source, or duplicate the table). If you want to disable the *table-level* deduplication that removes rows with duplicate column values, that is a separate setting — see [Auto-dedupe](table-management-settings.md#auto-dedupe) to toggle it on or off.

**Note:** This tracking behavior applies to **CRM and database sources** (Salesforce, HubSpot, Snowflake, and similar), to **Google Sheets sources** (which generate a unique ID per row by hashing the **"Fields to deduplicate by"** fields configured on the source), to **Google Maps sources** (Find local businesses using Google Maps), and to the **Find People** list builder source (which tracks previously-seen profiles and skips them on subsequent runs). **Find Companies** does not track records this way — deleting rows and re-running will re-import matching companies, subject to your table's auto-dedupe settings.

### My Google Sheets source found rows but fewer rows appear in my table than expected

Two separate behaviors can cause a Google Sheets source to report finding rows while fewer (or none) land in your table:

**Source-level deduplication: deleted rows not re-added**

The Google Sheets source generates a unique ID for each row by hashing the **"Fields to deduplicate by"** fields you configured when setting up the source. Clay tracks which IDs it has already imported, and subsequent runs — including runs after you delete rows from the table — skip any row whose hash was seen in a previous import. Deleting rows from the table does not clear this tracking.

To re-import the same rows after deleting them: delete the existing Google Sheets source and re-add it. A fresh source has no import history and will treat every matching row as new. Before re-adding, enable [auto-dedupe](table-management-settings.md) on a unique column (such as Email) to prevent duplicate rows if some rows are still in the table.

**Non-unique deduplication fields: rows collapsing into one**

If the fields you selected under **"Fields to deduplicate by"** are not unique per row — for example, if you selected **Company** and multiple rows in your sheet share the same company name — those rows produce identical hashes and collapse into a single record. The run history may report *N* rows found while only one row appears in your table per unique hash value.

To get one Clay row per sheet row, set **"Fields to deduplicate by"** to a field that is genuinely unique per record, such as **Email**, **LinkedIn Profile URL**, or a dedicated ID column. Avoid fields like Company or Title that many rows may share.

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

### Why did my source import fewer rows than the number of records it found?

**If your source found N records but only added fewer rows than expected, the most likely cause is that auto-dedupe is enabled on your table.** When auto-dedupe is active, Clay checks each newly added row against existing rows in the same table. If a new row has the same value in the dedupe column as an existing row, the duplicate is deleted — reducing the final row count below the number the source found. Clay indicates this with the message: *"The number of results added may be less than requested, as a result of deduping."*

**Note:** Auto-dedupe only deduplicates within the same table — it does not remove rows based on records in other tables or other tabs in your workbook.

To check or adjust your deduplication setting:

1.  Click the **gear icon** in the table footer (bottom-right), or open the table name dropdown and select **Edit table settings**.
2.  In the settings panel, find the **Deduplication** section.
3.  Toggle auto-dedupe off if you don't want deduplication, or change which column is used for matching.

For a full explanation of how auto-dedupe works — including column type requirements and simultaneous-insert limitations — see [Auto-dedupe](table-management-settings.md#auto-dedupe).

A second common cause of fewer-than-expected rows is hitting the 50,000-row source limit — see [What are the row limits for Clay tables and sources?](#what-are-the-row-limits-for-clay-tables-and-sources) below.

A third cause — specific to **CRM, database, and Google Sheets sources** (Salesforce, HubSpot, Snowflake, Google Sheets) that have been run at least once before — is **source record tracking**. Each CRM source definition remembers every record it has ever imported, including rows you've since deleted from the table. On subsequent runs, the source skips previously-seen records and only adds genuinely new ones. When all incoming records were previously imported by the same source definition, the run reports 0 rows added even though the source found records upstream. See [I deleted rows from my table and re-ran the source, but they didn't reappear](#i-deleted-rows-from-my-table-and-re-ran-the-source-but-they-didnt-reappear) for the fix.

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

For large ongoing Snowflake imports that regularly approach or exceed 50,000 records, consider [Audiences](audiences.md) instead of a standard table. Audiences scales to millions of records without per-source limits.

### Why did my source run automatically even though it's set to "Run manually"?

**"Run this source: Manually" only prevents the source from running on a recurring schedule — it does not prevent all forms of automatic triggering.**

The **Run this source** setting in the source panel controls the schedule:

-   **Manually** — the source will not run on a schedule. It runs when you click **Run now**, or when a non-schedule trigger fires.
-   **On a schedule** — the source runs automatically at the selected interval (hourly, daily, weekly, or monthly).

Beyond the schedule, sources can also run in response to other events. For example, if your Find People source uses a Clay companies table as its input (via the **Companies** filter), adding new rows to that input table can trigger the source to re-run for those new entries. This input-update trigger fires independently of the source's schedule setting.

**Note:** The table's **auto-run** setting is a separate control. It determines whether enrichment columns (action fields) run automatically when new rows arrive — it does not trigger sources. See [Auto-run](table-management-settings.md#auto-run) for more.

To investigate why a source ran unexpectedly, click the source column title and select **View Run History**.

### What happened to the Action button and Source option?

The toolbar button previously labeled **Action** has been renamed to **Tools** — this applies to all workspaces. Within the **Tools** panel, the tab previously labeled **Sources** is called **Import** in workspaces where the Functions feature is enabled (currently in beta — contact support to enable it); workspaces without Functions enabled continue to see a **Sources** tab in the same panel.
