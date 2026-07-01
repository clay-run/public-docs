---
title: Serper integration overview
description: Use Serper.dev to perform Google searches and scrape Google Maps data at scale in Clay, including performance limits and batch recommendations.
last_synced: 2026-06-04T00:00:00.000Z
---

# Serper integration overview

Use Serper.dev to perform Google searches and scrape Google Maps data in Clay.

Serper.dev is a Google Search API that powers Clay's **Search Google** enrichment. For advanced use cases — such as using your own Serper API key or scraping Google Maps with custom pagination — you can also call Serper directly via the [HTTP API](http-api-integration-overview.md) integration.

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

### `Source` Find with a Google Search

Pull Google search results as rows into a Clay table. Use this source when you want to seed a list from a Google search query — for example, finding companies, websites, or people matching a specific pattern.

**Inputs**

-   **Google search query**: The query to run. Supports Google search operators (e.g., `site:crunchbase.com intitle:"CEO"`). See [Using Google search operators](#using-google-search-operators) below.
-   **Number of results** (Optional): Number of results to return. Maximum is 300.
-   **Language** (Optional): Language for the search. Defaults to English.
-   **Country** (Optional): Country to scope the search to. Defaults to United States.

**Outputs**

Each result row contains: Title, Link, Displayed link, Snippet, Position, Thumbnail, Favicon, and Source.

## Using Google search operators

The **Google search query** field in both **Find with a Google Search** and **Search Google (Perform Search)** accepts standard Google search operators for precision targeting:

-   `site:` — restrict results to a specific domain (e.g., `site:crunchbase.com`)
-   `intitle:` — match pages with a specific word in the title (e.g., `intitle:"CEO"`)
-   `inurl:` — match pages with a specific word in the URL (e.g., `inurl:about`)
-   `" "` — exact phrase match (e.g., `"software company"`)
-   `AND` / `OR` — combine or broaden search terms
-   `-` — exclude pages containing a specific term

**Example:** To find technology company executive profiles on a professional directory:

```
site:crunchbase.com intitle:"CEO" AND ("software company" OR "tech startup")
```

## Using Serper with your own API key

Clay's built-in **Search Google** enrichment runs through Clay's managed Serper account. If you have your own Serper API key — for example, to run higher volumes or access additional Serper endpoints — you can call Serper's API directly using the [HTTP API](http-api-integration-overview.md) integration.

**Requirement:** HTTP API is available on Growth plan and above. See [plans and billing](plans-and-billing.md) for details.

To set this up:

1.  Create an account at [serper.dev](https://serper.dev/) and copy your API key.
2.  In the Serper dashboard, select **Playground** → **Code** → **cURL** to view the endpoint URL, request headers, and JSON body structure for the endpoint you want to use (e.g., `https://google.serper.dev/search`).
3.  Add an **HTTP API** column to your Clay table. Configure it with the same endpoint URL, headers (add your Serper API key as the value for the `X-API-KEY` header), and body structure from the cURL output.
4.  Build your Google search query using a formula — Serper's `q` parameter expects a single query string, so use a formula to combine any dynamic inputs into one string.
5.  Save and run the column to execute the search and return results.

For **Google Maps** use cases, see [Using Serper for Google Maps scraping](#using-serper-for-google-maps-scraping) below.

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
