---
title: Write to Other Table
description: Easily transfer data between Clay tables.
last_synced: 2026-04-26T01:40:56.846Z
---

# Write to Other Table

Easily transfer data between Clay tables.

**Write to Other Table is deprecated as of December 2025.** You cannot create new Write to Other Table actions — the action panel shows a deprecation notice when you try. Existing actions will continue to work. For all new multi-table workflows, use [Send Table Data](https://university.clay.com/docs/send-table-data), which replaces Write to Other Table with additional functionality including built-in upsert support and no API key required.

**Migrating to Send Table Data:**
- **List mapping** (sending each list item as its own row): use **Send row for each item in a list**
- **Column mapping** (copying specific columns to another table): use **Send row**

The **Write to Other Table** action in Clay connects data across tables, streamlining complex workflows, especially between _Company_ and _People_ tables.

A few example cases where you will find Write to Other Table useful:

-   **Parsing lists**: Break down a list in a cell and map each item to another table. _Ex. A list of emails._
-   **Column mapping**: Mirroring column data from one table to another.

## Setting up Write to Other Table

To set up the action, you'll need:

-   **Clay API Key:** [Your Clay API key](https://www.clay.com/university/guide/guide-find-clay-api-key) to create an integration.
-   **Source table:** The parent table to copy data from.
-   **Destination table:** The child table to send data to.

## Using Write to Other Table

### Use Case #1: List Mapping

_Use Write to Other Table to map out lists to into rows for another table._

Each cell can contain a list of items (e.g., find contacts at company). Use **Write to Other Table** to map each item individually to rows in the destination table.

**Step 1: Select your Clay account**

If no account is selected, obtain your API key to set up a Clay integration.

**Step 2: Select a table to write to**

Choose a destination table, ideally within your current workbook.

**Step 3: Select the column with lists**

Choose the column containing cells with lists you want to map (e.g., email addresses found in each cell).

**Step 4: Map list data to your new table**

Select the list properties to map into your new table columns.

**Step 5 (Optional): Configure run settings**

**Auto-update** will automatically enrich new rows if they are added.

The **Only run if** allows you to set conditions to control when the AI runs. For example, you can make the AI run only if specific data fields are filled.

### Use Case #2: Column mapping

_Use Write to Other Table to copy columns from one table to another._

**Copying Columns** lets you transfer specific columns from one table to another, keeping data aligned and consistent. This simplifies workflows by reducing manual data entry across tables.

#### Tutorial

**Step 1: Select your Clay account**

If no account is selected, obtain your API key to set up a Clay integration.

**Step 2: Select a table to write to**

Choose a destination table, ideally within your current workbook.

**Step 3: Omit the list by entering /**

Enter "/" to skip list selection, as you won't be mapping a list in this step.

**Step 4: Map out columns**

Select the columns you want to copy from the source table and match them to the appropriate columns in the destination table.

**Step 5 (Optional): Configure run settings**

**Auto-update** will automatically enrich new rows if they are added.

The **Only run if** allows you to set conditions to control when the AI runs. For example, you can make the AI run only if specific data fields are filled.

## Write to Other Table constraints

The **Write to Other Table** action has two main constraints that you might come across.

-   Write to Other Table connections count toward the same workspace-wide table connection limit as Send Table Data (20 tables by default). **This includes tables across workbooks.** If you exceed the limit, you'll see the error: *"Maximum number of table ID checks exceeded (limit: 20)"*.
-   Data can only be sent in a linear direction (A → B → C). In other words, loops are not possible (A → B → A).
    -   If you want to go the other direction, you can reference data from any table (B→ A) using one of these other actions:
        -   **`Lookup Multiple Rows in Other Table`**
        -   **`Lookup Single Row in Other Table`**

## FAQ

### **I received an "Invalid credentials" error, what can I do?**

This error means your Clay API key is incorrect or missing. To fix:

1.  Go to **Settings** → **Connections** and search for **Clay**.
2.  Update or re-enter your Clay API key. See [Find Your Clay API Key](https://www.clay.com/university/guide/guide-find-clay-api-key) if you need to locate it.
3.  Save your changes and retry the action.

### **Why am I seeing the error "You cannot write to the selected table because the sequence of Write to Other Table integrations is misconfigured"?**

This error occurs when there's invalid or conflicting data, such as:

-   Writing to a deleted column.
-   Sending data to a table that references another table.

To Fix:

1.  Reconfigure your **Write to Other Table** integrations.
2.  Double-check that all columns and tables exist and are correctly set up.
3.  Add the integrations again to ensure no misconfigurations remain.

### **How do I send comma separated data within a cell to a new column?**

If you have data in a comma-separated list and want to send it to a new column or table, follow these steps:

1.  Use **Extract Data From Values** to process the CSV data.
2.  Add the correct column using the **Forward Slash** (/) command.
3.  Apply a custom extraction **Regex**: `[^,"]+\"?[^,"]+`

This will split the values into a list.

Once complete, you can send the newly created list to the desired column or table.

### **Can I write individual values to another table, or does it have to be a list?**

Lists are optional. You can write individual values or entire lists depending on your column setup.

### **What should I do if my Write to Other Table column isn't processing correctly?**

If the column isn't running, force-run it: right-click the column header and select **Run column** → **Force run all [N] rows**. This re-queues every row regardless of its current status.

If the issue persists, rebuild the column:

1.  Delete the affected Write to Other Table column.
2.  Create a new Write to Other Table column and reconfigure the mapping.
3.  Re-map your data to the destination table. Ensure **auto-dedupe** is enabled in the destination table (see [Auto-dedupe](table-management-settings.md#auto-dedupe)) to prevent duplicate rows.
