---
title: Table management settings
description: Manage table settings including auto-dedupe, duplicate table, view graph, rename, edit description, view history, auto-delete, and navigating to a table by ID.
last_synced: 2026-04-26T01:40:46.622Z
---

# Table management settings

Manage table settings including auto-dedupe, duplicate table, view graph, rename, edit description, view history, and auto-delete.

## Access table management settings

You can access your table settings via your table settings dropdown.

-   For **workbooks**: Locate the table dropdown in the bottom workbook navigation bar.
-   For **tables**: Find the table dropdown in the left section of the top navigation bar.

You can also click the `⛭` icon in the top toolbar to open the Run Settings panel directly.

## Auto-dedupe

Auto-dedupe continuously monitors a specified column to detect and resolve duplicate values. When duplicates are found, Clay keeps one row and deletes the rest — you choose whether to keep the **oldest** or **newest** row (defaults to **Keep oldest row**). Blank cells, stale cells, and cells with more than 200 characters are excluded from this process.

**When does auto-dedupe fire?** Auto-dedupe runs whenever a row is added to the table **and** whenever a cell value in the dedupe column changes — including when a formula field or enrichment column fills in from an empty or stale state. This means if the dedupe column cell is blank or still processing when a row is first inserted, the duplicate check runs again automatically once the cell resolves. You don't need to manually trigger deduplication after a cell updates.

