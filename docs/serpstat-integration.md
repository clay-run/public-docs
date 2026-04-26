---
title: SerpStat integration
source_url: https://university.clay.com/docs/serpstat-integration
description: Aggregate data from various regions to assess online visibility and reach.
last_synced: 2026-04-26T01:40:39.887Z
upstream_hash: 3d2402c4942e2d4f1799ab8c41b4adeb2cdafae86a710721a7385630550e5b9e
---

# SerpStat integration

Aggregate data from various regions to assess online visibility and reach.

SerpStat provides insights into the geographic sources of a company's organic web traffic, estimating monthly traffic and identifying key markets for targeted strategies.

The integration aggregates data from various regions to assess online visibility and reach, presenting key metrics for comprehensive market analysis.

## **Enriching data with SerpStat**

1.  While in a Clay table, click `Add enrichment` and search for `SerpStat`.
2.  Under `Integrations`, select one of the SerpStat options.
    -   If you have your own account, click `+ Add account` and go through authentication. Otherwise, use the Clay provided key.

### `Action` Get traffic distribution by geography

Use this action to get insights into the geographic sources of a company's organic web traffic, enabling identification of key markets and informing targeted marketing strategies.

**Inputs**

-   **Company domain:** Company website (e.g., `google.com`, `ads.google.com`, or `google.com/maps`)
-   **Country limit (Optional):** Number of countries to return. Default is `10`, maximum is `100`. One credit per country.

**Output**

-   **Country code:** Two-letter country code
-   **Country name:** Full name of the country
-   **Estimated monthly organic traffic:** Estimated number of monthly organic visits from this country
-   **Google domain:** The Google domain used in that country

### `Action` Get website traffic

Use this action to get estimated monthly organic web traffic data for companies based on their website domains, helping users assess online visibility and reach.

**Inputs**

-   **Company domain:** Enter the target website domain (e.g., `google.com`, `ads.google.com`, or `google.com/maps`)

**Output**

-   **Analyzed domain:** The domain that was analyzed
-   **Regions count:** Number of regions/countries with traffic data
-   **Total estimated monthly organic traffic:** Estimated total monthly organic website visits

### **Run settings**

-   **Auto-update**
-   **Only run if:** The enrichment will only run if conditions are met. ([Learn more about conditional formulas here!](https://www.clay.com/university/lesson/ai-formulas-conditional-runs-clay-101))
