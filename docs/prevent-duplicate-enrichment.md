---
title: Prevent duplicate records from being enriched
description: Use a lookup and a ranking formula so only one of several duplicate rows runs enrichment, with a dedicated workflow for Salesforce parent/child account hierarchies.
---

# Prevent duplicate records from being enriched

When the same value shows up in more than one row, this setup lets only **one** of those rows run enrichment—so you don't spend credits enriching the same record twice.

## How it works

Each duplicate value gets numbered by the order it appears in the table (`1, 2, 3…`), and you gate enrichment so it fires only on `1`. The rest are recognized as copies and skipped.

```
Unique ID column → Lookup rows in same table → Formula ranks each match → Run only where rank = 1
```

## The setup

The recipe uses four columns.

### 1. Create the Unique ID column

Add a **formula column** that assigns each row a random unique number. Use a prompt like:

> Return a random 10-digit number if `/[Column Name]` is not empty

Replace `/[Column Name]` with the column that holds the value you're deduplicating on (for example, your Company ID column). The formula generates a different random number for each row — that per-row uniqueness is what lets Step 3 locate exactly this row in the lookup results.

**Do not re-run this column after the initial run.** Formula columns regenerate values on every run. Re-running replaces every row's number with a new random value, which breaks the ranking formula in Step 3. Run the column once when it's set up, then leave it.

Give the column a clean, memorable name—you'll type that exact name into the prompt in Step 3.

### 2. Add "Lookup Multiple Rows in Other Table"

Add the **Lookup Multiple Rows in Other Table** integration and point it back at **the same table you're working in**. Have it search the column that holds the value you're de-duplicating, so it surfaces every row that shares that value.

