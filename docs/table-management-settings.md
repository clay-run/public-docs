---
title: Table management settings
description: Manage table settings like rename, auto-dedupe, auto-run,
  auto-delete, and table descriptions.
last_synced: 2026-04-26T01:40:46.622Z
---

# Table management settings

Manage table settings like rename, auto-dedupe, auto-run, auto-delete, and table descriptions.

## Access table management settings

You can access your table settings via your table settings dropdown.

-   For **workbooks**: Locate the table dropdown in the bottom workbook navigation bar.
-   For **tables**: Find the table dropdown in the left section of the top navigation bar.

You can also click the `⛭` icon in the top toolbar to open the Run Settings panel directly.

## Auto-dedupe

Auto-dedupe continuously monitors a specified column to detect and resolve duplicate values. When duplicates are found, Clay keeps one row and deletes the rest — you choose whether to keep the **oldest** or **newest** row (defaults to **Keep oldest row**). Blank cells, stale cells, and cells with more than 200 characters are excluded from this process.

**When does auto-dedupe fire?** Auto-dedupe runs whenever a row is added to the table **and** whenever a cell value in the dedupe column changes — including when a formula field recalculates from an empty or stale state to its final value. This means if a formula field is blank or still processing when a row is first inserted, the duplicate check runs again automatically once the formula resolves. You don't need to manually trigger deduplication after a formula updates.

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

Auto-run automatically runs enrichments whenever rows are added or edited, keeping your table current. You can control this feature at multiple levels: table-level (master control), column-level (individual control), and through conditional logic.

### How Clay decides whether a cell runs

Every time a source runs or re-runs, Clay walks through a short decision tree before executing any enrichment cell. Understanding this flow helps you predict exactly which cells will fire — and which will be skipped.

**Step 1 — New or existing row?**

-   **New row** (no matching ID in the table): Clay skips ahead to step 2.
-   **Existing row** (matching ID already present):
    -   If **"Update existing rows"** is **off**: the row is untouched. Existing data is preserved and no action columns are triggered.
    -   If **"Update existing rows"** is **on**: the source column is updated with the latest source data, then Clay proceeds to step 2.

**Step 2 — Table-level auto-run**

-   If the table's **Auto-run toggle is off** (shows "Manual"): the cell is marked stale and skipped. It will only run on a manual click.
-   If the table's **Auto-run toggle is on** (shows "Auto-run"): Clay checks the **"Keep existing results"** checkbox.
    -   **"Keep existing results" checked**: only cells that are new, empty, or errored are eligible to run. Cells with an existing successful result are preserved and skipped.
    -   **"Keep existing results" unchecked** (default): all cells are eligible; Clay proceeds to step 3.

**Step 3 — Column-level auto-run**

-   If the **column's Auto-run toggle is off**: the cell is marked stale and skipped (only runs on a manual click).
-   If the **column's Auto-run toggle is on** (default): **the cell runs**.

**Note: Adding a source to an existing table auto-runs enrichments on the first 10 rows only.** When you import a data source into a table that already exists — including tables created by duplicating a workbook and then adding a source afterward — Clay automatically queues enrichments for only the **first 10 imported rows**. The remaining rows are added to the table but do not trigger auto-run. This is intentional behavior to prevent unexpected credit burns: importing a large source into a table with many enrichment columns could otherwise trigger a significant spend all at once. To process the remaining rows, manually run them: select all rows in the table, right-click, and choose **Run [N] rows** — or right-click the first column in your workflow and select **Run column**.

### Table-level auto-run (master control)

Table-level auto-run acts as the master switch that controls automatic enrichment for the entire table.

-   When **enabled**: Enrichments run automatically whenever rows are added or edited.
    -   When the "**Keep existing results**" option is enabled, only errored, empty, or new cells can run automatically. Cells that already have existing data **will not** run automatically.
-   When **disabled**: You must manually click cells to trigger enrichments.
-   **Default setting**: Enabled by default — Clay is designed to automatically enrich data as soon as it arrives.

