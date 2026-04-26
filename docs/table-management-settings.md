---
title: Table management settings
source_url: https://university.clay.com/docs/table-management-settings
last_synced: 2026-04-26T01:40:46.376Z
upstream_hash: 91b61f42ba6de20fc97b66bb2f08fd0583dbc7d76ebd27b5618f1935e1af8d28
---

# Table management settings

Manage table settings like rename, auto-dedupe, auto-run, auto-delete, and table descriptions.

## Access table management settings

You can access your table settings via your table settings dropdown.

-   For **workbooks**: Locate the table dropdown in the bottom workbook navigation bar.
-   For **tables**: Find the table dropdown in the left section of the top navigation bar.

## Auto-dedupe

Auto-dedupe continuously monitors a specified column to detect and resolve duplicate values by retaining the oldest row and deleting the duplicates. Blank cells and cells with more than 200 characters are excluded from this process.

To enable or disable auto-dedupe:

1.  Open your table settings dropdown.
2.  Click the table dropdown menu and select `Enable/Disable auto-dedupe`.
3.  Toggle the auto-dedupe setting on or off.
4.  Select the column to be used for identifying duplicate values.

## Auto-run

Auto-run automatically runs enrichments whenever rows are added or edited, keeping your table current. You can control this feature at multiple levels: table-level (master control), column-level (individual control), and through conditional logic.

### Table-level auto-run (master control)

Table-level auto-run acts as the master switch that controls automatic enrichment for the entire table.

-   When **enabled**: Enrichments run automatically whenever rows are added or edited.
    -   When the "**Keep existing results**" option is enabled, only errored, empty, or new cells can run automatically. Cells that already have existing data **will not** run automatically.
-   When **disabled**: You must manually click cells to trigger enrichments.
-   **Default setting**: Enabled by default — Clay is designed to automatically enrich data as soon as it arrives.

**To enable or disable table-level auto-run:**

1.  Click the table name to access table settings.
2.  Under the Run Settings section, toggle the `Auto-run` mode.
3.  If enabling, choose:
    -   `Continue without running` — Don't run existing cells right now.
    -   `Update cells` — Immediately run all cells that are out-of-date.

### Column-level auto-run (individual control)

Column-level auto-run controls whether a specific enrichment runs automatically. This setting only works when table-level auto-run is enabled.

**To enable or disable column-level auto-run:**

1.  Click the name of the column → `Edit column`.
2.  Toggle auto-run on/off under `Run settings`. Click `Save` to apply your changes.

**Important:** Table-level auto-run acts as the parent setting:

-   If table-run is **OFF**: No columns will run automatically, regardless of column settings.
-   If table-level is **ON** + column-level is **OFF**: That specific column won't run automatically.
-   If table-level is **ON** + column-level is **ON**: Column runs automatically. ✅

### Conditional runs ("Only run if")

Add conditional logic to control when an enrichment executes. The enrichment only runs when the formula evaluates to true.

**Common use cases:**

-   Only run if LinkedIn URL exists: `LinkedIn URL is not empty`
-   Only run if company size > 50: `Company Size > 50`
-   Only run if email is missing: `Email is empty`
-   Only run for specific industries: `Industry = "Technology"`

**To set up conditional runs:**

1.  In column settings (`Edit column`), enable `Only run if` under `Run settings`.
2.  Click `Use AI` to write the formula in plain language, or write the formula manually using column references.
3.  Click `Save` — the enrichment now only runs when the condition is met.

**Why this matters:** Conditional runs help control costs by preventing enrichments from running when data already exists or conditions aren't met.

### Update Existing Rows toggle (for scheduled source imports)

For tables with scheduled source imports, the `Update existing rows` toggle controls whether scheduled source runs will overwrite existing records with the same identifier.

**Two options:**

-   **Update Existing Rows: ON** ("All") — Re-runs enrichments on all rows with each scheduled run. Use for ongoing data hygiene and backfills. Higher credit usage.
    -   **Note**: You likely will want to turn off the "**Keep existing results**" auto-run option for this scenario so that enrichments will re-run for existing rows that receive an update from your source.
-   **Update Existing: OFF** ("Net New") — Only runs enrichments on newly added records. Skips existing records. Lower credit usage — more cost-efficient.

