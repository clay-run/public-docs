---
title: Zenrows integration
source_url: https://university.clay.com/docs/zenrows-integration-overview
description: Extract data from websites with the Zenrows scraper.
last_synced: 2026-04-26T01:40:58.780Z
---

# Zenrows integration

Extract data from websites with the Zenrows scraper.

## Connecting to Zenrows

1.  In the home sidebar, click `Settings` → `Connections`.
2.  Click `Add connection` and search for `Zenrows`.
3.  Enter your Zenrows API key, which you can find in your [Zenrows dashboard](https://app.zenrows.com/).
4.  Click `Authenticate` to save the connection.

## Enriching data with Zenrows

1.  While in a Clay table, click `Add enrichment` and search for `Zenrows`.
2.  Under `Integrations`, select `Zenrows`.
3.  In the modal, you will be asked to `Select Zenrows account`.
    -   If you haven't already connected your Zenrows account, click `+ Add account` and go through authentication.

### `Action` Scrape Website

Run a Zenrows scrape on a website URL.

**Inputs**

-   **Scrape URL:** The URL you want to scrape. Must be a valid URL.
-   **Autoparse**: Automatically parse the scraper response. When enabled, the CSS Extractors and HTML Output Fields options are hidden.
-   **CSS Extractors** *(only when Autoparse is off)*: Provide CSS selectors in JSON format to extract specific elements (e.g. `{"links": "a @href", "images": "img @src"}`). Takes precedence over HTML Output Fields.
-   **HTML Output Fields** *(only when Autoparse is off)*: Select which HTML elements to return—Title, Keywords, Description, Social Links, Emails, Phone Numbers, Body Text, and more. Overridden by CSS Extractors when specified.
-   **Render Javascript**: Enable to render JavaScript with a headless browser for pages that require it.
-   **Wait Time (ms)**: Milliseconds to wait before scraping (0–20,000). Only applies when Render Javascript is enabled.
-   **Wait for CSS selector** *(only when Render Javascript is on)*: A CSS selector to wait for in the DOM before scraping. Takes precedence over Wait Time.
-   **Premium Proxy**: Use a premium proxy for privacy.
-   **Anti-Bot**: Enable anti-bot measures for bot-protected sites.
-   **Proxy Country**: Specify proxy's country with a two-letter code.
-   **Extract data by field paths**: Filter the returned data using JSONPath expressions. Enable filtering, then choose Include or Exclude mode and enter one or more paths (e.g. `$.store.books[*].title`). Use the "Use AI" button to generate paths automatically.

**Run settings**

By default, new rows within your Clay table will automatically be formatted. Learn more about auto-update in [this brief guide](https://docs.clay.com/en/articles/9642165-auto-update-and-auto-dedupe-table).
