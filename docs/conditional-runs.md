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

## See also

[Conditional statements](https://www.clay.com/university/guide/conditional-statements)

[Comparison operators](https://www.clay.com/university/guide/comparison-operators)

[Logical operators](https://www.clay.com/university/guide/logical-operators)
