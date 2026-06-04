---
title: Serper integration overview
source_url: https://university.clay.com/docs/serper-integration-overview
description: Use Serper.dev to perform Google searches and scrape Google Maps data at scale in Clay, including performance limits and batch recommendations.
last_synced: 2026-06-04T00:00:00.000Z
---

# Serper integration overview

Use Serper.dev to perform Google searches and scrape Google Maps data in Clay.

Serper.dev is a Google Search API that powers Clay's **Search Google** enrichment. For advanced use cases such as Google Maps scraping with custom pagination, you can also call Serper directly via the [HTTP API](http-api-integration-overview.md) integration.

## Available actions

### `Action` Search Google (Perform Search)

Perform any Google search query and return results, including organic results, ads, and result counts.

**Inputs**

-   **Google search query**: The query to search for (e.g., `{{"Company Domain"}} mentions in the news`).
-   **Number of results** (Optional): Number of results to return. Defaults to 5. Maximum is 10.
-   **Language** (Optional): Language for the search. Defaults to English.
-   **Country** (Optional): Country to scope the search to. Defaults to United States.
-   **Include Result Count** (Optional): When enabled, returns the approximate total result count from Google.
-   **Include Ads** (Optional): When enabled, ad results are included.

**Outputs**

-   **Search Results**: An array of results, each containing position, title, link, redirect link, displayed link, and thumbnail.

## Using Serper for Google Maps scraping

To scrape Google Maps listings, call Serper's Places endpoint directly using the [HTTP API](http-api-integration-overview.md) integration. Each call covers one page of results — add one column per page to collect multiple pages of results for a given location.

**Tip:** Use Serper's **Places endpoint** (`https://google.serper.dev/places`) rather than the Maps endpoint. The Maps endpoint returns vastly different results for each page, making systematic collection unreliable.

## Performance at scale

Serper.dev behaves more like a scraping service than a stable API. At scale — for example, a table with hundreds of rows and multiple Serper columns running simultaneously — Serper can silently throttle requests. This causes columns to run very slowly without surfacing an obvious error message.

To avoid hitting these limits:

-   **Run in batches**: Process your table in smaller groups of rows rather than running all rows at once.
-   **Limit to 3 concurrent locations at a time**: Running more than 3 locations simultaneously can trigger Serper's rate limits. Serper tends to overestimate its own rate limits, so staying at 3 or fewer concurrent locations is the safest threshold.
-   **Use sequential columns with conditional logic**: If you have multiple Serper columns (e.g., one per page of results), use [conditional runs](conditional-runs.md) to gate each column on the previous one completing, rather than running all columns in parallel.

For production-scale Google Maps scraping across many locations (state-wide or country-wide), consider handling pagination outside Clay — using a workflow tool like n8n or Make, or a Python script — then pushing results into a Clay table via [webhook](webhook-integration-guide.md) for further enrichment.

## Run settings

-   **Auto-update**: When enabled, the enrichment re-runs automatically when input values change.
-   **Only run if**: Use a formula to control when the enrichment runs. ([Learn more about conditional formulas](https://www.clay.com/university/lesson/ai-formulas-conditional-runs-clay-101))
