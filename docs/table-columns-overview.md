---
title: Table columns
description: Learn how to navigate columns in your Clay table, including column types, limits, child column mapping, and how to resolve circular dependency errors.
last_synced: 2026-04-26T01:40:46.052Z
---

# Table columns

Learn how to navigate columns in your Clay table.

## Column data types

There are a data types you can specify for your column. Here's a high level overview of each one:

-   **Text:** Accepts text inputs. You can use this for text fields, summaries, or descriptions
-   **URL:** Takes in links and will open the link if you click on the cell.
-   **Checkbox:** A true/false field that displays a checkbox. Ideal for conditional runs.
-   **Select:** Select from a list of predefined tags. This is useful for categorizing your contacts and companies.
    -   You can also split into views: create a view for each Select option with one click to slice your table by things like Account Tier or Segment.
-   **Multi-select:** Select multiple options from a list of predefined tags. Similar to Select, but allows choosing more than one tag per cell.
-   **Number:** Allows numerical values to be entered, ideal for ISO time measurements, lead scores, or revenue measurements.
-   **Date:** Accepts a date and time range.
-   **Currency:** Express your values in currency amounts.
-   **Assigned To:** Tag anyone in your Clay workspace.
-   **Email:** Accepts any email address input.
-   **Image from URL:** Upload image URLs for easy retrieval.

## Add columns

You can add a new column to your table in a few ways:

-   Scroll to the right of your table and select `Add column`.
-   Open the dropdown menu for an existing column and choose `Insert right` or `Insert left` to access the column creation dropdown.
-   In the column creation dropdown, you can either:
    -   Specify the **data type** for your new column (e.g., Text, Number, Date).
    -   Perform advanced actions, such as:
        -   **Use AI** for AI data processing or research
        -   Select **Message drafting**, **Enrichment waterfall**, or **Formula** for specific calculations or actions.
        -   **Merge columns** to combine data from multiple columns.

### Switching column data type

You can switch the data type of your column within your table. To do this:

1.  Click on the column title.
2.  Hover over the current data type to see the dropdown of other options.
3.  Select your new input type.

## Column input types

There are two types of input formats available for columns:

-   Text with tokens
-   Formulas

By default, columns are set to the **Text with tokens** input format.

### Switching column input types

You can switch the data type of your column within your table. To do this:

1.  Click on the header of the column you want to edit to access the dropdown menu.
2.  Select `Edit column` from the dropdown.
3.  Click on the gear icon and select your new input type.
4.  Press `Save settings` to save your changes.

## Column limits

-   Clay tables have a default column limit of **100** (all column types combined).
-   Clay tables have a default enrichment column limit of **40**. This is a separate, independent cap — your table's enrichment column count is tracked on its own, regardless of how high the total column limit is.
-   Tables using phone or email waterfalls can have this limit raised to a maximum of **60** (for that table only).
-   Note: Enterprise Plans may have custom column limits. Each limit (total and enrichment) is set independently — a custom total column limit does not automatically raise the enrichment column limit.

### "Cannot create new computable field due to table size limit"

If you see the error **"Table cannot create new computable field due to table size limit"** — whether you're adding a new enrichment column, connecting a new data source, or saving a workflow as a Function ("Replace columns with function") — your table has reached the **40 enrichment column limit**. Despite the phrase "table size," this error is about column count — not row count or data volume. It can appear even on a table that has very few or no rows.

If your table's enrichment limit was previously raised (for example, to 60 for a phone or email waterfall table) and you hit that higher cap, the in-product error instead reads **"This table has reached the [N] enrichment columns limit"** — where [N] is your table's current limit. The cause and resolutions are identical.

Enrichment (action) columns include any column that runs an integration, waterfall, AI enrichment, lookup, or other data action. Your table can hold up to 40 of these before new ones are blocked. This cap is enforced independently from your workspace's total column limit — even if your workspace has a custom total column limit (such as 99 instead of the default 100), the enrichment column limit remains at 40 unless it was separately raised.

**To resolve this:**

