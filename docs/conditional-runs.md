---
title: Conditional runs
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

**Skip enrichment for personal or free email addresses**: Prevent an enrichment from running on rows where the email address belongs to a free-provider domain — Gmail, Yahoo, Outlook, Hotmail, and similar. This ensures credits are spent only on rows that carry a work or professional email.

1.  Add a **Formula column** — for example, named "Is Personal Email" — that checks whether the email domain is a free provider and returns `true` for personal addresses and `false` for work addresses. See [Conditional statements](conditional-statements.md) for an example formula using `contains` to match domains like `gmail.com` or `yahoo.com`.
2.  On each enrichment column that uses email as an input, open **Run settings → Only run if** and set a condition referencing the formula column: `/Is Personal Email == false`. Clay runs the enrichment only for rows where the formula confirmed the address is not personal.

Rows where the formula flags the address as personal show **"Run condition not met"** — no credits are consumed for those rows.

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

### Use "is empty" and "is not empty" to check for blank fields

When checking whether a field has a value — in a run condition or a formula column — **always use `is empty` or `is not empty`**. These are the correct Clay operators for blank-field checks.

**"exist" and "does not exist" are not valid operators in Clay.** Writing `/Column does not exist` or `/Column exist` will not behave as expected; the condition may silently fail or never match.

**Correct**:

- `/Email is not empty` — condition passes when the Email column has a value
- `/Domain is empty` — condition passes when the Domain column is blank

**You may also see `!{{column}}` syntax in existing run conditions.** The single `!` (negation operator) returns `true` when the column is empty or blank, and `false` when it has a value — making it equivalent to `/column is empty`. For example, a run condition of `!{{Email Address}}` means "only run when Email Address is blank." On rows where Email Address already contains data, the condition evaluates to `false` and the cell shows **"Run condition not met"** — this is expected behavior, not an error. To understand why a specific row was skipped, click the cell and use the **Explain** button in the cell details panel. To change the run condition, click the column header → **Edit column** → scroll to **Run settings** → update the **Only run if** formula → click **Save**.

### Avoid combining `!!` with equality checks on 0 or other falsy values

The `!!` prefix coerces a value to boolean: `!!value` returns `true` for truthy values and `false` for falsy ones. Falsy values include `0`, `""` (empty string), `null`, and `false`.

This means a condition like `!!{{DNC}} && {{DNC}} == 0` is **always false** and will never trigger the enrichment — because:

- When `{{DNC}}` is `0`, `!!0` evaluates to `false`, which immediately short-circuits the entire `&&` chain.
- When `{{DNC}}` is any non-zero value, `{{DNC}} == 0` is `false`.

No value of `{{DNC}}` can satisfy both clauses simultaneously.

**Use `!!` only to check "this column has a non-empty value":**

| Purpose | Correct formula |
|---|---|
| Column is not empty | `!!{{Email}}` |
| Numeric column equals zero | `{{DNC}} == 0` |
| Column is not empty AND another column equals zero | `!!{{Email}} && {{DNC}} == 0` |

**Never write** `!!{{Column}} && {{Column}} == 0` — that is a self-contradicting condition and will always evaluate to false.

If your condition was generated by the formula AI and shows "Run condition not met" even when the values look correct, open the condition editor and check for this pattern. Remove any `!!{{Column}}` clause that is also used in an equality check for `0` in the same condition.

### Formula preview may not match runtime results

The preview in the run condition editor is built from the column values loaded when you opened the panel — it does not refresh automatically as your table runs. If upstream columns have run or changed since you opened the editor, the preview can show stale or incomplete results.

For formulas that reference many columns, or that depend on complex values like waterfall outputs or nested lists, the preview may also resolve references differently than the actual runtime evaluation does.

**If the preview looks wrong, don't assume your formula is broken.** Save the condition, run a few test rows, and check the table for the **"Run condition not met"** status on the cells you expect to be skipped. The actual run results are the authoritative source — the preview is a best-effort guide, not a guarantee.

### Only matching rows consume credits

When a run condition is set, Clay only processes rows where the condition evaluates to **true**. Rows where the condition is not met are skipped and shown as **"Run condition not met"** — no credits are consumed for those rows.

This means clicking **"Run all rows"** with a condition in place is safe: Clay will only run (and charge credits for) the rows that actually match your condition.

**The credit estimate shown before running is based on the full row count** — it does not account for how many rows your condition will skip. Treat it as a worst-case ceiling: if only a portion of your rows satisfy the condition, your actual credit spend will be proportionally lower.

### "Run condition not met" cells appear empty to downstream columns

When a run condition is not met, Clay skips the enrichment and stores **no output** for that row — the cell value is empty. Any downstream columns that reference this cell (formula columns, waterfall columns, CRM push columns, etc.) will receive an empty value for those rows.

