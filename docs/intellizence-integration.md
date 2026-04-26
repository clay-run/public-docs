---
title: Intellizence integration
source_url: https://university.clay.com/docs/intellizence-integration
last_synced: 2026-04-26T01:40:11.949Z
upstream_hash: 76d723f8fd38c8b233d8b0d58561c6390878ef96946b33eefcb42b9b96cde3c4
---

# Intellizence integration

Enrich your tables with company. news and funding info.

Intellizence is a business intelligence tool for monitoring company activity and news.

This integration lets you enrich your Clay tables with company intelligence data from Intellizence, including news alerts and funding information.

## **Creating a table with Intellizence**

1.  In a workbook, click `+ Add` at the bottom.
2.  Search for `XXX` and select from the results.
3.  In the modal, you will be asked to `Select XXX account`.
    -   If you haven't already connected your XXX account, click `+ Add account` and go through authentication.

### `Source` **Find news for companies with Intellizence**

Find news for companies based on a list of provided domains.

**Inputs**

-   **Company Domains**: List of company domains.
-   **Earliest Publish Date (Optional)**
    -   _Note: Intellizence only covers selected companies with news after January 2024, and there may be up to a 72-hour delay before news is available._
-   **Topics (Optional)**
-   **Max News Events (Optional)**: Limit the number of articles.

## **Enriching data with Intellizence**

1.  While in a Clay table, click `Add enrichment` and search for `Intellizence`.
2.  Under `Integrations`, select one of the Intellizence enrichment options.

### `Action` Enrich Company with Latest News Data

Use this action to find the latest news about a company using its domain. _Note: Intellizence only covers selected companies after December 2023._

**Inputs**

-   **Company Domain**
-   **Earliest Publish Date (Optional)**
-   **Latest Publish Date (Optional)**
-   **Topics (Optional)**
-   **Max News Events (Optional)**

### `Action` Enrich Company with Latest Fundraising Data

Use this action to find the latest fundraising data about a company using its domain. _Note: Intellizence only covers venture-backed startups who have publicly announced funding after January 2022._

**Inputs**

-   **Company Domain**

### **Run settings**

-   **Auto-update**
-   **Only run if:** The enrichment will only run if conditions are met. ([Learn more about conditional formulas here!](https://www.clay.com/university/lesson/ai-formulas-conditional-runs-clay-101))