| Field | Value |
| --- | --- |
| **Table to Search** | This same table (the one you're in) |
| **Target Column** | The column being de-duplicated (e.g. `Name`) |
| **Filter Operator** | `Contains` |
| **Row Value** | This row's value from that column |

This returns a `records` array—every row in the table whose value matches the current row.

> If you only need a single match, the "Lookup Single Row in Other Table" action is faster. For de-duplication you need every match, so use the multiple-rows action.

### 3. Add a formula column to rank each match

Add another **formula column** and describe the formula with the prompt below. It walks the array from the lookup and returns the *position* of this row among the matches—1 for the first occurrence, 2 for the second, and so on.

**Prompt:**

> Only run if `/Unique ID` is not empty, then return a number label depending on which number of occurrences any of the "Unique ID" fields from the following array `/Lookup → records` match `/Unique ID`
>
> For example, if the first value of "Unique ID" you find from the array is true, then return 1, if it's the second value then return 2 and so on
>
> Otherwise return 2

**Inserting the lookup value:** Where the prompt references the array, insert the lookup output and choose the **"( Insert all items )"** option that appears *beneath the `records` field*—not a single sub-item. This passes the whole set of matched records into the formula.

```
Lookup Multiple Rows in Other Table → records → ( Insert all items )
```

> **Name it exactly.** The column name must be spelled identically to what you tell the prompt to look for. For example, column `Unique ID` → prompt searches for "Unique ID"; column `Unique Number` → prompt searches for "Unique Number".

### 4. Gate enrichment on rank = 1

The formula now returns a row-position number for every identical value in the table. Use that output as a [conditional run](conditional-runs.md) on your enrichment column: run only when the rank equals `1`.

The first occurrence of each value enriches; every later copy is skipped—one record enriched per unique value.

## What you'll see

For three rows sharing the same value, the ranking formula returns:

| Value | Rank | Result |
| --- | --- | --- |
| `acme.com` | 1 | Enriches |
| `acme.com` | 2 | Skipped |
| `acme.com` | 3 | Skipped |

Only the first row clears the `rank = 1` condition, so the duplicates never consume enrichment credits.

## Cleaning up duplicate rows after enrichment

After enrichment runs, you can delete the duplicate rows so only one row per unique value remains. Click the header of the column you're deduplicating on and select **Dedupe** from the dropdown. Clay shows each group of duplicate values and lets you confirm which to remove — it keeps the first row in each group and deletes the rest.

**Note:** Dedupe is available on Text, Email, and URL columns only. Export your table to CSV before running Dedupe — there is no built-in undo for row deletions. For full details and recovery options, see [Dedupe columns](table-columns-overview.md#dedupe-columns).

## Handling Salesforce parent/child account hierarchies

When you import a Salesforce list that contains both parent accounts and child accounts that roll up to the same parent, you end up with multiple rows representing the same underlying company. Because rows in Clay process independently — each row has no awareness of any other row in the table — each duplicate runs every enrichment column on its own. This is why AI enrichments like Claygent can return different Account Scores or Account Briefs for two rows that represent the same company.

The recommended approach is to enrich only the parent account and then propagate those results to the child rows.

### Step 1: Build a normalized parent identifier

Avoid using Company Name as your deduplication key — names are inconsistent across records ("Acme" vs "Acme Corp" vs "Acme, Inc."). Instead, use a Salesforce ID or normalized domain as the key, since these are stable and match exactly.

Add a **formula column** that extracts or normalizes the parent account identifier. For example, if your table has an **Ultimate Parent Account ID** column from Salesforce, create a formula column that pulls that value into a clean text field. This becomes your dedup key.

### Step 2: Enable Auto-dedupe on the parent identifier

Auto-dedupe removes duplicate rows whenever two rows share the same value in a specified column. It performs exact-match comparison, which is why normalizing the key in Step 1 matters.

1. Click the gear (⚙) icon at the bottom right of the table to open Table Settings.
2. Find the **Deduplication** section and toggle **Auto-dedupe rows** on.
3. Under **Dedupe via column**, select the normalized parent identifier column from Step 1.
4. Choose **Keep oldest row** or **Keep newest row** depending on which version of a duplicate record you want to retain.
5. Click **Save changes**.

When Auto-dedupe is enabled, Clay immediately checks all existing rows and removes any that share the same parent identifier. Going forward, new imports that add a row with a matching identifier are automatically deduplicated as they arrive.

For full Auto-dedupe configuration details, including column type requirements and the deduplication history panel, see [Table management settings](table-management-settings.md#auto-dedupe).

### Step 3: Add run conditions to gate enrichments on parent accounts only

Expensive enrichments — AI research columns, job opening searches, or any Claygent workflow — should run only for parent account rows, not for every child that survived deduplication.

For each enrichment column you want to restrict to parent accounts:

1. Open the column's **Run Settings → Only run if**.
2. Set a condition that evaluates to true only for parent rows — for example, if you have an **Is Parent Account** field from Salesforce, use `/Is Parent Account equals true`. Or, if your parent identifier column is only populated for parent rows, use `/Parent Identifier is not empty`.
3. Child account rows that don't meet the condition show **"Run condition not met"** and consume no credits.

For a complete guide to conditional run syntax and operators, see [Conditional runs](conditional-runs.md).

### Step 4: Turn off "Update existing rows" in the Salesforce source

If your Salesforce table source runs on a schedule, the **Update existing rows** toggle controls whether re-imports update records that already exist in the table. When turned off (the default for most source types), scheduled re-runs only add net-new records — existing rows are not re-evaluated or re-enriched.

Turn this off if your goal is to enrich each account only once, rather than re-processing every scheduled import.

1. Click the Salesforce source column header → **Edit column**.
2. Toggle **Update existing rows** off.
3. Save.

For a full explanation of how this toggle interacts with the auto-run enrichment pipeline, see [Auto-run](auto-run.md#update-existing-rows-toggle-for-scheduled-source-imports).

### Step 5: Use Clay Lookup to propagate parent results to child rows

After parent accounts are enriched, child rows still need access to those results. Use a **Lookup single row in other table** column (pointed at the same table) to pull the parent's enrichment values into each child row.

1. Add a **Lookup single row in other table** column.
2. Set **Table to search** to this same table.
3. Set **Target column** to the normalized parent identifier column.
4. Set **Row value** to the current row's parent identifier column.
5. Run the lookup.

For each child row, the lookup returns the matching parent row. From there, click **Add as column** on any enrichment field you want to surface (Account Score, Account Brief, etc.) — the child row now shows the parent's enriched values without running those enrichments a second time.

**Cost:** Lookup Rows does not consume Actions or Data Credits. See [Lookup Rows](lookup-rows.md) for full configuration details.