**This is why downstream columns that depend on this data will show empty results for those rows.** The row itself still appears in any downstream column, but the value fed into it from the skipped enrichment is empty — so any formula, waterfall step, or output that requires this data will produce no result for that row.

**Note:** If a row previously ran and produced output, that output is preserved when the condition is not met on a subsequent run — the run condition only gates new executions and does not clear existing cell data.

### Using the "Explain" button to diagnose a skipped run condition

When a cell shows **"Run condition not met"**, an **Explain** button appears next to the status message in the cell details panel. Clicking it triggers an AI analysis of your run condition formula and the current row's values, then returns a plain-language explanation of exactly why the condition evaluated to false for that row.

**To use it:** Click the cell showing "Run condition not met," then click the **Explain** button in the status area. The explanation appears inline below the message.

This is particularly useful when the formula looks correct but the condition still isn't met — for example, when a value appears populated in the table but the comparison fails due to type mismatches, unexpected whitespace, or a nested formula that resolves differently at runtime than it previews.

### Running an action only once per row (new rows only)

Clay has no built-in "is new row" flag. To prevent an action column — such as sending a Slack message, writing to a CRM, or sending an email — from re-firing on rows it already processed, gate it on a **separate upstream column** that only has a value after the row was first processed:

`/My Upstream Column is not empty`

On new rows, the upstream column hasn't run yet, so the condition is false and the action waits. Once the upstream column runs and produces a value, the condition is true and the action fires.

**Important**: You cannot use a column's own previous output as its own run condition — Clay detects this as a circular dependency and will reject the configuration. The guard must be a different column.

**Simpler alternative for scheduled re-run tables**: If the root cause is that your action column is included in a scheduled re-run, the easiest fix is to uncheck it from the scheduled re-run list (Table Settings → Run Settings → Re-run columns on a schedule). Table-level Auto-run still fires the column for genuinely new rows. See [Scheduled columns](scheduled-columns.md).

### Running a downstream action only after all upstream columns have finished

Clay columns execute based on a dependency graph — each column fires as soon as its own declared inputs are ready — not in a strict left-to-right sequence. A column with no declared dependency on a sibling column will not wait for that sibling to finish. This means a downstream action column (such as one that sends data to a CRM or webhook) can run before sibling enrichment columns finish, even if those columns appear to the left of it in the table.

**Note:** Dragging a column to a different position in the table view changes its display order only — it does not change execution order. Execution order is determined exclusively by column references (dependencies), not by visual position.

To prevent a downstream action from running before all required upstream enrichments are complete, use one of these approaches:

**Option 1 — Multi-column condition in "Only run if"**

In the action column's **Run settings → Only run if**, require every upstream column to have a value:

`/Column A is not empty AND /Column B is not empty AND /Column C is not empty`

The action fires only once all referenced columns have results for that row. Replace `/Column A`, `/Column B`, `/Column C` with the actual column names in your table.

**Important for CRM object lookups (HubSpot, Salesforce)**: When a Lookup Record column is still processing, its output fields are temporarily empty. A run condition that checks a *separate downstream column* populated by the lookup (for example, `{{HubSpot Contact ID}} is empty`) will not wait for the lookup to finish — Clay only registers a dependency on columns that are directly referenced in the run condition formula.

To ensure the run condition evaluates only after the lookup has completed, reference the **lookup column's result object directly** using dot-notation:

`{{My HubSpot Lookup}}?.id is not empty`

When the run condition formula contains `{{My HubSpot Lookup}}`, Clay registers that lookup column as an upstream dependency and delays evaluation until the lookup finishes. A reference to a separate column that the lookup populates (rather than the lookup column itself) does not create this dependency.

**Option 2 — Guard formula column**

Create a dedicated **Formula column** (for example, named "All Done") that returns a non-empty value only when all required upstream columns have results:

`{{Column A}} && {{Column B}} && {{Column C}}`

This returns a truthy value only when all referenced columns are populated. Then set the action column's **Only run if** condition to:

`/All Done is not empty`

This keeps the run condition simple and is easier to maintain when checking many columns.

**Note:** With Auto-run enabled, the "Only run if" condition is re-evaluated each time an upstream value changes for that row. The action fires as soon as the condition first becomes true — meaning as soon as all referenced columns are non-empty. If you need to gate on columns that are not otherwise in the action column's dependency chain, include them explicitly in your guard condition or formula.

**Option 3 — Disable Auto-run and run the action manually**

Turn off Auto-run on the action column (Edit column → Run settings → toggle Auto-run off). Once all other enrichments have finished, manually trigger the column: right-click its column header → **Run column** → **Run all rows**. This gives you complete control over when the action fires and is the simplest option when your workflow does not need to run automatically.

### "Circular dependency error" when setting a run condition

