---
title: Google News integration
description: News aggregator delivering current events and information.
last_synced: 2026-04-26T01:40:03.783Z
---

# Google News integration

News aggregator delivering current events and information.

## Google News Overview

Google News in Clay allows users to find news results for a given query, or pull a stream of news articles as rows in a Clay table.

## **Available Actions with the Google News Integration**

### `Action` Find News Results

Given a query find results from Google News.

**Step 1:** Enter search query.

Provide the query you want to search for. You can input plain text directly or reference data from other columns to dynamically generate the query.

**Step 2 (Optional):** Specify the language for the search.

If no language is provided, the search will default to English.

**Step 3 (Optional):** Filter news results by date, selecting a range from the past hour to the past year. Note that Google's date filtering is best-effort — for niche or company-specific searches, Google News may return articles from outside the selected range.

**Step 4:** Configure run settings.

By default, new rows within your Clay table will automatically run the Google News action. Learn more about auto-update in [this brief guide](https://docs.clay.com/en/articles/9642165-auto-update-and-auto-dedupe-table).

To run enrichment only under specific conditions, use formulas that trigger the column when the formula is true. Learn more about AI formulas in [this Clay University lesson](https://www.clay.com/university/lesson/ai-formulas-conditional-runs-clay-101).

**Step 5:** Run your enrichment to find results from Google News.

## Output fields

The **Find News Results** action returns two output fields:

- **`news_results`** — An array containing the individual news articles found. Each article includes the title, URL link, source name, publication date, and a text snippet.
- **`total_news_results`** — A number representing the total count of articles returned.

### Waterfall output: why the merged column shows a number

When **Find News Results** is used as a step in a waterfall column, the **Waterfall output** dropdown controls which field appears in the merged column:

- If you select **`total_news_results`**, the merged column displays a number — the count of articles found (for example, `5` or `60`). This is a count, not the articles themselves.
- To display article data in the merged column, select a field from **`news_results`** — for example, `news_results > 0 > title` to show the first article's headline, or `news_results > 0 > link` for its URL.

To browse all articles returned for a row — regardless of which field is selected in the merged column — expand the waterfall by clicking the **»** arrow on the column header, then click into the Google News sub-column cell for that row. The cell details panel shows the full list of articles.

To change the waterfall output field: click the waterfall column header → **Edit column** → open the **Waterfall output** dropdown and select a different field → click **Save**.

### "Run condition not met" on sub-columns

If a sub-column within the waterfall shows **"Run condition not met"**, it means the waterfall's run condition was not satisfied for that row — for example, if the query input column is empty. Rows with no input will be skipped and shown with this status; no credits are consumed for those rows. See [Conditional runs](conditional-runs.md) for how to set or adjust run conditions.

## `Source` Pull Google News RSS Feed

The **Pull Google News RSS Feed** source imports Google News articles into a Clay table as rows. Use it to monitor ongoing topics — such as business expansions, facility relocations, or company announcements — and enrich, filter, or route the results with other Clay columns.

**Step 1:** Add the source to your table.

In a workbook, click `+ Add` at the bottom. Search for `Google News RSS` and select **Pull Google News RSS Feed**.

**Step 2:** Configure your search.

-   **Has words** — Articles must contain these words (e.g., `warehouse expansion relocation`).
-   **Exact phrase** (optional) — Articles must include this phrase verbatim (e.g., `distribution center opening`).
-   **Exclude words** (optional) — Filter out articles that contain these words.
-   **Website** (optional) — Restrict results to a specific domain (e.g., `businesswire.com`).

**Step 3:** Set the date range.

Filter by recency: **Past hour**, **Past 24 hours**, **Past week**, or **Past 30 days**.

**Step 4:** Set a result limit (optional).

Specify the maximum number of articles to return, up to 100.

**Step 5:** Click `Import to new table` to load matching articles as rows.
