---
title: Zenrows integration
source_url: https://university.clay.com/docs/zenrows-integration-overview
description: Extract data from websites with the Zenrows scraper.
last_synced: 2026-04-26T01:40:58.780Z
upstream_hash: b67a9643e22db9f692aa7f8fff672f59032a956b1ae8b8615d6eb6ba3b8d16a7
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

-   **Company URL:** The URL you are trying to scrape.
-   **Autoparse**: Automatically parse scraper response.
-   **HTML Output Fields**: Select specific HTML elements to extract.
-   **Render Javascript**: Enable for pages needing JavaScript.
-   **Premium Proxy**: Use a premium proxy for privacy.
-   **Anti-Bot**: Enable anti-bot measures for protected sites.
-   **Proxy Country**: Specify proxy’s country with a two-letter code.

**Run settings**

-   **Auto-update**
-   **Only run if:** The enrichment will only run if conditions are met.