When you save a run condition, Clay validates that the column referenced in the condition does not depend — directly or through a chain of other columns — on the column being gated. If a cycle is detected, Clay shows a **"Circular dependency error"** modal and prevents saving. The modal lists the specific column(s) that complete the loop.

**This check covers indirect chains, not just direct self-reference.** Even if the condition column doesn't visibly reference the gated column, the error can still occur if the condition column's value is derived from other columns that themselves depend on the gated column's output.

**Example**: You want Work Email to run only when a Status field is not "customer". But Status is written by a matching step that reads from Apollo Contact, which depends on Work Email. The full dependency chain is:

`Work Email → Apollo Contact → Match Records → Status`

Setting a run condition on Work Email based on Status creates the loop:

`Work Email → Status → Work Email`

Clay blocks this and lists Status (or the intermediate column completing the cycle) in the error modal.

**How to diagnose**: Starting from the column referenced in your run condition, trace each of its inputs one step at a time. Work backwards through the dependency chain until you either reach raw source columns (import data or columns not derived from any enrichment) or encounter the column you're trying to gate.

**How to fix**: Find the step in the dependency chain that uses the gated column as an input, and replace that input with an equivalent identifier that comes from your import source — one that exists before the gated enrichment runs. Common substitutes: Company Domain, Company Name, professional profile URL, First Name, Last Name.

Alternatively, restructure so the condition-determining step happens fully upstream using only pre-enrichment data as inputs, with no dependency on the gated column.

**If the error appears but the column you are configuring does not visibly depend on the gated column**: The circular dependency check traverses the full column graph of your entire table at save time. If another column in the table has accumulated stale dependency information — for example, from a prior column deletion or recreation — the traversal can flag an apparent cycle in those other columns and block your save, even though your run condition itself is not the source of the cycle. In this case, the error modal may not name any specific column completing the loop.

**How to fix a false positive caused by stale column dependencies**:

1. Look for other columns in the table that reference a column which has been deleted or recreated. Formula columns and prompt columns are the most common source of stale references.
2. Open **Edit Column** on each suspect column. If the formula or prompt references a column name that no longer exists, replace that reference with the correct current column name.
3. Save those columns — re-saving recompiles the formula into an up-to-date dependency record, clearing the stale cycle.
4. Return to your original column and try saving the run condition again.

### "Only run if" re-evaluates each time an upstream column changes

With **Auto-run** enabled, Clay re-evaluates an action column's "Only run if" condition each time a value in the current row changes — including each time an upstream enrichment column finishes running. The condition is **not a one-time gate**: if it evaluates to `true` on multiple occasions as different enrichments complete, the action column can run multiple times on the same row.

**Consequence for webhook and HTTP API export columns**: If you gate a webhook on upstream enrichments being done, it can fire more than once per row. To ensure the action fires only once, use the guard-column pattern described in [Running a downstream action only after all upstream columns have finished](#running-a-downstream-action-only-after-all-upstream-columns-have-finished): gate the action on a formula column or multi-column condition that only becomes true once all required upstream work is finished.

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

### If "Run empty or out-of-date rows" appears to do nothing

If clicking **"Run [N] empty or out-of-date rows"** from the column header appears to do nothing — no Confirm Run panel, no spinner, no progress — but opening an individual blank cell and clicking **"Re-run this cell"** works on those same rows, use **Force run all [N] rows** from the column dropdown instead:

1. Right-click the column header to open the column menu.
2. Select **Run column** → **Force run all [N] rows**.

This queues every row in the column regardless of its current state — the same mode used by the individual **"Re-run this cell"** button in the cell details panel.

**Note:** Force run will re-run rows that already have results, not just blank ones. Review the estimated credit cost before confirming.

### Running a column can re-trigger dependent downstream columns

When you run an enrichment column that other enrichment columns depend on, Clay shows a **Confirm Run** panel before starting. This panel lists any dependent downstream columns that may automatically re-run and their estimated credit cost. If you confirm, those downstream columns are marked as out-of-date and queued to re-run — their stored values persist until they actually execute, at which point new results replace them.

Before confirming a run on an upstream column, check whether any listed downstream columns contain data you want to keep. If so:

-   Temporarily disable **Auto-run** on the downstream columns before running the upstream column.
-   Or choose **Save and don't run** when saving the upstream column's settings, so no rows are immediately queued and you can run columns individually in a controlled order.

If the Confirm Run panel does not appear when you run a column, that column has no downstream action columns configured to run automatically — running it will not affect other columns.

See [Credit usage](credit-usage.md) for more detail on the run cost breakdown displayed in this panel.

## See also

[Conditional statements](https://www.clay.com/university/guide/conditional-statements)

[Comparison operators](https://www.clay.com/university/guide/comparison-operators)

[Logical operators](https://www.clay.com/university/guide/logical-operators)
