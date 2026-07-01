---
title: Run progress
description: Clay provides multiple ways to track and monitor run progress
  across your tables, including how to set a row limit to control which rows are
  processed, manually trigger unrun enrichment cells, run enrichments on a
  specific subset of rows, troubleshoot cells stuck in Queued status, diagnose
  enrichments that aren't triggering automatically, resolve persistent error
  messages by clearing the browser cache, and troubleshoot slow cell loading
  when using multiple tables in a workbook.
last_synced: 2026-04-26T01:40:34.620Z
---

# Run progress

Clay provides multiple ways to track and monitor run progress across your tables.

Clay provides multiple ways to track and monitor **run progress** across your tables. These tools help you confirm that columns are executing correctly, data remains current, and issues are quickly identified.

## Column progress bar

The progress bar gives you a snapshot of a column's current state. It shows:

-   Whether the column is actively running
-   The percentage of all rows in the table that have run (including rows not currently visible)
-   A breakdown of rows by status:
    -   🟢 **`Successful`** — The cell completed successfully.
        -   _Note: "Run condition not met" is also treated as a successful run_
    -   ⚪ **`Running`** — The cell is in progress or queued.
    -   🔴 **`Failed`** — The cell ran but encountered an error, such as:
        -   Missing required inputs
        -   Format/type errors
        -   Cell size limit exceeded
        -   Run timeout
        -   Other unexpected issues

Hovering over the progress bar displays a detailed status breakdown. This includes _all_ rows in the table, even if filters or row limits are applied.

**Formula & Derived Columns** — These calculate instantly. They don't display "Running" status or partial completion percentages. Instead, they appear with a ✅ once ready.

**Waterfall Columns** — The progress bar shows the overall percentage of all waterfall cells that have run.

For Sources and Signals, the status displayed depends on the update state:

-   **`Updating…`** — Actively refreshing
-   **`Waiting for events…`** — Monitoring for new events (applies to Signals + Webhooks only)
-   **`Up to date`** — Fully refreshed with the latest data

## **Run indicators**

Several icons can appear on the right side of the cell to indicate specific column statuses:

-   ⏯️ **icon:** The user has turned auto-update off for this column.
-   **Green timer icon:** This column runs automatically on a periodic schedule.
    -   Hover over the icon to see the frequency ("daily", etc.).
-   **⌨️ icon**: Basic column types with no formulas or input tokens are distinguished by this "manual entry" icon.

## **Table-level progress**