**To configure Update Existing:**

1.  Open your source column → `Edit column` → `Sources`.
2.  Toggle `Update Existing` on or off based on your needs.

### Common scenarios

**Full automation:**

-   Table-level: ✅ ON
-   All columns: ✅ ON
-   Conditional runs: Not set
-   **Result**: New rows → All enrichments run automatically

**Selective automation:**

-   Table-level: ✅ ON
-   Email column: ✅ ON
-   Other columns: ❌ OFF
-   **Result**: New rows → Only email enrichment runs automatically

**Manual control (testing mode):**

-   Table-level: ❌ OFF
-   Column-level: ✅ ON (doesn't matter)
-   **Result**: New rows → Must manually click cells to run enrichments

**Conditional execution:**

-   Table-level: ✅ ON
-   Column-level: ✅ ON
-   Conditional run: "Only if LinkedIn URL exists"
-   **Result**: Rows with LinkedIn URL → Enrichment runs; Rows without → Skipped

### Best practices

**When building/testing tables:**

1.  Turn table-level auto-run OFF to prevent accidental credit usage.
2.  Add sample data (5-10 rows).
3.  Manually test enrichments by clicking cells.
4.  Refine your setup.
5.  Turn auto-run ON when ready for production.

**When running production workflows:**

1.  Turn table-level auto-run ON.
2.  Configure column-level toggles strategically.
3.  Use conditional logic (`Only run if`) for cost control.
4.  Monitor credit usage.

**For credit control:**

-   Use `Only run if` conditions extensively.
    -   Example: `Email is empty` — only find email when missing.
    -   Example: `Company Size > 50` — only enrich companies in your ICP.
-   For table auto-run, we recommend having the "Keep existing results" option checked to avoid accidentally overwriting data and wasting credits.

## Duplicate table

**Note:** Duplicating a table will only copy the sources. You cannot duplicate all of the data within a table.

To duplicate your table:

1.  Click on the title of the table on the top left.
2.  Select `Duplicate table`.

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

When enabled, passthrough tables operate on data added via webhooks. Following is a step-by-step process of passthrough tables.

1.  **Data ingestion**: New rows are added to a Clay table through webhooks.
2.  **Enrichment**: Clay runs all configured enrichments and operations on the new data.
3.  **Review interval**: Clay reviews the table to identify rows ready for passthrough after a 60-second interval.
    -   Criteria for passthrough: Rows that meet the following conditions are selected:
        -   The total number of rows in the table exceeds a specified threshold of 5,000 rows. If you need to raise the threshold, contact support.
        -   All enrichment processes have been completed for those rows.
4.  **Data transfer**: Selected rows are automatically transmitted to your designated destination (e.g., Snowflake, HubSpot, Google Sheets) via an API integration.
5.  **Deletion**: Once the data transfer is confirmed successful, the original rows are deleted from the Clay table.

### Enabling or disabling passthrough tables

To enable or disable passthrough tables:

1.  Open your table with webhooks as the source.
    -   Ensure that the table you want to configure has webhooks set as its data source. Passthrough features only work with tables where the source is webhooks.
2.  Navigate to the bottom navigation panel and select `Enable auto-delete`.
3.  Within the auto-delete settings, enable `Automatic Row Deletion`.
    -   This action activates the passthrough functionality by ensuring that rows are automatically deleted after processing and transferring.

## Rename your table

To rename your table:

1.  Open your table settings dropdown.
2.  Select `Rename` and enter your new table name.

## Edit table description

To edit your table description:

1.  Open your table settings dropdown.
2.  Select `Edit table description` and enter your new table description.

## View table history

Track changes to your table, including who made them and when. View updates to settings, columns, and enrichments with AI-generated summaries.

**What you can track:**

-   Table settings (name, description, run settings)
-   Column additions, updates, and deletions
-   Detailed change diffs with AI summaries

**Retention:** Change log retention varies by plan:

-   Free / Trial: Not enabled
-   Launch / Growth: 30 days
-   Enterprise: 180 days

**To view table history:**

1.  Open your table.
2.  Click the `History` → `Change log`.
3.  Review the timeline of changes, including who made each change and when.
4.  Click `View details` to get more information.
