---
title: Zenrows integration
description: Extract data from websites with the Zenrows scraper.
last_synced: 2026-04-26T01:40:58.780Z
---

# Zenrows integration

Extract data from websites with the Zenrows scraper.

Zenrows is a web scraping service that helps you extract data from websites efficiently.

With this integration, you can reliably return website information directly into your Clay table.

## Setting up the Zenrows integration

1.  While in a Clay table, click `Add enrichment` and search for `Zenrows`.
2.  Under `Integrations`, select the Zenrows action.
3.  By default, you will be using your Clay-managed Zenrows account, but you can also select `+ Add Account` if you have your own Zenrows account.

## Using the Zenrows integration

### `Action` Run Zenrows scrape

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

-   **Auto-update**
-   **Only run if:** The enrichment will only run if conditions are met.
