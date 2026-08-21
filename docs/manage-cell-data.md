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

Clay enforces three types of cell size limits:

-   **Basic columns** (text and formula columns): 8 kB limit
-   **Source columns** (the **"Rows from: [source table name]"** column in destination tables that receives data via Send Table Data): 100 kB limit
-   **Action columns** (enrichment outputs): 200 kB limit

When a basic column's data exceeds the 8 kB limit, the cell shows **"Cell data size exceeds limit (8 kB)"**. The final step of a waterfall returns a basic column with an 8 kB limit. If your waterfall contains large amounts of data, it may exceed this limit.

**Common scenarios where cell size limits are encountered:**

-   **Gong transcripts:** Often exceed the 200 kB limit.
-   **Technology waterfall (BuiltWith):** Can output over 200 kB; use keywords to filter.
-   **HTTP-API and webhooks:** May bring in over 200 kB; use field-path filters.
-   **Snowflake Lookup:** Large query results can exceed the 200 kB limit. Select only the columns you need instead of `SELECT *`, and avoid broad wildcard patterns (e.g., a leading `%` in an `ILIKE` clause) that match far more rows than intended. See the [Snowflake integration](snowflake-integration.md) page for additional tips.
-   **Lookup Multiple Rows in Other Table:** Lookup Multiple Rows results are stored in action columns, which have a hard 200 kB limit. The error **"Cell data size exceeds limit (200 kB)"** can appear even when the lookup stays within the 100-record cap — records with densely populated fields (few blank values) produce a larger payload than sparsely populated ones, so 100 fully populated records can exceed the limit while 100 sparse ones do not. To fix this, lower the **Limit** setting in the lookup column's configuration (default 100, max 100) to a smaller number so fewer records are returned per row. See [Lookup Rows](lookup-rows.md) for configuration details.
-   **Extracting large enrichment outputs to formula or text columns:** Formula and text columns enforce an 8 kB limit. When you use a formula to pull content from a large enrichment — for example, job postings from a **Find Active Job Openings** or **Find Open Jobs** enrichment, or articles from a **Find Most Recent News** enrichment — the cell shows **"Cell data size exceeds limit (8 kB)"** or goes blank when the full enrichment output exceeds 8 kB. Three workarounds:
    -   **Filter to specific fields in the enrichment settings.** Open the enrichment column settings and, if the enrichment includes a **Filter data by field paths** or **Extract data by field paths** option, configure it to return only the fields you need (for example, just the job title and description rather than the full posting). This keeps the enrichment output small enough to extract specific fields into formula columns.
    -   **Reference the enrichment column directly in a Use AI column.** Instead of pulling raw content into a formula column, point a **Use AI** (Claude, GPT, or another model) column directly at the enrichment column and prompt it to analyze or summarize the data — for example, "What roles is this company currently hiring for?" The enrichment action column holds up to 200 kB, so the AI column reads the full output without hitting the 8 kB restriction and returns a structured answer.
    -   **Extract individual items into separate columns.** If the enrichment returns a list, create one formula column per item using its index — for example, `{{Enrichment Column}}?.results?.[0]?.title` for the first item and `{{Enrichment Column}}?.results?.[1]?.title` for the second — rather than joining all items into one column. You can also click a populated enrichment cell, hover over any nested field in the cell details panel, and click **Add column** to add that specific field as its own column.
-   **Long text in text columns:** Long email replies (e.g., from the campaign events table) and AI-generated text such as personalized outreach messages or reply drafts can exceed the 8 kB limit when stored in a text column, showing **"Cell data size exceeds limit (8 kB)"**. To work around this, add a formula column with `LEFT({{Column Name}}, 7000)` to extract the first 7,000 characters, then use that formula column as input to downstream AI columns or exports.