**Note:** There is no workspace-wide setting to disable auto-run across all tables at once. Auto-run must be configured individually for each table.

**To enable or disable table-level auto-run:**

**Note:** The Auto-run toggle cannot be changed while the table is actively running. Stop the run first by clicking the **Stop** button in the run summary panel at the bottom-right. If the toggle remains greyed out after stopping, try a hard refresh (`Cmd+Shift+R` on Mac, `Ctrl+Shift+R` on Windows/Linux) to clear stale browser state.

1.  Click the `⛭` icon in the top toolbar, or click the table name and navigate to **Run Settings**.
2.  Toggle the `Auto-run` mode.
3.  If enabling, choose:
    -   `Continue without running` — Don't run existing cells right now.
    -   `Update cells` — Immediately run all cells that are out-of-date.

**Note:** Rows added while auto-run was disabled are **not** automatically queued when you re-enable auto-run. Choosing `Continue without running` leaves those rows unrun — they will not trigger on the next source sync. To process them, either choose `Update cells` when re-enabling, or manually trigger the column (right-click the column header → **Run column** → **Run N empty or out-of-date rows**).

**To enable "Keep existing results":**

"Keep existing results" is only available when Auto-run is turned on. To enable it:

1.  Click the `⛭` icon in the top toolbar (or click the table name → **Run Settings**).
2.  Make sure the `Auto-run` toggle is **on**.
3.  Check the **"Keep existing results"** checkbox.
    -   With this checked: only empty, errored, or new cells run automatically — cells with existing successful results are skipped.
    -   With this unchecked (default): all cells are eligible to run, including ones that already have results.

**Tip:** Enable "Keep existing results" before uploading new rows to an existing table if you don't want to re-run enrichments on rows that are already complete. This prevents accidental full-table re-runs and protects your credits.

**Understanding the out-of-date indicator**

The out-of-date clock indicator on a cell means the cell is stale — it has an existing result but auto-run is not re-running it. The most common cause is "Keep existing results" being enabled: Clay skips cells that already have a result rather than overwriting them and spending credits. The cell's current value is still usable downstream; other columns can reference it normally.

A cell also shows as out of date when its inputs have changed since it last ran — for example, if an upstream column with auto-run enabled re-ran and updated its values, or if the column's own configuration was modified (such as editing a prompt). In these cases the indicator is informational: the existing value is still valid and usable downstream. In many cases re-running would produce the same result, so only trigger a re-run if you specifically need fresh output.

**Manual tables and sequential column runs:** If your table is in Manual mode and you run enrichment columns one at a time from left to right, you may see the out-of-date indicator appear across most columns — including ones you've already run. This is expected behavior, not a bug. Every time you run an upstream column, Clay immediately marks all downstream columns that depend on it as out of date, because their inputs may have changed. In a table where columns feed sequentially into each other (for example, a scoring table), running them in order creates a wave of stale indicators that propagates forward as you work. **Your data is not broken**: cell values marked out of date because auto-run is off are still valid and can be referenced by other columns without blocking downstream runs.

Since the table is in Manual mode, these indicators won't auto-clear. A few options:

-   **Ignore the icons** if the values look correct — the clock icon in this context is a workflow indicator, not a data quality signal.
-   **Run all columns in order** — right-click each column header from left to right and select **Run column → Run [N] empty or out-of-date rows** to clear all stale indicators in one pass.
-   **Switch to auto-run with "Keep existing results"** — turn on Auto-run and check **Keep existing results**. The table will then automatically queue only empty, errored, or new cells when dependencies change, without re-running (and spending credits on) cells that already have results.

If a cell **keeps** showing as out of date even after you re-run it, check whether an upstream column has auto-run enabled. Each time that upstream column runs and updates its output, Clay marks any column referencing it as out of date again — even one you just re-ran. To resolve this:

-   **Disable auto-run on the downstream column** — the column will only run when you trigger it manually. This is the most targeted fix and leaves the upstream column untouched.
-   **Disable auto-run on the upstream column** — stops the cascade at its source, but means the upstream column also switches to manual-only mode.
-   **Enable "Keep existing results"** at the table level — cells with existing results are no longer automatically re-run, so the stale indicator appears but no credits are consumed re-running the column on every upstream change.

