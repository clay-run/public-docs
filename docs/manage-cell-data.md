---
title: Manage cell data
description: Learn how to manage cell data within your Clay table.
last_synced: 2026-04-26T01:40:19.169Z
---

# Manage cell data

Learn how to manage cell data within your Clay table.

## Inspect cell details

View and analyze enriched data or outputs within a specific cell.

To inspect cell details:

1.  Locate the cell you want to inspect.
2.  Click on the cell to open the cell details panel.

If you re-run a cell while the cell details panel is open, the output automatically refreshes to show the latest data — no need to close and reopen the panel or reload the page.

## Search within a cell

Quickly find specific data within a cell's outputs using the search feature.

To search for outputs in a cell:

1.  Click on the cell to open the cell details panel.
2.  Type a keyword or data point into the search bar to filter and display matching outputs.

## Cell output schema

A cell output schema describes how data is structured in an enrichment output. It shows:

-   **Keys and values:** Labels like "Company Name" or "Contact Email" with their corresponding data types (text, numbers, or lists).
-   **Organization:** Whether data is a single value (e.g., "John Doe") or a grouped list (e.g., multiple contacts).
-   **Nested data:** Information grouped under larger categories. For example, "Company Lookalikes" might contain "Lookalike #1" and "Lookalike #2," each with their own details.

## Lists

A list is an array of items grouped together in a single cell. Lists most often appear as outputs from enrichment (action) columns — for example, a "Find Contacts at Company" enrichment returning multiple people. They can also be produced by a formula column that returns an array (e.g., `[{{Col1}}, {{Col2}}, {{Col3}}]`).

Lists use zero-based indexing, where the first item is at index 0, the second at index 1, and so on. For example, in a skills list, "Solution Selling" is at index 0, "Cloud Computing" is at index 1, and "Virtualization" is at index 2.

## Take action on a list

In the **Cell details** panel, click **Take action on list** to access the following actions:

-   **Filter, find keywords, and more using formula:** Search for and filter specific items using formulas.
-   **Write each item to new row in other table:** Send each list item as its own row to another table.
-   **Create column with items separated by commas:** Join all items into a single comma-separated text field (only available for lists of simple values).
-   **Ask question about items with AI:** Get answers or summaries about the list using AI.

## Cell size limits

Clay has two types of cell size limits:

-   **Basic columns** (text and formula columns): 8KB limit
-   **Action columns** (enrichment outputs): 200KB limit

The final step of a waterfall returns a basic column with an 8KB limit. If your waterfall contains large amounts of data, it may exceed this limit.

**Common scenarios where cell size limits are encountered:**

-   **Gong transcripts:** Often exceed the 200KB limit.
-   **Technology waterfall (BuiltWith):** Can output over 200KB; use keywords to filter.
-   **HTTP-API and webhooks:** May bring in over 200KB; use field-path filters.
-   **Snowflake Lookup:** Large query results can exceed the 200 kB limit. Select only the columns you need instead of `SELECT *`, and avoid broad wildcard patterns (e.g., a leading `%` in an `ILIKE` clause) that match far more rows than intended. See the [Snowflake integration](snowflake-integration.md) page for additional tips.
-   **Extracting to basic columns:** May hit the 8KB limit when extracting large action fields.
-   **Email reply content:** Long email replies (e.g., from the campaign events table) can exceed the 8KB limit when written to a text column. To work around this, reference the reply field in a formula column and use a text function such as `LEFT({{Reply Body}}, 7000)` to extract just the first portion of the content.