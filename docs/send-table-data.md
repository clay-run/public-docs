---
title: Send table data
source_url: https://university.clay.com/docs/send-table-data
description: Send data between tables to create simple multi-table setups.
last_synced: 2026-04-26T01:40:38.918Z
---

# Send table data

Send data between tables to create simple multi-table setups.

Send table data in Clay lets you route records between tables, making multi-table setups simple to manage and intuitive to use.

**Note:** Send Table Data replaces the deprecated [Write to Other Table](https://university.clay.com/docs/write-to-table-integration-overview) action. If you previously used Write to Other Table, use Send Table Data for all new multi-table workflows going forward.

### When to use Lookup Rows vs. Send Table Data

Both Lookup Rows and Send Table Data move information between tables, but they work in opposite directions and serve different purposes.

**Use Lookup Rows when...**

Lookup Rows **pulls** data from another table into your current table based on matching criteria. It's non-destructive and doesn't modify the source table.

-   You need to **enrich your current table** with data that already exists in another table
-   You want to **check if a record exists** in another table without modifying anything
-   You need to **count or aggregate** rows that share a trait (e.g., how many people work at each company)
-   You want to **reference** data from a central table (like a pricing list, messaging library, or Do Not Contact list)
-   You're working with **static reference data** that multiple tables need to access

[**Learn more about Lookup Rows →**](https://university.clay.com/docs/lookup-rows)

**Use Send Table Data when...**

Send Table Data **pushes** data from your current table into another table. It creates or updates rows in the destination table.

-   You need to **route or segment** your data into different tables based on logic or filters
-   You want to **flatten lists** into individual rows (e.g., turn a list of 5 people into 5 separate rows)
-   You need to **merge data** from several tables into one consolidated table
-   You want to **separate concerns** across multiple tables (e.g., companies in one table, people in another)
-   You're building **multi-stage workflows** where each table handles a specific step in your process

## Sending table data

To send data from one table to another:

1.  Open the **Exports** tab in the command center sidebar and select **Send table data**.
2.  Select the destination table.
3.  Choose the method:
    -   `Send row`: Choose which columns to send as a row to the other table.
    -   `Send row for each item in a list`
4.  Select data to send over.
5.  Click `Save`.

### Using `Send row`

`Send row` sends each row as-is to another table. Use it to filter or segment data, or to separate logic across multiple tables. It transfers specific columns, keeping your data aligned and reducing manual entry. Any extracted basic field can be sent to the destination table using the checklist selectors.

**Additionally you can:**

-   Send nested data from the parent table. (This is useful when you want to avoid extracting basic fields from an action column's output.)
-   Map any selected column to a specific existing column in the destination table. By default, each column routes to a destination column with the same name — hover over the row and click the **edit icon** to open a dropdown of all destination columns and choose a different target.

**Note:** When you first send a row, it creates a new row in the destination table. For subsequent sends, it updates that same row. This applies to both regular row data and nested data. You can turn this off to always create a new row via the \`Update existing rows on re-run\` setting.

### Using `Send row for each item in a list`

Each cell can hold a list of items — like a list of people found at a company, or a list of job postings returned by Find Active Job Openings. To turn each item in that list into its own row in another table, use `Send row for each item in a list`.

This is useful for **flattening lists**. For example, if you run Find Active Job Openings on a list of companies, each cell may contain multiple job postings — use this method to send each posting as its own row in a destination table, giving you a clean per-role breakdown you can filter and analyze. Similarly, if you find multiple people at a company, you can send each person as a separate row. **This method always creates a new row for each item.**

**Note:** This method sends a maximum of **20 items per row** per run. If the list has more than 20 items, only the first 20 will be sent—there is no setting to increase this limit. For workflows that need to process more than 20 items per row, use [Lookup Multiple Rows](https://university.clay.com/docs/lookup-rows) to query the destination table directly instead.

You can also select additional data to send along with the flattened list, just like with `Send row`.

**Tip: Use "Take action on list" to set this up automatically**

The easiest way to configure `Send row for each item in a list` is to use the **Take action on list** shortcut from the cell details panel:

1.  Click on a cell in the column whose list you want to flatten (for example, a "Find Active Job Openings" or "Find Contacts at Company" result cell).
2.  In the Cell details panel, hover over the list section (e.g., "People") to reveal the **Take action on list** button.
3.  Select **Write each item to new row in other table**.

This opens the Send Table Data configuration with the correct list field already pre-populated — so you don't need to manually identify which field to use as the list source.

**Selecting the right list field manually**

The list input shows a **"Type / to insert column"** placeholder when no column has been selected. Click in the field, type `/`, and pick the column that holds your array data (for example, `Job Openings` or `Contacts`). **If you save without selecting a column, the column will run but fail at runtime with `Invalid send table data inputs … "listData" … "Required"`** — meaning Clay has no list to iterate over.

When configuring the list field by hand, select the **list itself** (e.g., `People`), not an indexed element from within that list (e.g., `People.0`, which is just the first person). When you hover over an array-type column in the token picker, you'll see an **Insert all items** option — click it to insert the full list rather than a single indexed element. Selecting a single indexed element instead of the whole array is a common source of confusion: the configuration will show a **"Please add a valid list."** error because an indexed element isn't recognized as a list.

**If the column holds a stringified JSON array** — for example, a text value that looks like `[{"name": "Alice"}, {"name": "Bob"}]`, common when data arrives from an HTTP API call or webhook — Clay won't recognize it as a native list and will show the same **"Please add a valid list."** error. To fix this, click the **gear icon** on the right side of the list input to switch to formula mode, then enter `JSON.parse(/YourColumn)`, replacing `YourColumn` with the name of your column (use `/` to reference it). This converts the text string into a native array that Clay can iterate over.

If your table has no rows with data yet, Clay skips this validation and accepts the formula as-is. In that case, run a few rows first so the enrichment column has real output, then re-open the Send Table Data configuration to confirm the list field is valid before running the full table.

## Advanced settings

**Update existing rows on re-run**

When re-running, updates the matching row in the destination table instead of creating a new one.

**Auto-extract new columns**

Automatically creates new columns in the destination table for any that don't already exist.

**Auto-map existing columns**

Automatically maps incoming fields to existing destination columns that share the same name. For columns that already have a formula, the new source is appended to the existing formula. For columns without a formula (e.g., manually entered or CSV-imported data), a new extraction formula is set — **this will overwrite any existing values in those columns**.

## Mapping table data in the destination table

When you send data to a destination table, it appears in the leftmost column as **"rows from: \[source table name\]"**. The data is stored within this cell and needs to be extracted into individual columns to use it in your workflow.

**Tip:** `Auto-extract new columns` is **on by default** and automatically creates a new column for each sent field — but only for fields that don't already have a matching column in the destination table. If your destination table already has columns with plain-text (non-formula) data, those columns won't be updated automatically. Use **Add to column** below to map those fields manually, or enable `Auto-map existing columns` in the advanced settings.

To manually map data from the source column to columns in the destination table:

1.  Click into the source cell (the "rows from: \[source table name\]" cell).
2.  Hover over any field you want to extract.
3.  Click `Add to column`.
4.  Choose to either:
    -   **Create a new column**: Name the column and click `Create column`.
    -   **Map to an existing column**: Select an existing column from the dropdown.
        -   **If the column contains plain-text data** — for example, values imported from a CSV or entered manually — Clay shows a **"Data overwrite"** warning: *"Mapping to this destination column will overwrite all of its existing data. This action cannot be undone."* Confirming permanently replaces every value in that column with a formula driven by the incoming Send Table Data source. There is no merge option — only cancel or overwrite.
        -   **To keep existing data while also bringing in new data:** Instead of mapping to the existing column, use **Create a new column** to extract the incoming field into a separate column. Then add a [Merge column](https://university.clay.com/docs/table-columns-overview#merge-columns) that references both the original column and the new one — it returns the first non-empty value per row, preserving whichever source has data.
        -   If the existing column is already empty, the warning is safe to dismiss.

Repeat this process for each field you want to extract into its own column.

## Guide: Merging two tables with Send table data

## Best practices & troubleshooting

-   There can be a **maximum of 20 tables** in the workspace-wide routing graph. **This includes tables across workbooks.** The limit is a safety check on how many tables Clay traverses through the inter-table routing graph during validation — not the number of Send Table Data columns. If you exceed this limit, you'll see the error: *"Maximum number of table ID checks exceeded (limit: 20)"*. To work within this limit:
    -   **Lookup Single Row / Lookup Multiple Rows do not count toward this limit.** If you're using Send Table Data primarily to check whether a record exists in another table (for example, a "Do Not Contact" or "Recently Contacted" list), replace those with Lookup Rows — they return the same match result without consuming a slot in the traversal. See [Lookup Rows](https://university.clay.com/docs/lookup-rows) for setup instructions.
    -   If multiple workbooks all write to the **same destination table**, that table generally counts as only **one** connection regardless of how many workbooks or columns point to it. Centralizing writes into a small number of shared destination tables can significantly reduce your connection count.
    -   This limit applies across all plans.
-   **Data can only be sent in a linear direction** (A → B → C). In other words, loops are not possible (A → B → C → A).
    -   If you want to receive data in the table you're also sending data from, use one of these other actions:
        -   `Lookup Multiple Rows in Other Table`
        -   `Lookup Single Row in Other Table`
-   **"✅ Sent" means Clay dispatched the data — not that individual columns in the destination table have been populated.** The `Sent At` timestamp and `Number Of Rows Sent` confirm that Clay placed those rows into the **"rows from: [source table]"** column in the destination table. For fields that don't yet have a matching column, `Auto-extract new columns` (on by default) creates them automatically. However, if the destination table already has columns with plain-text data — for example, rows filled in manually or imported from a CSV — those existing columns won't be updated automatically. In that case, open the destination table, click the source cell, and use **Add to column** to map each field. See [Mapping table data in the destination table](#mapping-table-data-in-the-destination-table) above.
-   **Some cells show "Run condition not met" while others appear blank — what's the difference?** "Run condition not met" means the row's run condition evaluated to false and the action was deliberately skipped — no credits are consumed for those rows (any reserved credits are automatically refunded). Blank or out-of-date cells (shown with a clock icon and the tooltip "This cell is out of date") mean the action hasn't run for that row yet — for example, the run was stopped before reaching those rows, or auto-run wasn't enabled when they were added. To process the remaining rows, right-click the column header and select **Run column → Run [N] empty or out-of-date rows**. See [Run progress](run-progress.md) for a full explanation of cell states.
-   **The "Send data to table with auto-run on" confirmation dialog shows a higher cost estimate than you expect to pay.** The dialog calculates "Estimated total cost" by multiplying the per-row credit estimate by the total number of rows being sent — it does not filter for run conditions. If your Send table data column has a run condition, only rows where the condition evaluates to true will actually run and consume credits; rows that show "Run condition not met" are skipped at no cost. The dialog's own tooltip notes this is a *maximum* estimate: "actual usage may vary based on your data and configurations."
-   **All rows in the destination table show the same contact's data (for example, the same email or LinkedIn URL repeated across every row):** the field mappings within the list are referencing a fixed indexed position (like the first contact) instead of each item's own data. Delete the Send Table Data column and recreate it using **Take action on list** from the cell details panel (see [Using Send row for each item in a list](#using-send-row-for-each-item-in-a-list)), which auto-configures both the list source and the correct per-item field mappings.
-   **Some rows show `"Invalid send table data inputs … 'listData' … 'Required'"` while others succeed (using `Send row for each item in a list`):** This error means the list column had no data for that specific row — for example, an enrichment returned no results for that company, or a webhook event didn't include the expected field. Clay validates each row individually at runtime, so rows with a valid list array succeed and rows without one fail. **Fix:** Add a [run condition](https://university.clay.com/docs/conditional-runs) to the Send Table Data column so it only runs when the list column is not empty. For example, if your list column is `Find Contacts at Company`, set the condition to run only when `Find Contacts at Company` has a value.
-   **Send to Table is creating new columns in the destination table instead of populating my existing ones.** By default, `Auto-extract new columns` creates a new column for each incoming field. To route incoming data into an *existing* column instead: open the destination table, click the **"rows from: [source table name]"** cell, hover over the field you want to map (e.g., an email address), and click **Add to column** — then select an existing column from the dropdown (labeled **Map to an existing column**). Repeat for each field you want to map. If the existing column is empty, dismiss the data-overwrite warning safely. To map multiple fields at once, enable **Auto-map existing columns** in the action's advanced settings — Clay will automatically set formulas on all destination columns whose names match incoming fields. Note that for columns with manually entered or CSV-imported values, this will overwrite that existing data.