**Note:** Changing "Keep existing results" does **not** automatically re-run cells already showing the out-of-date indicator — the new setting only applies to future auto-run triggers. To refresh currently stale cells:

-   **Disable "Keep existing results"** (uncheck it): a prompt appears asking whether you'd like to update out-of-date cells — click **Update cells** to immediately queue all stale cells.
-   **Run from the column header**: right-click the enrichment column header → **Run column** → **Run [N] empty or out-of-date rows**.
-   **Re-trigger auto-run**: toggle Auto-run off, then back on, and choose **Update cells** to queue all currently stale cells.

**Understanding the manually-overwritten indicator**

When you type a value directly into a cell that has a formula — or paste values in bulk into a formula column — Clay treats each entered value as an intentional override and suspends the column's formula for those cells. Affected cells display a pencil icon; hovering over it shows the tooltip "This cell's value has been manually overwritten."

While a cell is in this state:

-   **The formula is suspended for that cell.** Auto-run skips overwritten cells — they are not queued to run, do not consume credits, and do not trigger downstream columns.
-   **The manually entered value is treated as the row's authoritative value.** Other columns can still reference it, but the formula that drives this column will not re-evaluate for that row.

**To restore a cell to its formula-driven state:** hover over the cell and click the ↺ **Reset to original value** button. This clears the overwrite state and allows the formula to re-run on the next auto-run trigger.

**Why this commonly appears:** When you paste data in bulk into a formula column — for example, pasting email addresses into a waterfall lookup column — Clay marks each pasted cell as overwritten to preserve your input. If enrichments stop running for pasted rows, look for the pencil icon and use the ↺ **Reset to original value** button to resume formula-driven behavior for those cells.

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

When you duplicate a table, Clay copies the table structure and run settings — but **does not copy enriched data**. The duplicate starts empty; you'll need to manually trigger enrichments and source imports to populate it.

**What is copied:**
-   Column headers and their configuration (enrichment settings, formulas, conditional run logic)
-   Run settings, including the **Auto-run** toggle and "Keep existing results" setting
-   Scheduling configuration (if the table has a scheduled source import)

**What is not copied:**
-   Enriched data — enrichment columns start empty in the duplicate
-   Source import history — the duplicate starts with a fresh record count

**To copy existing enriched data without re-running enrichments:** Use [Send Table Data](send-table-data.md) to transfer rows from the original table to the duplicate. Add a Send Table Data column to the original table, select the columns you want to copy, and set the destination to the duplicate. This moves the already-computed cell values directly — the Send Table Data action itself consumes no credits. **Important:** Because auto-run carries over to the duplicate (see below), enrichment columns in the destination (such as Claygent) will automatically re-fire on incoming rows and consume credits unless you turn off auto-run in the duplicate — or disable it on individual enrichment columns you don't want to re-run — before sending data.

**Auto-run carries over:** Because run settings are preserved, if Auto-run was enabled in the original table, the duplicate will also have Auto-run enabled. To create a copy that starts in manual mode (useful for demos or templates), turn off Auto-run in the original table **before** duplicating — or turn it off in the duplicate immediately after creating it. See [Auto-run](#auto-run) for how to toggle this setting.

**Connected sources (Salesforce, SOQL queries, and similar):** If a table has a Salesforce report, SOQL query, or other import source configured, duplicating copies the source configuration but does **not** automatically start the import. You will need to manually trigger the source in the duplicated table when you're ready to populate it with data.

**Webhook sources:** If a table has a webhook source column, duplicating generates a **brand new, unique webhook URL** for the copy. The original table's URL is not affected. Any external system sending data to the original URL will not automatically send to the new table — you need to update your sending tool to POST to the new URL. To find the new URL, click the webhook source column in the duplicate. See [Webhooks in Clay](webhook-integration-guide.md) for more details.

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
