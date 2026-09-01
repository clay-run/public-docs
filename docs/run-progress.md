---
title: Run progress
description: Clay provides multiple ways to track and monitor run progress
  across your tables, including how to use the built-in Errored rows view to
  filter to failed rows, set a row limit to control which rows are processed,
  manually trigger unrun enrichment cells, run enrichments on a specific subset
  of rows, troubleshoot cells stuck in Queued status, recover action column cells
  stuck in Queued status when the Stop button is grayed out, diagnose enrichments
  that aren't triggering automatically, resolve persistent error messages by
  clearing the browser cache, and troubleshoot slow cell loading when using
  multiple tables in a workbook.
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

## Filtering to errored rows

Every Clay table includes a built-in **Errored rows** view that instantly filters the table to show only rows where at least one enrichment cell failed. Use this view to quickly identify and investigate failed runs without manually setting up a filter.

To open the Errored rows view:

1.  Click the view selector dropdown at the top of the table toolbar (it shows the name of your current view, for example **Default view**).
2.  Select **Errored rows**.

The table immediately updates to display only rows with at least one 🔴 Failed cell. Click any red cell to open the **Cell Details** panel and read the specific error message for that row.

To re-run only the errored rows, select them (click a row number, then **Shift+click** to extend the selection) and right-click → **Run [N] rows**. Alternatively, right-click any enrichment column header and choose **Run column** → **Run [N] empty or out-of-date rows** to re-run just that column for all currently visible errored rows.

To return to the full table, click the view selector again and choose **Default view** or **All rows**.

**For automated error monitoring:** Enterprise workspaces can use [table alerts](table-alerts.md) to receive notifications when a column's failure rate exceeds a configured threshold — so you're alerted to errors without checking the table manually.

## Stopping a run

To stop a running table, click the **Stop** button in the run summary panel at the bottom-right of the table.

**Important: clicking Stop does not immediately cancel enrichments that are already in progress.** When you click Stop, Clay cancels all queued cells that haven't been dispatched yet — but any enrichment calls already sent to an external data provider will run to completion and **will still consume credits**. You may see a short delay between clicking Stop and the table fully halting while these in-flight calls finish.

**If the Stop button appears greyed out with the tooltip "No runs are in progress for this table" while cells still show Running or Synthesizing status, this is expected during AI column runs.** The Stop button only becomes active when requests are actively in-flight (already dispatched to a data provider). During large Claygent or AI column runs, Clay dispatches rows in small concurrent batches through a rate limiter. Between batches, no requests are in-flight, so the button temporarily deactivates even though queued cells remain. The run will continue automatically — to stop it, wait for the Stop button to become active between batches and click it then.

To prevent unintended credit usage before it starts, turn off [auto-run](auto-run.md) before importing large batches of rows. This prevents enrichments from triggering automatically on new data.

## Manually running unrun cells

The progress tooltip shows **"X% left to run"** — this figure represents enrichment cells that have not yet completed, including cells currently in progress and cells that haven't started at all. If [auto-run](auto-run.md) is disabled, cells won't start automatically; you'll need to trigger them manually.

To manually run the remaining cells for a specific column:

1.  **Right-click** the enrichment column header.
2.  Select **Run column** → **Run [N] empty or out-of-date rows**.

    This triggers all cells in that column that are:
    -   **Empty** — never been run
    -   **Errored** — previously ran but encountered an error
    -   **Out-of-date** (also referred to as **stale**) — the cell ran before but is no longer current. In the UI, out-of-date cells show a clock icon with the tooltip "This cell is out of date." A cell becomes out of date when its inputs have changed since it last ran, or when auto-run is disabled and the cell hasn't been re-triggered. For a full explanation, see the **Understanding the out-of-date indicator** section in [Auto-run](auto-run.md).

3.  Repeat for each enrichment column you want to run.

> **Note:** There is no single button to run all columns at once — this option must be used column by column.

**Alternative — enable auto-run:** Turn on `Auto-run` in your [run settings](auto-run.md) and choose `Update cells` to immediately queue any out-of-date cells.

## Running enrichments on specific rows

To run enrichment or waterfall columns on a targeted subset of rows — for example, to test a configuration on a small sample or re-run rows that returned unexpected results:

1.  **Select the rows** you want to run: click a row number to select it, then drag or **Shift+click** to extend the selection across a range.
2.  **Right-click** anywhere on the selected rows and choose **Run [N] rows**.

This triggers all enrichment and waterfall columns on those rows only, leaving other rows unaffected.

**To run a single column on specific rows only**, select the cells in that column for your target rows, then right-click → **Run [N] cells**.

**If an enrichment column shows a clock icon after "Run [N] rows" and doesn't complete**, this typically occurs on tables with auto-run turned off (shown as **Manual** in the top navigation bar). When Clay runs a row, it dispatches upstream columns first. While upstream columns are in progress, Clay marks any downstream columns that depend on them as out-of-date. On manual tables, those downstream columns are not automatically re-triggered after the upstream run finishes — leaving a clock icon that doesn't resolve on its own. On tables with auto-run enabled, downstream cells can re-run automatically after upstream columns complete.

