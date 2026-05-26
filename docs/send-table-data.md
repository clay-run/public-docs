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

1.  While in a table, click `Exports` → `Send table data`.
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
-   Rename any field in the destination table using the destination column dropdown.

**Note:** When you first send a row, it creates a new row in the destination table. For subsequent sends, it updates that same row. This applies to both regular row data and nested data. You can turn this off to always create a new row via the \`Update existing rows on re-run\` setting.

### Using `Send row for each item in a list`

Each cell can hold a list of items—like a list of people found at a company. To turn each item in that list into its own row in another table, use `Send row for each item in a list`.

This is useful for **flattening lists**. For example, if you find multiple people at a company, you can send each person as a separate row in the destination table. **This method always creates a new row for each item.**

You can also select additional data to send along with the flattened list, just like with `Send row`.

**Tip: Use "Take action on list" to set this up automatically**

The easiest way to configure `Send row for each item in a list` is to use the **Take action on list** shortcut from the cell details panel:

1.  Click on a cell in the column whose list you want to flatten (for example, a "Find Contacts at Company" result cell).
2.  In the Cell details panel, hover over the list section (e.g., "People") to reveal the **Take action on list** button.
3.  Select **Write each item to new row in other table**.

This opens the Send Table Data configuration with the correct list field already pre-populated — so you don't need to manually identify which field to use as the list source.

**Selecting the right list field manually**

When configuring the list field by hand, select the **list itself** (e.g., `People`), not an indexed element from within that list (e.g., `People.0`, which is just the first person). Selecting a single indexed element instead of the whole array is a common source of confusion: the configuration will show a **"Please add a valid list."** error because an indexed element isn't recognized as a list.

If your table has no rows with data yet, Clay skips this validation and accepts the formula as-is. In that case, run a few rows first so the enrichment column has real output, then re-open the Send Table Data configuration to confirm the list field is valid before running the full table.

**Next step: extract fields as columns in the destination table**

After each list item arrives as a new row in the destination table, its fields are stored inside the source cell — they won't automatically appear as separate columns. To surface individual fields like Title, Company, Start Date, or Is Current, you need to extract them. Enable **Auto-extract new columns** (see [Advanced settings](#advanced-settings)) when configuring Send Table Data to create those columns automatically, or follow the steps under [Mapping table data in the destination table](#mapping-table-data-in-the-destination-table).

## Advanced settings

**Update existing rows on re-run**

When re-running, updates the matching row in the destination table instead of creating a new one.

**Auto-extract new columns**

Automatically creates new columns in the destination table for any that don't already exist.

**Auto-map existing columns**

For existing columns in the destination table, updates the formula to reference the configured source data. For columns without a formula (e.g., manually entered data or CSV imports), the formula won't be updated to avoid overwriting data.

## Mapping table data in the destination table

When you send data to a destination table, it appears in the leftmost column as **"rows from: \[source table name\]"**. The data is stored within this cell and needs to be extracted into individual columns to use it in your workflow.

**Tip:** You can automatically extract all fields to new columns by enabling the `Auto-extract new columns` setting when configuring Send table data. This creates a column for each field in the destination table.

To manually map data from the source column to columns in the destination table:

1.  Click into the source cell (the "rows from: \[source table name\]" cell).
2.  Hover over any field you want to extract.
3.  Click `Add to column`.
4.  Choose to either:
    -   **Create a new column**: Name the column and click `Create column`.
    -   **Map to an existing column**: Select an existing column from the dropdown.
        -   If the column doesn't already have a formula configured, you'll see a warning about the risk of overwriting data. If the column is empty, it's safe to proceed.

Repeat this process for each field you want to extract into its own column.

## Guide: Merging two tables with Send table data

## Best practices & troubleshooting

-   There can be a **maximum of 20 tables** connected. **This includes tables across workbooks.**
-   **Data can only be sent in a linear direction** (A → B → C). In other words, loops are not possible (A → B → C → A).
    -   If you want to receive data in the table you're also sending data from, use one of these other actions:
        -   `Lookup Multiple Rows in Other Table`
        -   `Lookup Single Row in Other Table`
-   **"✅ Sent" means Clay dispatched the data — not that it has appeared at the destination yet.** The `Sent At` timestamp and `Number Of Rows Sent` shown in the cell details confirm that Clay successfully placed those rows into the destination table's incoming source. The destination table still needs to process those rows before they become visible. To verify data is arriving, open the destination table and check its [column progress bar](https://university.clay.com/docs/run-progress-ui).