-   **Delete unused enrichment columns.** Click the column header dropdown → `Delete column` for any enrichment columns you no longer need. Hidden enrichment columns still count toward the limit, so open the columns panel to check for any hidden ones.
-   **Consolidate with Functions.** [Functions](https://university.clay.com/docs/functions) run multiple enrichment steps in a background mini-table and return a single column to your main table — collapsing 20–50 enrichment columns into one. This is the most effective way to stay within the limit while keeping your workflows intact.
-   **Request a higher limit.** Tables using email or phone waterfalls can have the enrichment column limit raised to 60. Contact support if you need a higher limit for your use case.

## Create child columns from a parent column

When you enrich data within Clay, your results will be presented as arrays of data, which sometimes includes nested endpoints. You can create individual child columns by mapping specific endpoints from the parent column's enrichment.

### Add a new child column

To create a new column with an endpoint from an enrichment (parent column):

1.  Click on the cell of the enrichment containing the endpoint you want to use. This will open the **Cell details** panel on the right.
2.  Hover over the endpoint you want to map out and to the right click `Add as column`.
3.  In the **Add description as new column** section, enter your column description and click `Create column` to generate a new column.

### Map child columns to an existing column

To map an endpoint from an enrichment to an existing column:

1.  Click on the cell of the enrichment containing the endpoint you want to use. This will open the **Cell details** panel on the right.
2.  Hover over the desired endpoint and click `Add as column` on the right.
3.  Under **Map to an existing column**, click on the column you want to map this enrichment endpoint to.

**Warning:** Mapping to a column that already contains data — including values from CSV imports or manual entry — will permanently erase those values. Clay replaces the destination column's formula with one that references your integration source. For any row where that source has no data (such as rows you imported from a CSV or typed in manually), the formula evaluates to empty and overwrites whatever was in that cell. Clay shows a confirmation dialog when the destination column contains manually entered data, but the overwrite cannot be undone once confirmed.

If your table has rows from mixed sources, map to a **new** column instead, then combine the integration data and your manual data using a [Merge column](#merge-columns).

### Circular dependency error

If Clay blocks the save with a **Circular dependency error**, it means the destination column is already used as an input somewhere upstream in the same enrichment chain — directly or indirectly through another dependent column. Mapping into it would create a loop, so Clay prevents the save.

**How to fix it:**

-   Map the enrichment result to a **new column** instead of the existing destination.
-   Or, open the enrichment(s) that reference the destination column as an input and remove that reference, then re-map.

To visualize the full dependency chain and identify where the loop originates, open **Graph view**: click the view selector dropdown in your table toolbar and choose **Graph view**.

### Find the parent column of your child column

You can identify the parent column of a child column to better understand its data context. Follow these steps:

1.  Click on the child column to open the dropdown menu.
2.  Within the menu, select `Go to parent column`.

## Hiding columns

You can hide a column to help simplify your table view. This is helpful when you want to hide parent columns.

To hide a column:

1.  Click on the header of the column you want to hide to access the dropdown menu.
2.  Within the menu, select `Hide`.

**Important:** Hiding a column only removes it from the current view — it does **not** disable the column's auto-run setting. A hidden column with auto-run enabled will still run automatically and consume credits whenever rows are added or edited. To stop a column from running, open it in `Edit column` → `Run settings` and toggle auto-run off. To access a hidden column's settings, temporarily unhide it using the columns panel, or switch to a view where it is visible.

### Unhide a column

When a column is hidden, it disappears from the table entirely — there is no header to click on. To bring it back, use the columns panel:

1.  Click the **columns button** in the table toolbar (shown as "N/N columns", for example **12/38 columns**).
2.  In the panel that opens, find the column you want to restore. Hidden columns display a closed-eye icon next to their name.
3.  Click the eye icon next to the column to make it visible again.

## Merge columns

You can merge data from multiple columns into a new column. "Merge columns" uses a **waterfall** pattern — it returns the **first non-empty value** from the columns in your formula. For example, if Column A is empty, Clay falls back to Column B, then Column C, and so on. This is ideal for coalescing a single value from multiple data providers (such as finding the best available LinkedIn URL across several enrichment sources).

1.  Click `Add column` → `Merge columns`.
2.  Select a `Data type` from the dropdown.
3.  In the formula field, type `/` to open the column picker and select each column you want to include as a fallback step.
4.  Click `Save settings`.

**Note:** There is no "List" column data type in Clay. A Merge column always returns a **single value** (the first non-empty result across your columns), not an array of all values.

If you need to collect **all values** from multiple columns into a list — for example, to gather LinkedIn URLs from five separate columns so you can send each URL as its own row to another table — use a formula column with array syntax instead:

1.  Add a new column and choose a data type (e.g., **Text**).
2.  Switch its input type to **Formula**: click the column header → **Edit column** → gear icon → select **Formula**.
3.  Write your array formula by wrapping column references in square brackets, separated by commas. Type `/` to insert each column reference. For example: `[{{LinkedIn URL 1}}, {{LinkedIn URL 2}}, {{LinkedIn URL 3}}]`
4.  Click **Save settings**. Each cell will now contain a list of all the included values.
5.  To send each list item as a separate row to another table: click a populated cell → **Cell details** → **Take action on list** → **Write each item to new row in other table**.

**Tip:** If you plan to use a merged column for deduplication, make sure all enrichment columns feeding it have run and are not stale. A stale upstream column causes the merged column itself to become stale, which causes auto-dedupe to skip it.

## Dedupe columns

You can dedupe your rows based on a specific column's values.

**Note:** Column deduplication removes duplicate **rows** from the table. If you want to deduplicate items within a list stored inside a single cell (for example, an array of domains), use the **Normalize and Deduplicate a List** enrichment instead — see [Clay formatters overview](https://university.clay.com/docs/clay-formatters-integration-overview) for details.

To dedupe a column:

1.  Click on the header of the column you want to dedupe to access the dropdown menu.
2.  Within the menu, select `Dedupe`.
3.  Confirm the duplicate values you want to remove and select `Delete`.

A few rules to keep in mind for column deduplication:

-   Deleted rows cannot be recovered, so proceed with caution.
-   Duplicates are identified based on exact string matches.
    -   Deduplication is case-sensitive, meaning `Clay` and `clay` are treated as different.
    -   Extra whitespace is considered, so `Clay (with a space)` and `Clay` are not the same.
-   **Auto-dedupe skips stale cells.** If a merged column — or any enrichment column it references — is stale, the row is excluded from auto-dedupe entirely and will not be flagged as a duplicate. Re-run all stale enrichment columns and confirm the merged column has refreshed before expecting auto-dedupe to catch those rows.
-   **Manual (one-time) column dedup skips blank cells only.** If the merged column has a previously stored value, that value is compared for duplicates even if the cell is stale. Only rows where the merged column is empty are excluded from manual dedup.

## Rename columns

You can rename your columns to make them easier to identify. To rename a column:

1.  Click on the column header you want to rename.
2.  Select the `Rename` option from the dropdown menu.
3.  Enter the new column name and press Enter to save it.

## Pin column

If your table has many columns, you can pin specific columns to keep them easily viewable. To pin a column:

1.  Click on the column header you want to pin.
2.  Select the `Pin` option from the dropdown menu.

## Color column headers

You can color column headers to visually organize your table and make important columns easier to identify. Column colors are view-specific, meaning different views of the same table can have different colored columns.

To color a single column header:

1.  Click on the column header to open the dropdown menu.
2.  Select `Change color` and choose your desired color.

To color multiple column headers at once:

1.  Select multiple column headers by holding `Shift` or `Cmd` (Mac) / `Ctrl` (Windows).
2.  Right-click on any selected column.
3.  Select `Change color` and choose your desired color.

### Best practices

Use colored columns to keep your tables organized:

-   **Group related columns** by using the same color for columns that belong to the same workflow step or data category (e.g., all email-related columns in blue).
-   **Highlight important columns** with distinct colors to draw attention to key columns you reference frequently.
-   **Mark column status** by using colors to indicate states (e.g., green for complete, yellow for needs work, red for experimental).
-   **Separate workflow stages** by using different colors to visually distinguish between stages of your data pipeline (e.g., sourcing, enrichment, validation, outreach).
