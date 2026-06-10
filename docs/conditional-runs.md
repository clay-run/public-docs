---
title: Conditional runs
source_url: https://university.clay.com/docs/conditional-runs
description: Add programmable logic to your Clay workflows.
last_synced: 2026-04-26T01:39:47.459Z
---

# Conditional runs

Add programmable logic to your Clay workflows.

## What are conditional runs?

Conditional runs allow you to execute specific actions or enrichments in a workflow only if certain conditions are met, helping you add programmable logic to your workflows.

## Applications

**Upload to CRM**: Add a contact only if it has a valid email.

-   **Condition**: `{{email}} is not empty`

**Sequencer Filtering**: Add leads to a sequence based on lead score or industry.

-   **Condition**: `{{lead_score}} > 80 AND {{industry}} == "SaaS"`

**Write to Table**: Populate a column only if the lead's region matches a target location.

-   **Condition**: `{{region}} == "North America"`

**Round-Robin Assignments**: Create a column for each rep and use a conditional run for actions based on assignments.

-   **Condition**: `{{assigned_rep}} == "Kareem"`

**Send a Slack message or other action only for new rows**: Run an action only once per row by gating it on an upstream column that only has a value after the row has been processed.

-   **Condition**: `/Upstream Column is not empty`

## How do they work?

Conditional runs are built on **Conditional statements** and evaluate a condition as true or false to determine whether to execute or skip an action.

### Structure of conditional runs

Conditional runs are structured like an **if-else statement**:

`if (conditional statement is true) {`

`run the enrichment`

`} else {`

`don't run the enrichment`

`}`

To create a conditional statement within the **Conditional formula generator**:

**Reference Dynamic Variables**

-   Use / to select variables or columns from your workflow, such as {{company\_size}} or {{revenue}}.
-   These variables dynamically adapt based on your data.

**Apply Comparison Operators**

-   Compare values using operators like equals, greater than, or not equal to.
-   Example: `{{company_size}} > 500`.

**Combine with Logical Operators (Optional)**

-   Add complexity to your conditions with:
    -   **AND**: Requires all conditions to be true.
    -   **OR**: Passes if at least one condition is true.
    -   **NOT**: Reverses a condition (e.g., `NOT {{status}} == "Closed"`).

## How do I use conditional runs?

**Step 1: Open the Conditional runs editor**

Navigate to the **Run Settings** of the action you want to configure and click on "Use AI".

**Step 2: Define the conditional logic**

Define the logic that determines how the condition will evaluate.

**Step 3: Generate the Formula**

Click **"Generate formula"** to automatically translate your condition into a formula.

**Step 4: Verify the Output**

Look at the sample outputs on the right to ensure your condition behaves as expected.

Adjust your condition as needed based on the results.

**Note:** The preview uses data loaded when the panel was opened and may not reflect the most recent values in your columns. If upstream columns have run or changed since you opened the editor, the preview can show stale results that don't match what actually evaluates at runtime. See the **Formula preview may not match runtime results** tip below.

## Tips

### Always use / to reference a column

To reference a column's data in a run condition, **type `/` followed by the column name** (e.g., `/Domain`). This opens an inline picker and inserts a live reference to that column's data.

**If you type a column name without the leading `/`, it is treated as a literal text string — not a column reference.** The condition will silently compare against a fixed string instead of your actual data, and the enrichment will not behave as expected. Always use `/ColumnName` syntax.

**Example**: To run an enrichment only on rows that don't have a domain, set the condition to:

`/Domain is empty`

(where `/Domain` references the column named "Domain" in your table).

### Formula preview may not match runtime results

The preview in the run condition editor is built from the column values loaded when you opened the panel — it does not refresh automatically as your table runs. If upstream columns have run or changed since you opened the editor, the preview can show stale or incomplete results.

For formulas that reference many columns, or that depend on complex values like waterfall outputs or nested lists, the preview may also resolve references differently than the actual runtime evaluation does.

**If the preview looks wrong, don't assume your formula is broken.** Save the condition, run a few test rows, and check the table for the **"Run condition not met"** status on the cells you expect to be skipped. The actual run results are the authoritative source — the preview is a best-effort guide, not a guarantee.

### Only matching rows consume credits

When a run condition is set, Clay only processes rows where the condition evaluates to **true**. Rows where the condition is not met are skipped and shown as **"Run condition not met"** — no credits are consumed for those rows.

This means clicking **"Run all rows"** with a condition in place is safe: Clay will only run (and charge credits for) the rows that actually match your condition.

### "Run condition not met" cells appear empty to downstream columns

When a run condition is not met, Clay skips the enrichment and stores **no output** for that row — the cell value is empty. Any downstream columns that reference this cell (formula columns, waterfall columns, CRM push columns, etc.) will receive an empty value for those rows.

