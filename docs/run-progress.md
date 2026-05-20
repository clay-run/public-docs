---
title: Run progress
source_url: https://university.clay.com/docs/run-progress
description: Clay provides multiple ways to track and monitor run progress
  across your tables, including how to manually trigger unrun enrichment cells.
last_synced: 2026-04-26T01:40:34.656Z
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

Seeing cells "left to run" in the progress bar does **not** mean those cells are actively running — it means they have not been executed yet and are waiting. Cells won't run automatically if [auto-run](table-management-settings.md) is disabled for the table or column.

To manually run the remaining cells for a specific column:

1.  **Right-click** the enrichment column header.
2.  Select **Play** → **Run empty or out-of-date rows**.

    This triggers all cells in that column that are:
    -   **Empty** — never been run
    -   **Errored** — previously ran but encountered an error
    -   **Stale** — previously ran successfully, but an input value has changed since then

3.  Repeat for each enrichment column you want to run.

> **Note:** There is no single button to run all columns at once — this option must be used column by column.

**Alternative — enable auto-run:** Turn on `Auto-run` in your [table settings](table-management-settings.md) and choose `Update cells` to immediately queue any out-of-date cells.
