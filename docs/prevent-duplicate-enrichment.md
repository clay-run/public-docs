---
title: Prevent duplicate records from being enriched
description: Use a lookup and a ranking formula so only one of several duplicate rows runs enrichment.
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
