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

## Tips

### Always use / to reference a column

To reference a column's data in a run condition, **type `/` followed by the column name** (e.g., `/Domain`). This opens an inline picker and inserts a live reference to that column's data.

**If you type a column name without the leading `/`, it is treated as a literal text string — not a column reference.** The condition will silently compare against a fixed string instead of your actual data, and the enrichment will not behave as expected. Always use `/ColumnName` syntax.

**Example**: To run an enrichment only on rows that don't have a domain, set the condition to:

`/Domain is empty`

(where `/Domain` references the column named "Domain" in your table).

### Only matching rows consume credits

When a run condition is set, Clay only processes rows where the condition evaluates to **true**. Rows where the condition is not met are skipped and shown as **"Run condition not met"** — no credits are consumed for those rows.

This means clicking **"Run all rows"** with a condition in place is safe: Clay will only run (and charge credits for) the rows that actually match your condition.

### "Run condition not met" when you expect a row to trigger

This status means the formula evaluated successfully and returned **false** for that row — it is not a formula error. If rows you expect to match are being skipped, check two things:

**Every column referenced in the formula must have a value for that row.** If your condition is `/Publish Date >= /Cutoff Date` but the `/Cutoff Date` column is empty for that row, the comparison returns false. Open each column referenced in your formula and confirm it has a value for the rows that are being skipped.

**For OR conditions, both (all) branches must be false for the row to be skipped.** If a row shows "Run condition not met" on an `A OR B` condition, it means both `A` and `B` evaluated to false for that row — check each branch independently to find which referenced column is empty or evaluating unexpectedly.

### Running an action only once per row (new rows only)

Clay has no built-in "is new row" flag. To prevent an action column — such as sending a Slack message, writing to a CRM, or sending an email — from re-firing on rows it already processed, gate it on a **separate upstream column** that only has a value after the row was first processed:

`/My Upstream Column is not empty`

On new rows, the upstream column hasn't run yet, so the condition is false and the action waits. Once the upstream column runs and produces a value, the condition is true and the action fires.

**Important**: You cannot use a column's own previous output as its own run condition — Clay detects this as a circular dependency and will reject the configuration. The guard must be a different column.

**Simpler alternative for scheduled re-run tables**: If the root cause is that your action column is included in a scheduled re-run, the easiest fix is to uncheck it from the scheduled re-run list (Table Settings → Run Settings → Re-run columns on a schedule). Table-level Auto-run still fires the column for genuinely new rows. See [Scheduled columns](scheduled-columns.md).

## See also

[Conditional statements](https://www.clay.com/university/guide/conditional-statements)

[Comparison operators](https://www.clay.com/university/guide/comparison-operators)

[Logical operators](https://www.clay.com/university/guide/logical-operators)
