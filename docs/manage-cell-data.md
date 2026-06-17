---
title: Manage cell data
source_url: https://university.clay.com/docs/manage-cell-data
description: Learn how to manage cell data within your Clay table.
last_synced: 2026-04-26T01:40:19.169Z
---

# Manage cell data

Learn how to manage cell data within your Clay table.

## Viewing and interacting with cell data

All cell data in Clay is stored as JSON, but Clay makes it easy to view and interact with it in a human-readable format:

-   **Click on a cell** to open it in the right-side panel, which displays the cell’s data in a more readable format.
-   **Hover over a cell** to see a brief summary of its content—a compact view of the data stored.

Clay provides several ways to extract specific values out of cells and into columns:

-   **Click and drag** a specific value from the cell panel to an existing column in your table, or drop it into an empty area to create a new column. This is an easy way to pull specific fields out of enrichment results.
-   **Add field path filter:** When you add an enrichment, configure the column to extract specific fields from the enrichment output. Use this to pre-select the fields you want to surface when you set up the enrichment.
-   **Dot notation in formulas:** Reference specific fields from an enrichment result using dot notation in a formula column. For example, if you have an enrichment stored in a column named `Find Company` and want to extract the `name` field, you can write `{{Find Company}}.name` in the formula.

## Cell data size limits

Clay enforces cell data size limits based on the type of column:

| Column type | Size limit |
| --- | --- |
| Enrichment/action column | 200 kB |
| Basic column (extracted field, formula, text) | 8 kB |

### Why does my data appear truncated in an extracted column?

When you extract a value from an enrichment column into a basic column, the basic column has an 8 kB limit. If the original data exceeds this limit, the extracted value will be truncated or empty.

To work around this, reference the enrichment column directly in downstream enrichments and AI columns, rather than extracting the value to an intermediate column. You can reference enrichment column outputs using the `/` picker in any enrichment or AI input field.

### When does the 200 kB limit on enrichment columns apply?

The 200 kB limit applies to the output data stored in an enrichment or action column. If your enrichment returns more than 200 kB of data (for example, a large web page scrape), Clay will not store the excess data and you may see incomplete results.

Common cases where the 200 kB limit may be hit:

-   **Web scraping:** Pages with large amounts of content or embedded data.
-   **HTTP-API and webhooks:** May bring in over 200KB; use field-path filters.
-   **Extracting to basic columns:** May hit the 8KB limit when extracting large action fields.
-   **Email reply content:** Long email replies (e.g., from the campaign events table) can exceed the 8KB limit when written to a text column. To work around this, reference the reply field in a formula column and use a text function such as `LEFT({{Reply Body}}, 7000)` to extract just the first portion of the content.

### "The value in this field is larger than the cell size limit" error

When you try to extract a large enrichment value into a text or formula column and the value exceeds 8KB, Clay shows this warning:

> The value in this field is larger than the cell size limit of an extracted column. To reference this data, you should use the enrichment or source output directly.

**Creating a formula column that references the extracted column will not help** — formula columns share the same 8KB limit as text columns.

**The fix:** Instead of extracting the value to a separate column, add the enrichment action column's output as a direct input to your downstream enrichment or AI column. In the input field, use the slash picker (`/`) to select the original enrichment column's nested output value. This passes the data between enrichment columns without writing it to a basic column, so the 8KB limit does not apply.

**Cross-table workflows:** Lookup columns (e.g., Lookup Single Row in Other Table) also pass data through a basic column and are subject to the same 8KB cap. If your large enrichment output is in one table and you need to process it in another, move the downstream enrichment step into the same table as the large action column, reference the output directly there, and use Send to Table Data to push the result to your other table.