![](https://cdn.prod.website-files.com/687e604972375496b891fe58/691e65a876bd32a9f8e8f845_68ba32156edf36d6435cbe6b_Run%2520Progress%2520UI%2520Feedback%2520\(1\).png)

The table-level progress bar, shown at the bottom right of a table, provides a summary view of the entire table's run status. It displays:

-   The percentage of **all enrichment cells** in the table that have run.
    -   _Note: Includes non-visible rows, but not non-visible columns._
-   The percentage of rows by status (same definitions as at the column level).
-   Whether any column in the table is currently running.
-   **Run summary panel** — Hovering over the panel reveals:
    -   A detailed breakdown of status percentages.
    -   Table-level auto-run and scheduled run settings.
    -   A toggle to enable/disable column-level run status data.

## Stopping a run

To stop a running table, click the **Stop** button in the run summary panel at the bottom-right of the table.

**Important: clicking Stop does not immediately cancel enrichments that are already in progress.** When you click Stop, Clay cancels all queued cells that haven't been dispatched yet — but any enrichment calls already sent to an external data provider will run to completion and **will still consume credits**. You may see a short delay between clicking Stop and the table fully halting while these in-flight calls finish.

To prevent unintended credit usage before it starts, turn off [auto-run](table-management-settings.md) before importing large batches of rows. This prevents enrichments from triggering automatically on new data.

## Manually running unrun cells

The progress tooltip shows **"X% left to run"** — this figure represents enrichment cells that have not yet completed, including cells currently in progress and cells that haven't started at all. If [auto-run](table-management-settings.md) is disabled, cells won't start automatically; you'll need to trigger them manually.

To manually run the remaining cells for a specific column:

1.  **Right-click** the enrichment column header.
2.  Select **Run column** → **Run [N] empty or out-of-date rows**.

    This triggers all cells in that column that are:
    -   **Empty** — never been run
    -   **Errored** — previously ran but encountered an error
    -   **Out-of-date** (also referred to as **stale**) — the cell ran before but is no longer current. In the UI, out-of-date cells show a clock icon with the tooltip "This cell is out of date." A cell becomes out of date when its inputs have changed since it last ran, or when auto-run is disabled and the cell hasn't been re-triggered. For a full explanation, see the **Understanding the out-of-date indicator** section in [Table management settings](table-management-settings.md).

3.  Repeat for each enrichment column you want to run.

> **Note:** There is no single button to run all columns at once — this option must be used column by column.

**Alternative — enable auto-run:** Turn on `Auto-run` in your [table settings](table-management-settings.md) and choose `Update cells` to immediately queue any out-of-date cells.

## Running enrichments on specific rows

To run enrichment or waterfall columns on a targeted subset of rows — for example, to test a configuration on a small sample or re-run rows that returned unexpected results:

1.  **Select the rows** you want to run: click a row number to select it, then drag or **Shift+click** to extend the selection across a range.
2.  **Right-click** anywhere on the selected rows and choose **Run [N] rows**.

This triggers all enrichment and waterfall columns on those rows only, leaving other rows unaffected.

**To run a single column on specific rows only**, select the cells in that column for your target rows, then right-click → **Run [N] cells**.

## Setting a row limit

If you want to process only a portion of your table — for example, to find emails for the first 1,000 rows before committing credits to a full run — use the **Row limit** and **Starting row** settings in the toolbar.

Click the **rows** button in the table toolbar (it shows the count of currently visible rows out of the total, for example **6,236/6,236 rows**). A popover opens with two fields:

-   **Starting row** — The row to start from. Leave blank to begin at row 1. Enter a number to skip ahead — for example, enter `1001` to start processing from row 1,001 onward.
-   **Row limit** — The maximum number of rows to include. Enter `1000` to cap the table at 1,000 rows. Leave blank (or click **Show all rows**) to remove the limit.

Click **Save changes** to apply. The toolbar updates to show the new visible count (for example, **1,000/6,236 rows**), and enrichments will only run on those rows going forward.

To remove the limit and return to the full table, click **Show all rows** in the same popover.

> **Note:** The column and table-level progress bars always count _all_ rows in the table — including rows outside your current row limit. The limit controls which rows are visible and eligible to run, but the progress percentages reflect the full table.

## Troubleshooting cells stuck in Queued status

Cells show a **Queued** status when they are waiting to be processed. This is normal when running large tables — Clay processes many rows concurrently, but rows still queue when the system is handling prior requests or when an external API is rate-limiting responses. In most cases the queue resolves automatically.

If cells remain Queued for an extended period, common causes include:

-   **High concurrency in progress** — Clay runs many rows at once; if a large number are queued simultaneously, later rows wait while earlier ones complete. The queue will clear on its own.
-   **External API rate limits** — Integrations such as OpenAI or HubSpot enforce per-minute request limits. For Clay's managed integrations (where Clay provides the API key), Clay handles this automatically and the queue resumes once the rate-limit window resets. If you are using your own API key, Clay may send requests faster than your account's tier allows — rows that exhaust the retry window return a **"Rate limit wait time exceeded"** error. To prevent this on enrichment columns that support it (such as HTTP API), configure the **Custom rate limit** setting on the column to match your provider's tier; see [Enrichments](enrichments.md) for details. For AI enrichments using a personal API key, see [AI tokens](ai-tokens.md).
-   **API quota exhausted** — If you've hit a quota ceiling (e.g., OpenAI, Google), new runs are blocked until the quota resets or is increased in the provider's dashboard.
-   **Auto-run settings** — If auto-run is enabled and triggering repeated re-runs, rows may accumulate in the queue unexpectedly. See [Table management settings](table-management-settings.md) for how to adjust auto-run and scheduled run behavior.
-   **Column edited or stopped mid-run** — If a column's settings were changed while a run was in progress, or if a run was stopped partway through, some rows may remain stuck in Queued status and not resume on their own.

> **Note on CPJ source previews:** When previewing a CPJ source column (Companies, People, or Jobs search) in the Sculptor column builder, previews are capped at **50 per hour** on trial and free plans, and **5,000 per hour** on paid plans. This cap applies only to interactive previews in the column builder — it does not apply to "Run column" or right-click → "Run [N] rows" on table rows.

**To unblock a stuck queue:**

1.  **Wait a few minutes** — Active processing usually clears the backlog without intervention.
2.  **Hard refresh the page** — Press `Ctrl+Shift+R` (Windows/Linux) or `Cmd+Shift+R` (Mac) to reload and clear any stale browser state.
3.  **Force-run the column** — Right-click the column header and select **Run column** → **Force run all [N] rows**. This re-queues and processes every row in the column regardless of its current status. Credits are charged for every row re-run at the standard rate; the UI displays the estimated cost before you confirm.
4.  **Check your API quotas** — If the column calls an external API (OpenAI, Google, etc.), verify you haven't exhausted a quota in that provider's dashboard.
5.  **Check the Clay status page** — If the issue persists and you suspect a platform-wide problem, visit [status.clay.com](https://status.clay.com/) for real-time updates on any active incidents.

**If rows remain Queued after a mid-run stop or column edit:** To process only the stuck rows without re-running ones that already completed, use the "is queued" filter to scope the run:

1.  Click **Filter** in the table toolbar, select the affected column, and set the condition to **is queued**. Only the stuck rows are now visible.
2.  Right-click the column header and select **Run column** → **Force run all [N] rows**. With the "is queued" filter active, this re-runs only the visible queued rows — completed rows are not re-run.
3.  Remove the filter when the run finishes.

> **Note:** **Run column → Run [N] empty or out-of-date rows** will not work here — queued rows are classified as "running," not as empty or stale, so that option shows 0 eligible rows and does nothing for this scenario. Use **Force run all [N] rows** instead.

## Troubleshooting: table appears stopped at a partial percentage with no credits consumed

If your table completes at a partial percentage — for example, 20–40% — and no credits are being consumed, enrichment cells have likely failed with `ERROR_MISSING_INPUT`. This error means a required input field is blank for those rows.

**`ERROR_MISSING_INPUT` cells are counted as Failed (🔴)** in the progress bar — the table has already processed those cells, just without a result. Clay does not charge credits for these cells, because the enrichment aborts before calling the external data provider.

**Most common cause: source data not yet populated**

This frequently happens when using a template or pre-built workflow where enrichment columns depend on data that hasn't been sourced yet. A typical pattern:

-   Your table includes person-enrichment columns — email finder, LinkedIn profile lookup, personalized message generator — that require inputs such as a LinkedIn URL, first name, or work email.
-   You've run a **Find Companies** source but haven't yet run **Find People** to populate person records in the table.
-   With no person data available, every person-enrichment column immediately fails with `ERROR_MISSING_INPUT`.

**How to resolve it:**

1.  Click the failing enrichment column header and check which input fields it requires (for example, "LinkedIn URL" or "First Name").
2.  Make sure the upstream column or source providing that data — typically a **Find People** run — has completed first.
3.  Once the required input data is in place, right-click the enrichment column header → **Run column** → **Run [N] empty or out-of-date rows** to re-process those cells.

> **Tip:** Clay's [Sculptor](sculptor.md) can analyze your table structure and identify what's missing. Click **Chat with Sculptor** in the top-right corner of your table.

## Troubleshooting: enrichments not triggering automatically despite auto-run being enabled

If your enrichment columns are configured with auto-run enabled but cells still show as out-of-date and nothing runs automatically, check whether the **table itself** is in Manual mode.

**The table-level Auto-run setting is the master switch.** When the table is in Manual mode, the top navigation bar displays a **Manual** badge — and no column in that table will run automatically, regardless of how individual column auto-run settings are configured.

To re-enable automatic enrichment:

1.  Click the `⛭` icon in the top toolbar (or click the table name → **Run Settings**).
2.  Toggle **Auto-run** on.
3.  Choose:
    -   **Update cells** — immediately queue all out-of-date cells to run.
    -   **Continue without running** — leave existing stale cells as-is and only auto-run future changes.

After enabling table-level auto-run, column-level settings take effect: columns with auto-run on will trigger automatically; columns with auto-run off will still require a manual trigger.

For the full auto-run decision tree and advanced options (conditional runs, "Keep existing results"), see [Table management settings](table-management-settings.md).

## Troubleshooting: identifying rows that errored vs. rows with no data

When a column's progress bar shows failed rows (🔴), you may need to find exactly *which* rows hit a specific error — for example, "The result of this run exceeded the cell size limit (200 kB)" — without catching rows that legitimately returned no data.

Add a formula column using `Clay.getCellStatus()` and point it at the affected enrichment column:

```
Clay.getCellStatus({{Your Column}})
```

This returns a status string for each cell. Cells that hit the cell size limit return `"ERROR_ACTION_OUTPUT_DATA_SIZE_LIMIT_EXCEEDED"`; cells that ran successfully but found nothing return `"SUCCESS_NO_DATA"`; cells with data return `"SUCCESS"`. Filter or sort the table on this formula column to isolate the error rows without catching legitimate empty results.

For the full list of `getCellStatus()` return values, see [Formulas](formula-generator.md).

## Troubleshooting: persistent error messages

If an error message stays visible after the underlying issue has been resolved — for example, after reauthorizing a connection, correcting a run setting, or confirming that a run has completed — the cause is usually stale browser state. Clearing your browser cache and refreshing the page resolves this in most cases.

**To clear cache and refresh:**

1.  **Clear your browser cache** — Open your browser settings, navigate to the Privacy or History section, and select **Clear browsing data**. Check **Cached images and files**, then clear. In Chrome, you can navigate directly to `chrome://settings/clearBrowserData`.
2.  **Refresh the page** — Press `Ctrl+R` (Windows/Linux) or `Cmd+R` (Mac) after clearing, or use a hard refresh (`Ctrl+Shift+R` / `Cmd+Shift+R`) to bypass the cache without clearing it entirely.

If the error persists after clearing the cache and refreshing, visit [status.clay.com](https://status.clay.com/) to check for any active platform incidents.

## Troubleshooting: slow cell loading with multiple workbook tables

Cell data may take longer to appear when a workbook contains large tables and multiple enrichments are running at the same time. Enrichment runs share a fixed pool of concurrency slots across your workspace — when many enrichments are active simultaneously, incoming requests queue behind earlier ones, which manifests as visible latency in loading cell data.

Performance impact is more pronounced with larger tables and more complex workflows, such as workbooks where tables are linked together (for example, a companies table feeding into a people table).

**To troubleshoot:** Hard refresh the page — press `Ctrl+Shift+R` (Windows/Linux) or `Cmd+Shift+R` (Mac) to reload and clear any stale browser state.