**Note — using an enrichment column as your dedupe key:** If the column selected for deduplication is populated by an enrichment action (for example, a "Find Website" enrichment that fills in a company's website URL), rows will be deduped as enrichment fills in those values. If multiple companies resolve to the same URL, only one row is kept and the rest are automatically deleted. To avoid unexpected row deletions, use a column that already contains a unique identifier before enrichment runs — such as company name, a social profile URL, or a CRM ID.

**View deduplication history:** To see which rows were removed by auto-dedupe, open the **History** panel (bottom-right of the table) and select **Row deduplication**. Each entry shows the deleted row, the column value that triggered the deletion, and the timestamp.

**Note — enabling auto-dedupe on a table with existing rows:** When you first set a dedupe column (or change it to a different column), Clay immediately runs deduplication against all existing rows in the table, retroactively removing any pre-existing duplicates. Before you save, the settings panel shows how many duplicate rows will be deleted so you can confirm the impact.

**Note:** Auto-dedupe only works with **Text**, **Email**, and **URL** column types. If the selected column uses a different data type (such as Number), auto-dedupe is automatically disabled. Convert the column to **Text** type first to use it for deduplication.

**Note:** The auto-dedupe toggle cannot be changed while the table is running. Stop the run first by clicking the **Stop** button in the run summary panel at the bottom-right of the table. If the toggle remains greyed out after the table has stopped, try a hard refresh (`Cmd+Shift+R` on Mac, `Ctrl+Shift+R` on Windows/Linux) to clear stale browser state.

To enable or disable auto-dedupe:

1.  Open the table name dropdown menu.
2.  Select `Edit table settings`.
3.  In the settings panel, find the **Auto-dedupe rows** toggle and turn it on or off.
4.  Select the column to be used for identifying duplicate values.
5.  Choose **Keep oldest row** or **Keep newest row** to set which duplicate is retained.

**Note:** Auto-dedupe monitors a **single column** only. If you need to deduplicate on a combination of fields — for example, treating each unique `OpportunityId + ContactId + Role` as a distinct row — use the **Uniqueness fields** setting in your source configuration instead (e.g., the [Salesforce SOQL source](salesforce-soql.md)). Source-level uniqueness fields apply at import time, before rows reach the table.

**Note — simultaneous row inserts:** Auto-dedupe may not catch duplicates when rows with the same value are added at the same time — for example, when a bulk import, a batch webhook, or concurrent sends push rows within milliseconds of each other. Each insert is processed in its own transaction and is not aware of the other before both are committed to the table, so both can slip through. This is a known limitation. As a workaround, add a dedupe or filter step in your workflow just before any downstream push (such as a CRM or email sequencer) to catch any duplicates that slip through.

## Auto-run

Auto-run controls whether enrichments fire automatically when rows are added or edited, keeping your table current. For complete documentation — including the run decision tree, table-level and column-level controls, "Keep existing results," the out-of-date indicator, the Update Existing Rows toggle, common scenarios, and best practices — see **[Auto-run](auto-run.md)**.

To quickly toggle auto-run: click the `⛭` icon in the top toolbar → toggle **Auto-run** on or off, then choose:

-   `Continue without running` — don't run existing stale cells right now.
-   `Update cells` — immediately queue all out-of-date cells to run.

## Duplicate table

When you duplicate a table, Clay copies the table structure and run settings — but **does not copy enriched data**. The duplicate starts empty; you'll need to manually trigger enrichments and source imports to populate it.

**What is copied:**
-   Column headers and their configuration (enrichment settings, formulas, conditional run logic)
-   Run settings, including the **Auto-run** toggle and "Keep existing results" setting
-   Scheduling configuration (if the table has a scheduled source import)

**What is not copied:**
-   Enriched data — enrichment columns start empty in the duplicate
-   Source import history — the duplicate starts with a fresh record count

**To copy existing enriched data without re-running enrichments:** Use [Send Table Data](send-table-data.md) to transfer rows from the original table to the duplicate. Add a Send Table Data column to the original table, select the columns you want to copy, and set the destination to the duplicate. This moves the already-computed cell values directly — the Send Table Data action itself consumes no credits. **Important:** Because auto-run carries over to the duplicate (see below), enrichment columns in the destination (such as Claygent) will automatically re-fire on incoming rows and consume credits unless you turn off auto-run in the duplicate — or disable it on individual enrichment columns you don't want to re-run — before sending data.

**Auto-run carries over:** Because run settings are preserved, if Auto-run was enabled in the original table, the duplicate will also have Auto-run enabled. To create a copy that starts in manual mode (useful for demos or templates), turn off Auto-run in the original table **before** duplicating — or turn it off in the duplicate immediately after creating it. See [Auto-run](auto-run.md) for how to toggle this setting.

**Connected sources (Salesforce, SOQL queries, and similar):** If a table has a Salesforce report, SOQL query, or other import source configured, duplicating copies the source configuration but does **not** automatically start the import. You will need to manually trigger the source in the duplicated table when you're ready to populate it with data.

**Webhook sources:** If a table has a webhook source column, duplicating generates a **brand new, unique webhook URL** for the copy. The original table's URL is not affected. Any external system sending data to the original URL will not automatically send to the new table — you need to update your sending tool to POST to the new URL. To find the new URL, click the webhook source column in the duplicate. See [Webhooks in Clay](webhook-integration-guide.md) for more details.

**Running a workflow on a new set of inputs:** Duplicating is also the recommended approach when you want to run an existing set of enrichment columns and automations on a completely different batch of data — for example, running the same people-finding and enrichment pipeline for a new city or a new target list. The duplicate starts with zero rows but all your column logic intact. After duplicating:

1.  In the duplicate, open the existing source column header and click **Edit source** to update the source to your new data — for example, swap in a different CSV file, change a location filter, or point it at a different reference table.
2.  Run the updated source. Your downstream enrichment columns, formulas, and conditional runs will repopulate automatically on the new rows without any rebuilding.

**Important:** Update the source by clicking **Edit source** in the source column header — do not add a second source alongside the existing one. Adding a new source leaves both active simultaneously; if you then delete the original, any downstream columns that reference it will break.

For workflows you want to run across many different input datasets over time, consider saving the downstream enrichment columns as a [Function](functions.md). Functions let you define the pipeline once and call it from multiple tables with different inputs, without re-creating the enrichment columns each time.

To duplicate a table:

1.  Click on the title of the table on the top left.
2.  Select `Duplicate table`.

**Duplicating a workbook:** To duplicate an entire workbook, open the workbook, click the workbook name in the top toolbar, and select `Duplicate`. Each table in the workbook is duplicated with the same behavior described above — structure and run settings are copied, enriched data is not, and connected sources don't automatically start importing. Note that workbooks with more than 10 tables cannot be duplicated by default; contact Clay support to raise this limit.

## View table graph

View Graph helps you visualize the enrichments and their relationships in your table. It enables you to explore data connections and edit directly within the graph.

To view your table graph:

1.  Open your table settings dropdown.
    -   If you're in a **table**, locate the dropdown in the top-left corner.
    -   If you're in a **workbook**, locate the dropdown in the bottom navigation bar.
2.  Select `View Graph`.

## Manage enrichments from table graph view

You can edit or add enrichments while using the graph view to refine your data.

**Edit existing enrichments:**

-   In the graph view, click on a node or connection to adjust relationships.
-   Modify enrichment settings directly to ensure the data meets your requirements.

**Add new enrichments:**

-   Switch back to the table view by closing the graph.
-   Click the `Add Enrichment` button in the top-right corner to create and configure new enrichments.

## Auto-delete (passthrough tables)

**Note:** This is a feature available to enterprise customers only.

Passthrough tables in Clay are a powerful feature designed to help you process and enrich large volumes of data efficiently.

They allow you to bypass the standard row limit by automatically processing incoming data, enriching it, and then forwarding it to a designated destination before deleting the original entries from the table.

This ensures your tables remain manageable while continuously handling new data.

**Note:** Passthrough features do not apply to CSVs, including bulk uploads at high volumes.

### How passthrough tables work

When enabled, passthrough tables fully bypass the 50,000 record import limit for data added via **webhooks**, **send table data**, or **signal sources**. Following is a step-by-step process of passthrough tables.

1.  **Data ingestion**: New rows are added to a Clay table via a compatible source.
2.  **Enrichment**: Clay runs all configured enrichments and operations on the new data.
3.  **Review interval**: Clay reviews the table to identify rows ready for passthrough after a 60-second interval.
    -   Criteria for passthrough: Rows that meet the following conditions are selected:
        -   The total number of rows in the table exceeds a specified threshold of 5,000 rows. If you need to raise the threshold, contact support.
        -   All enrichment processes have been completed for those rows.
4.  **Data transfer**: Selected rows are automatically transmitted to your designated destination (e.g., Snowflake, HubSpot, Google Sheets) via an API integration.
5.  **Deletion**: Once the data transfer is confirmed successful, the original rows are deleted from the Clay table.

### Enabling or disabling passthrough tables

To enable or disable passthrough tables:

1.  Open your table.
    -   To fully bypass the 50,000 record source limit, the table source must be **webhooks**, **send table data**, or a **signal source**. A warning appears if your table includes incompatible sources. See [auto-delete documentation](auto-delete.md) for details on source compatibility and warnings.
2.  Click the **auto-delete icon** (archive icon) in the bottom toolbar, or click the **table title** and select **Enable auto-delete** from the dropdown.
3.  In the auto-delete settings dialog, select your **Auto-delete mode**:
    -   **Disabled** — Rows will not be automatically deleted.
    -   **Delete when all actions finish** — Deletes rows once all action columns have finished running.
    -   **Delete based on conditional rules** — Deletes rows that match custom filter conditions you define.

    See [Auto-delete in tables](auto-delete.md) for details on each mode and additional configuration options.

## Rename your table

To rename your table:

1.  Open your table settings dropdown.
2.  Select `Rename` and enter your new table name.

## Edit table description

To edit your table description:

1.  Open your table settings dropdown.
2.  Select `Edit table description` and enter your new table description.

## View table history

Track changes to your table, including who made them and when. View updates to settings, column additions, updates, and deletions with AI-generated summaries.

**What you can track:**

-   Table settings (name, description, run settings)
-   Column additions, updates, and deletions
-   Detailed change diffs with AI summaries

**Retention:** Change log retention varies by plan:

-   Free / Trial: Not enabled
-   Starter, Explorer, Pro (legacy paid plans): 30 days
-   Launch / Growth: 30 days
-   Enterprise: 180 days

**To view table history:**

1.  Open your table.
2.  Click the `History` → `Change log`.
3.  Review the timeline of changes, including who made each change and when.
4.  Click `View details` to get more information.

For restoring your table to a previous configuration, see [Table versions](table-versions.md).

## Navigate to a table by ID

Every Clay table has a unique **table ID** (starting with `t_`). If you have a table's ID, you can open it directly in the Clay app by constructing a URL in this format:

```
https://app.clay.com/workspaces/<workspace_id>/tables/<table_id>
```

Replace `<workspace_id>` with your workspace ID and `<table_id>` with the table's ID. Paste the completed URL into your browser and you'll land directly on that table.

**Where to find your workspace ID:** Your workspace ID appears in the URL bar whenever you're inside Clay — for example, the `12345` in `https://app.clay.com/workspaces/12345/tables/...`.

**Where table IDs appear:**

-   In the browser URL bar when you're viewing the table — for example, the `t_abc123` in `https://app.clay.com/workspaces/12345/tables/t_abc123`.
-   In the **Origin** metadata field of a Clay record when that record was written to the table from another table. The `Origin` object contains a `Table Id` field (and `Originating Table Id`) that lets you trace a row back to the table that produced it.

**Note:** If the table is inside a workbook, the URL includes the workbook ID: `https://app.clay.com/workspaces/<workspace_id>/workbooks/<workbook_id>/tables/<table_id>`. Use whichever format matches the URL structure already visible in your browser when you are on that table.
