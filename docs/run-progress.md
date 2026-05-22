---
title: Run progress
source_url: https://university.clay.com/docs/run-progress
description: Clay provides multiple ways to track and monitor run progress
  across your tables, including how to manually trigger unrun enrichment cells,
  run enrichments on a specific subset of rows, and troubleshoot cells stuck in
  Queued status.
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

## Manually running unrun cells

The progress tooltip shows **"X% left to run"** — this figure represents enrichment cells that have not yet completed, including cells currently in progress and cells that haven't started at all. If [auto-run](table-management-settings.md) is disabled, cells won't start automatically; you'll need to trigger them manually.

To manually run the remaining cells for a specific column:

1.  **Right-click** the enrichment column header.
2.  Select **Run column** → **Run [N] empty or out-of-date rows**.

    This triggers all cells in that column that are:
    -   **Empty** — never been run
    -   **Errored** — previously ran but encountered an error
    -   **Stale** — previously ran successfully, but an input value has changed since then

3.  Repeat for each enrichment column you want to run.

> **Note:** There is no single button to run all columns at once — this option must be used column by column.

**Alternative — enable auto-run:** Turn on `Auto-run` in your [table settings](table-management-settings.md) and choose `Update cells` to immediately queue any out-of-date cells.

## Running enrichments on specific rows

To run enrichment or waterfall columns on a targeted subset of rows — for example, to test a configuration on a small sample or re-run rows that returned unexpected results:

1.  **Select the rows** you want to run: click a row number to select it, then drag or **Shift+click** to extend the selection across a range.
2.  **Right-click** anywhere on the selected rows and choose **Run [N] rows**.

This triggers all enrichment and waterfall columns on those rows only, leaving other rows unaffected.

**To run a single column on specific rows only**, select the cells in that column for your target rows, then right-click → **Run [N] cells**.

## Troubleshooting cells stuck in Queued status

Cells show a **Queued** status when they are waiting to be processed. This is normal when running large tables — Clay processes many rows concurrently, but rows still queue when the system is handling prior requests or when an external API is rate-limiting responses. In most cases the queue resolves automatically.

If cells remain Queued for an extended period, common causes include:

-   **High concurrency in progress** — Clay runs many rows at once; if a large number are queued simultaneously, later rows wait while earlier ones complete. The queue will clear on its own.
-   **External API rate limits** — Integrations such as OpenAI or HubSpot enforce per-minute request limits. Clay respects these automatically; the queue resumes once the rate-limit window resets.
-   **API quota exhausted** — If you've hit a quota ceiling (e.g., OpenAI, Google), new runs are blocked until the quota resets or is increased in the provider's dashboard.
-   **Auto-run settings** — If auto-run is enabled and triggering repeated re-runs, rows may accumulate in the queue unexpectedly. See [Table management settings](table-management-settings.md) for how to adjust auto-run and scheduled run behavior.

**To unblock a stuck queue:**

1.  **Wait a few minutes** — Active processing usually clears the backlog without intervention.
2.  **Hard refresh the page** — Press `Ctrl+Shift+R` (Windows/Linux) or `Cmd+Shift+R` (Mac) to reload and clear any stale browser state.
3.  **Force-run the column** — Right-click the column header and select **Run column** → **Force run all [N] rows**. This re-queues and processes every row in the column regardless of its current status.
4.  **Check your API quotas** — If the column calls an external API (OpenAI, Google, etc.), verify you haven't exhausted a quota in that provider's dashboard.
