---
title: Conditional runs
source_url: https://university.clay.com/docs/conditional-runs
description: Add programmable logic to your Clay workflows.
last_synced: 2026-04-26T01:39:47.459Z
upstream_hash: 5a8e8235bc00404d0e39059d0c5c20c6b6ae07159087118cdf762af5cd1f99de
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

**Write to Table**: Populate a column only if the lead’s region matches a target location.

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

`don’t run the enrichment`

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

Navigate to the **Run Settings** of the action you want to configure and click on “Use AI”.

**Step 2: Define the conditional logic**

Define the logic that determines how the condition will evaluate.

**Step 3: Generate the Formula**

Click **“Generate formula”** to automatically translate your condition into a formula.

**Step 4: Verify the Output**

Look at the sample outputs on the right to ensure your condition behaves as expected.

Adjust your condition as needed based on the results.

## See also

[Conditional statements](https://www.clay.com/university/guide/conditional-statements)

[Comparison operators](https://www.clay.com/university/guide/comparison-operators)

[Logical operators](https://www.clay.com/university/guide/logical-operators)