**To run enrichments on specific rows when a column has upstream dependencies, use the filter + run column approach instead:**

1.  Click **Filter** in the table toolbar and add conditions that match only the rows you want — for example, filter by name, company, or any field that identifies your target rows.
2.  Right-click the enrichment column header and choose **Run column** → **Run [N] empty or out-of-date rows**.

Running the column directly rather than the rows bypasses the dependency timing issue — the column run executes as a manual trigger and processes all visible rows in the current filtered view, regardless of the table's auto-run setting.

Remove the filter when the run finishes to return to the full table view.

## Setting a row limit

If you want to process only a portion of your table — for example, to find emails for the first 1,000 rows before committing credits to a full run — use the **Row limit** and **Starting row** settings in the toolbar.

Click the **rows** button in the table toolbar (it shows the count of currently visible rows out of the total, for example **6,236/6,236 rows**). A popover opens with two fields:

-   **Starting row** — The row to start from. Leave blank to begin at row 1. Enter a number to skip ahead — for example, enter `1001` to start processing from row 1,001 onward.
-   **Row limit** — The maximum number of rows to include. Enter `1000` to cap the table at 1,000 rows. Leave blank (or click **Show all rows**) to remove the limit.

Click **Save changes** to apply. The toolbar updates to show the new visible count (for example, **1,000/6,236 rows**), and enrichments will only run on those rows going forward.

To remove the limit and return to the full table, click **Show all rows** in the same popover.

> **Note:** The column and table-level progress bars always count _all_ rows in the table — including rows outside your current row limit. The limit controls which rows are visible and eligible to run, but the progress percentages reflect the full table.

> **Note for function tables:** If you're viewing a function's live view and see a count like **1,000/1,000 rows**, this is a different behavior from the user-set row limit described above. Function tables prune older processed rows once the live view reaches 1,000 rows — this is intentional and not a limit you configured. To retain and view historical runs, enable archiving in the function table's auto-delete settings. See [Is there a row limit for functions?](functions.md#is-there-a-row-limit-for-functions) for full details.

## Troubleshooting cells stuck in Queued status

Cells show a **Queued** status when they are waiting to be processed. This is normal when running large tables — Clay processes many rows concurrently, but rows still queue when the system is handling prior requests or when an external API is rate-limiting responses. In most cases the queue resolves automatically.

