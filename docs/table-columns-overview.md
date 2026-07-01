---
title: Table columns
description: Learn how to navigate columns in your Clay table, including column types, system columns (Created At and Updated At), limits, child column mapping, and how to resolve circular dependency errors.
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

## System columns: Created At and Updated At

Every Clay table includes two automatically maintained system columns: **Created At** and **Updated At**. These columns are hidden by default — to show them, open the columns panel (click the column count button in the toolbar) and toggle them on.

-   **Created At**: Records when a row was first added to the table.
-   **Updated At**: Records the most recent time any cell in the row changed. Clay automatically stamps a new value here whenever any column in the row is modified.

Both fields are system-managed: you cannot delete them, edit their settings, or manually change their values.

### Integration mapping limitation

**Updated At** and **Created At** are not available in the column picker when mapping Clay columns to an external integration — this applies to all integrations, including Google Sheets, Salesforce, and others. The mapping UI removes them from the selectable field list.

This is by design. Because Clay automatically overwrites **Updated At** on every record change, using it as an outbound mapping target creates an infinite loop risk: any column change updates **Updated At**, which re-triggers the outbound sync, which modifies more columns, which changes **Updated At** again — and the cycle repeats. See [Infinite loops](infinite-loops.md) for how to recognize and stop loop patterns.

If you need to push a timestamp to an external platform that reflects when a record was processed, create a separate column to hold that value — for example, a formula column or a manually set date column — and map that column to your destination instead.

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
3.  Under **Map to an existing column**, click on the column you want to map this enrichment endpoint to. What happens depends on the destination column's current state:
    -   **If the destination column has no formula** (for example, values you entered manually or imported from a CSV), Clay replaces the column with a formula referencing the new source column. Clay shows a **"Data overwrite"** warning before proceeding. If you confirm, that column will be blank for any rows where the new source column is empty — including rows from a different source in a multi-source table. **This cannot be undone.**
    -   **If the destination column already has a formula**, Clay automatically applies a waterfall pattern — the new source column is appended as a fallback, so existing data is preserved.

**To keep manually entered or CSV-imported data while also bringing in new enrichment data:** Instead of mapping to the existing column, use **Create new column** to extract the incoming field into a separate column. Then add a [Merge column](#merge-columns) that references both the original column and the new one — it returns the first non-empty value per row, preserving whichever source has data.

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

## Sort columns

You can sort your table by any column to arrange rows in ascending (A → Z / 0 → 9) or descending (Z → A / 9 → 0) order. Sorts are view-specific — each view of a table can have its own independent sort configuration.

### Sort by a single column

Click a column header to open its dropdown menu and select **Sort A → Z** or **Sort Z → A**. The table immediately reorders all rows by that column's values.

### Sort by multiple columns

When you apply more than one sort, Clay applies them **in priority order**: the first (top) sort arranges all rows, and each additional sort only reorders rows that have the **same value** for every higher-priority sort column. This is the same behavior as an `ORDER BY col1, col2, col3` clause in a database.

**Example:** If your view has three sorts active —

1.  Competitor Status (Z → A) — highest priority
2.  Hiring Sales (Z → A)
3.  Has RevOps (A → Z) — lowest priority

— then all rows are arranged by Competitor Status first. Within any group of rows that share the same Competitor Status value, those rows are further sorted by Hiring Sales. Within rows that share both the same Competitor Status and Hiring Sales value, Has RevOps then determines the order.

**This is expected behavior, not a bug.** If a column's sort appears to have no effect, it means the higher-priority sort columns have unique values for every row — there are no ties to break.

To manage multiple sorts:

1.  Click the **Sort** button in the table toolbar (it shows the number of active sorts when any are applied, e.g., **2 sorts**).
2.  Click **Add sort** to add another column and direction.
3.  **Drag** sort items up or down to change their priority — the topmost item always has the highest priority.
4.  Click the **×** on a sort item to remove it.

## Filter rows

You can filter your table to show only rows that match specific criteria. Filters are view-specific — each view of a table can have its own independent filter configuration.

**Filters are display-only.** They control which rows appear in the current view; they do not delete, move, or modify any rows. Every row remains in your table regardless of the active filter — rows that don't match are hidden from the view but are still stored.

### Apply a filter

1.  Click the **Filter** button in the table toolbar.
2.  Click **Add filter** and select a column to filter by.
3.  Choose a comparison operator (e.g., **is**, **contains**, **is not empty**) and enter a value.
4.  To add more conditions, click **Add filter** again. Multiple filters are applied together — a row must match all active filters to appear.
5.  To remove a single filter, click the **×** next to it. To remove all filters, click **Clear filters**.

### Check whether a filter is active

When a filter is active, the **Filter** button in the toolbar shows a number badge, and the row count displays as **X / Y rows** — X is the number of rows passing the filter, Y is the total. If Y is higher than X, some rows are being hidden by the active filter.

### Filters and source row limits

A source's row limit controls how many records Clay fetches from the external system **before** any view filter is applied. If your source fetches 10 rows and all 10 happen to be filtered out by your view filter, the table shows 0 / 10 rows — Clay does not automatically fetch more rows to compensate for filtered-out ones. To see more matching rows in this situation, increase the source limit so Clay retrieves a larger pool of records.

### Source filter changes and existing rows

Changing a source's import filter (the filter configured in the source setup) does **not** retroactively remove rows already in your table — those rows remain as-is, and only future source runs apply the updated criteria. See [Sources](sources.md#will-rows-already-in-my-table-be-removed-if-they-no-longer-match-the-source-filter) for full details.

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

### Troubleshooting merge columns

**The merge column stays empty even though upstream columns have data.** The most common cause is stale upstream columns. A Merge column returns the first non-empty value from the columns in its formula, but only reflects current data. If an upstream column shows the out-of-date indicator (the clock icon), re-run it first: click the column header and select **Run column → Run [N] empty or out-of-date rows**. Once the upstream column refreshes, the merge column will pick up the new value.

**The merge column doesn't update after new upstream data arrives.** If auto-run is disabled at the table level, downstream columns — including Merge columns — won't update automatically when upstream data changes. To re-enable: click the `⛭` icon in the top toolbar → toggle **Auto-run** on, then choose **Update cells** to immediately process rows that are out of date. See [Table management settings](table-management-settings.md#auto-run) for details on table-level and column-level auto-run.

**The merge column is only partially populated.** If some rows have a value but others don't, check that all upstream columns have finished running. A Merge column that depends on an incomplete enrichment or waterfall column stays empty on those rows until the upstream column produces a result.

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

### Rename color labels

You can give custom names to the color categories used in your table. For example, you might rename "Green" to "Approved" or "Red" to "Needs review." Custom labels apply to the whole table — they appear consistently across all views of that table.

To rename color labels:

1.  Click on a column header to open the dropdown menu.
2.  Select `Change color`.
3.  Click `Rename colors` at the bottom of the color picker.
4.  Enter a custom name for each color you want to rename.
5.  Click `Save changes`.

Colors with no custom name default to their original label (Red, Orange, Yellow, etc.). The Default (grey) color cannot be renamed.

### Best practices

Use colored columns to keep your tables organized:

-   **Group related columns** by using the same color for columns that belong to the same workflow step or data category (e.g., all email-related columns in blue).
-   **Highlight important columns** with distinct colors to draw attention to key columns you reference frequently.
-   **Mark column status** by using colors to indicate states (e.g., green for complete, yellow for needs work, red for experimental).
-   **Separate workflow stages** by using different colors to visually distinguish between stages of your data pipeline (e.g., sourcing, enrichment, validation, outreach).