**This is why downstream columns that depend on this data will show empty results for those rows.** The row itself still appears in any downstream column, but the value fed into it from the skipped enrichment is empty — so any formula, waterfall step, or output that requires this data will produce no result for that row.

**Note:** If a row previously ran and produced output, that output is preserved when the condition is not met on a subsequent run — the run condition only gates new executions and does not clear existing cell data.

### Running an action only once per row (new rows only)

Clay has no built-in "is new row" flag. To prevent an action column — such as sending a Slack message, writing to a CRM, or sending an email — from re-firing on rows it already processed, gate it on a **separate upstream column** that only has a value after the row was first processed:

`/My Upstream Column is not empty`

On new rows, the upstream column hasn't run yet, so the condition is false and the action waits. Once the upstream column runs and produces a value, the condition is true and the action fires.

**Important**: You cannot use a column's own previous output as its own run condition — Clay detects this as a circular dependency and will reject the configuration. The guard must be a different column.

**Simpler alternative for scheduled re-run tables**: If the root cause is that your action column is included in a scheduled re-run, the easiest fix is to uncheck it from the scheduled re-run list (Table Settings → Run Settings → Re-run columns on a schedule). Table-level Auto-run still fires the column for genuinely new rows. See [Scheduled columns](scheduled-columns.md).

### "Only run if" re-evaluates each time an upstream column changes

With **Auto-run** enabled, Clay re-evaluates an action column's "Only run if" condition each time a value in the current row changes — including each time an upstream enrichment column finishes running. The condition is **not a one-time gate**: if it evaluates to `true` on multiple occasions as different enrichments complete, the action column can run multiple times on the same row.

**Consequence for webhook and HTTP API export columns**: If you gate a webhook on upstream enrichments being done, it can fire more than once per row. To ensure the action fires only once, use the guard-column pattern from [Running an action only once per row](#running-an-action-only-once-per-row-new-rows-only): gate the action on a formula column that only becomes non-empty once all required upstream work is finished.

**When upstream enrichments have their own run conditions**: If an upstream enrichment was skipped because its own "Only run if" condition wasn't met, `Clay.getCellStatus()` returns `"ERROR_RUN_CONDITION_NOT_MET"` for that cell — not `"SUCCESS"` or `"SUCCESS_NO_DATA"`. To gate a downstream action on "enrichment finished, whether it ran or was skipped," check for each possible final state explicitly. See [Formulas](formula-generator.md) for the full list of `getCellStatus()` return values.

### Gating a run on data from another table

Run conditions can only reference columns in the **current row** — there is no formula syntax that directly queries another table from inside a run condition.

**Workaround**: Add a **Lookup Multiple Rows in Other Table** enrichment column to your current table first. That column queries the other table and stores a match count in the current row. You can then reference it in your run condition like any other column.

**Example**: You have a companies table and a people table. You want an enrichment to run only for companies that have at least one matching person in the people table.

1. In your companies table, add a **Lookup Multiple Rows in Other Table** enrichment column:
   - `Table to search` → your people table
   - `Target column` → the column to match on in the people table (e.g., `Company Domain`)
   - `Filter operator` → `Equals`
   - `Row value` → the matching column in your companies table (e.g., your `Domain` column)
2. Run the lookup column to populate results.
3. On the enrichment you want to gate, open **Run settings → Only run if** and set:

   `/People Lookup is not empty`

   (using `/` followed by the name you gave the lookup column)

The enrichment will now only fire for rows where the lookup returned at least one match.

**See also**: [Lookup Rows](lookup-rows.md) — full reference for single-row and multiple-row lookup patterns, including using lookups as suppression gates.

### Column stops running after a referenced column is deleted

If a run condition formula references a column that has been **deleted** from the table, the column stops running and its cells show **"Invalid input"** status. Opening the cell details panel shows a **"Conditional run errors"** message listing the missing field — for example: *"[Column name] is missing."* Downstream columns that depend on this column will also appear out of date.

**To fix:**

1. Click the column header → **Edit column** → open **Run settings**.
2. Find the **"Only run if"** formula — it will contain a reference to a column that no longer exists in the table.
3. Delete the broken condition by clicking the **×** next to it, or click **Use AI** to recreate it using a valid column reference.
4. Save the column.

Once saved, cells will clear the "Invalid input" state and run normally on the next trigger.

**Tip:** Before deleting a column, check whether any other columns reference it in a run condition. Open each dependent column's **Run settings** and update or remove conditions that point to the column you're about to delete.

## See also

[Conditional statements](https://www.clay.com/university/guide/conditional-statements)

[Comparison operators](https://www.clay.com/university/guide/comparison-operators)

[Logical operators](https://www.clay.com/university/guide/logical-operators)
