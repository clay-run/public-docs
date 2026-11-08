---
title: Scheduled columns
description: Automatically re-run your enrichments on a set schedule.
last_synced: 2026-04-26T01:40:37.281Z
---

# Scheduled columns

Automatically re-run your enrichments on a set schedule.

Scheduled columns let you automatically re-run specific columns or entire tables on a recurring basis.

This keeps your data current without manual updates (e.g., keeping enrichment data up-to-date like company headcount, funding info, or tech stack changes).

## Scheduling column runs

1.  While in a table, click the `⛭` icon in the top toolbar.
2.  Under `Run Settings`, select Re-run columns `on a schedule`.
3.  Choose the frequency to run:
    1.  Hour (Enterprise only)
    2.  Day
    3.  Week
    4.  Month
    5.  Custom — set a specific day of the week, time of day, and timezone (e.g., every Sunday at 6:00 AM Eastern Time).
4.  Decide whether you want to run `All columns` (the whole table) or `Only selected columns`.

**Note:** If the Hour option is not visible in your Run Settings, your current plan does not include hourly scheduling. On non-Enterprise plans, Day is the most frequent schedule available.

## Action columns and scheduled re-runs

Scheduled column re-runs fire for **every row** in the table on each cycle — including rows that already have successful results. Unlike table-level Auto-run, scheduled column runs always force-run and do not respect the "Keep existing results" option.

**Avoid including action columns in a scheduled re-run.** Columns that perform an external action — such as sending a Slack message, writing to a CRM, or sending an email — will fire for every row on every scheduled cycle, not just new rows. This can produce duplicate Slack messages, duplicate CRM records, or repeated emails on rows that were already processed.

To control this:

-   **Remove action columns from the scheduled re-run list.** Open **Table Settings** → **Run Settings** → **Re-run columns on a schedule** and uncheck any action columns. With table-level Auto-run enabled, the action column still fires automatically when a new row is added — it just won't repeat for all existing rows on every cycle.
-   **Add a run condition to the action column.** In the column's **Run settings**, enable `Only run if` and set a condition that's false once the action has already completed — for example, `/SlackMessage is empty`. This prevents the column from re-running on rows that already have a result, even if it's included in a scheduled re-run.

Scheduled columns are best suited for data enrichment columns where refreshing values over time is the goal — for example, headcount, funding data, or job titles.

## Downstream columns after a scheduled run

Scheduled column runs force-run **only the selected columns**. After the scheduled column completes and its output updates, downstream columns that reference it follow Clay's normal auto-run rules:

-   **Default mode (Auto-run on, "All columns"):** If the scheduled column's output changed for a row, downstream columns automatically re-run on those rows. If the output is unchanged, downstream columns stay up to date and are not re-triggered.
-   **"Keep existing results" mode:** Downstream columns that already have results are marked "out of date" but are **not** automatically re-run. The scheduled run does not cascade to them.
-   **Downstream column auto-run off:** The downstream column is marked "out of date" but requires a manual trigger.

**To make a downstream column re-run on the same recurring cycle as the upstream scheduled column**, add it to the scheduled run list (**Table Settings → Run Settings → Re-run columns on a schedule → Only selected columns**). Scheduled column runs always force-run, so the downstream column executes every cycle regardless of "Keep existing results."

To prevent the downstream column from running on every row on every cycle — for example, if you only want it to execute when the upstream value meets a condition — add a run condition. In the downstream column's **Run settings**, enable **Add run condition** and enter a formula that references the upstream column's value (for example, `Only run when [Sentiment] contains "BULLISH" & [Full Name] is not empty`). Clay evaluates the condition on each row and skips rows where it is not met, so you only consume credits for rows where the upstream result warrants it. See [Conditional runs](conditional-runs.md) for setup details.

## Troubleshooting

### Some rows show old timestamps after a scheduled run

Scheduled column reruns force-run every cell in the selected columns — they don't skip cells because a previous result already exists or because the input value looks the same as before. If specific rows still show an older "last updated" timestamp after a scheduled run completes, those cells were skipped due to one of the following conditions:

-   **Blank or missing inputs** — the cell's required input (such as a lookup key, email address, or referenced column value) is empty or could not be resolved. Clay skips the cell rather than running it with incomplete data.
-   **Unmet run condition** — the column has an **Only run if** condition configured, and that condition evaluated to false for the row. The cell is intentionally skipped, and no new timestamp is recorded.
-   **Formula or input validation error** — a formula feeding the column couldn't be evaluated (for example, a referenced column is missing, returns an unexpected type, or its value is invalid). The cell is skipped with an error status.

**To diagnose:** hover over or click into the cells in the affected rows to see their current status and any error messages. Fixing the underlying input — filling in a blank field, correcting the run condition, or resolving a formula error — will allow the next scheduled run to process those rows.

**Note:** A scheduled run completing successfully across the whole table does not guarantee every cell re-ran. The run itself fires for all rows, but individual cells with the issues above are skipped regardless.

## Usage limits

Each plan has a limit to the total number of tables with scheduled columns.

-   Starter: 100 tables
-   Launch: 100 tables
-   Growth: 100 tables
-   Enterprise: 1000 tables