**If enrichments across multiple tables or workbooks appear stuck at the same time**, check **[status.clay.com](https://status.clay.com/)** before troubleshooting individual tables — simultaneous stalling across tables is often caused by a platform-wide incident. If an incident is active, the Clay team is already working on a fix and no further action is needed on your end.

If cells remain Queued for an extended period, common causes include:

-   **High concurrency in progress** — Clay runs many rows at once; if a large number are queued simultaneously, later rows wait while earlier ones complete. The queue will clear on its own.
-   **External API rate limits** — Integrations such as OpenAI or HubSpot enforce per-minute request limits. For Clay's managed integrations (where Clay provides the API key), Clay handles this automatically and the queue resumes once the rate-limit window resets. If you are using your own API key, Clay may send requests faster than your account's tier allows — rows that exhaust the retry window return a **"Rate limit wait time exceeded"** error. To prevent this on enrichment columns that support it (such as HTTP API), configure the **Custom rate limit** setting on the column to match your provider's tier; see [Enrichments](enrichments.md) for details. For AI enrichments using a personal API key, see [AI tokens](ai-tokens.md).
-   **API quota exhausted** — If you've hit a quota ceiling (e.g., OpenAI, Google), new runs are blocked until the quota resets or is increased in the provider's dashboard.
-   **Auto-run settings** — If auto-run is enabled and triggering repeated re-runs, rows may accumulate in the queue unexpectedly. See [Auto-run](auto-run.md) for how to adjust auto-run and scheduled run behavior.
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

**If action column cells are stuck in Queued status and the Stop button is grayed out:** The Stop button becomes active when there are active run records in the queue. If an action column — a column that pushes data to an external system such as a CRM or marketing platform (for example, Update Marketo or Update HubSpot) — shows cells in "Queued..." status but the Stop button in the run summary panel is grayed out, those cells' run records are no longer present. There is nothing for Stop to cancel, and force-running the column will not clear these cells either.

To recover from this state:

1.  Right-click the action column header and select **Duplicate column**. The duplicate starts with a fresh queue state and no stuck entries.
2.  Delete the original column. Deleting removes the stuck entries.

The duplicate keeps your column settings. Once you have deleted the original, check the duplicate's auto-run setting before triggering it to confirm it is configured as expected.

## Troubleshooting: table appears stopped at a partial percentage with no credits consumed

If your table completes at a partial percentage — for example, 20–40% — and no credits are being consumed, enrichment cells have likely failed with `ERROR_MISSING_INPUT`. This error means a required input field is blank for those rows.

**`ERROR_MISSING_INPUT` cells are counted as Failed (🔴)** in the progress bar and appear in filtered views of errored rows — the table has already processed those cells, just without a result. Clay does not charge credits for these cells, because the enrichment aborts before calling the external data provider.

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

## Troubleshooting: cells showing "Some inputs missing"

When a cell shows **"Some inputs missing"**, a required input token in the column's settings is blank for that row. The column stopped before taking any action — no external API call was made and no credits were consumed.

Despite being a "stopped before running" state, these rows are classified as Failed (🔴) and appear in filtered views of errored rows. This is expected behavior: the status indicates the column could not proceed, not that an enrichment failed.

**To resolve rows showing "Some inputs missing":**

-   **Make the input optional.** Open the column settings and find the input field that is blank for those rows. Turn off its **Required to run** toggle. The column will run for all rows; for rows where that input is blank, the column proceeds without it.
-   **Add a run condition.** Add a [run condition](conditional-runs.md) so the column only fires when the required input has a value. Rows without that input will show **"Run condition not met"** instead — and unlike "Some inputs missing," that status is treated as a successful skip (🟢), so those rows no longer appear in errored row views.
-   **Consolidate inputs spread across multiple enrichment columns using a Merge column.** If the required input value exists in your table but lands in different columns per row — for example, an Org ID that one enrichment provider returns in one column while another provider returns it in a different column — the single column you mapped as the input will be blank on rows where the other provider ran. Add a [Merge column](table-columns-overview.md#merge-columns) that combines every column holding that input value; it returns the first non-empty value per row. Then re-map the enrichment's input to the merged column so it receives the value regardless of which source populated it.

## Troubleshooting: cells showing "Waiting for another column to finish"

When a cell shows **"Waiting for another column to finish"**, the column depends on an upstream column that is still running or queued. The cell is blocked and will not run until the upstream column completes — no action is needed on your part if the upstream column is actively processing.

This status most commonly appears on formula columns that extract values from a Clay Function column that is in **"Awaiting Callback"** state. Because the formula cannot calculate until the function returns a result, every row where the function is still processing shows **"Waiting for another column to finish"** in those dependent formula cells.

**To confirm the upstream column is the cause:**

1.  Look across the same row for an enrichment or function column whose cells show **"Awaiting Callback"**, **"Queued"**, or **"Running"** status.
2.  Once that upstream column finishes processing for the row, the dependent cells automatically recalculate and the **"Waiting for another column to finish"** status clears on its own.

**If the upstream column is a Clay Function stuck in "Awaiting Callback"**, see [What does "Awaiting Callback" mean on a function column?](functions.md#what-does-awaiting-callback-mean-on-a-function-column) for how to re-run or unblock it.

**If you need a column to run regardless of whether the upstream column has returned a value**, add or adjust a [run condition](conditional-runs.md) on the dependent column so it no longer waits on that upstream result.

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

For the full auto-run decision tree and advanced options (conditional runs, "Keep existing results"), see [Auto-run](auto-run.md).

## Troubleshooting: diagnosing column errors with Troubleshoot with AI

When a cell shows a 🔴 Failed status, clicking the cell opens the **Cell Details** panel, which displays the specific error message for that row. Reading the error message is the fastest way to understand what went wrong — for example, a missing required input, an invalid configuration, or an upstream column that hasn't run yet.

For additional help interpreting the error and getting step-by-step fix instructions, click the **Troubleshoot with AI** button at the bottom of the Cell Details panel. Clay sends the error context to an AI that returns concise, numbered suggestions for resolving the issue — typically pointing to a missing input, a column configuration change, or an upstream column that needs to run first. Available to all users on all plans.

**Troubleshoot with AI** is available for most error types. It does not appear for credit limit errors or compliance errors, which have dedicated resolution paths shown in the panel instead.

## Troubleshooting: identifying rows that errored vs. rows with no data

When a column's progress bar shows failed rows (🔴), you may need to find exactly *which* rows hit a specific error — for example, "The result of this run exceeded the cell size limit (200 kB)" — without catching rows that legitimately returned no data.

Add a formula column using `Clay.getCellStatus()` and point it at the affected enrichment column:

```
Clay.getCellStatus({{Your Column}})
```

This returns a status string for each cell. Cells that hit the cell size limit return `"ERROR_ACTION_OUTPUT_DATA_SIZE_LIMIT_EXCEEDED"`; cells that ran successfully but found nothing return `"SUCCESS_NO_DATA"`; cells with data return `"SUCCESS"`. Filter or sort the table on this formula column to isolate the error rows without catching legitimate empty results.

For the full list of `getCellStatus()` return values, see [Formulas](formula-generator.md).

To capture the error message text itself — for example, to forward the exact failure reason to a Slack notification or surface it in another column — use `Clay.getCellErrorMessagePreview()` in a formula column pointed at the failing enrichment:

```
Clay.getCellErrorMessagePreview({{Your Column}})
```

This returns up to 300 characters of the error text from a failed cell — the same message visible in the Cell Details panel when you click a red cell. `Clay.getCellStatus()` tells you *that* a cell errored and which error code; `Clay.getCellErrorMessagePreview()` tells you *why* — the human-readable error text. For full details and limitations, see [Formulas](formula-generator.md).

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
