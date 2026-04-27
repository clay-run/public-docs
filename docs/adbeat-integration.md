---
title: Adbeat integration
source_url: https://university.clay.com/docs/adbeat-integration
description: Helps with competitive analysis and lead generation by revealing
  advertising spend, successful campaigns,
last_synced: 2026-04-27T18:09:11.502Z
upstream_hash: a5359693b8c5faef7ba74f8e595f6728dda626f5c1d5793bc3c724e218e5b90c
---

# Adbeat integration

Helps with competitive analysis and lead generation by revealing advertising spend, successful campaigns,

Adbeat provides comprehensive insights into a company's advertising strategies by analyzing media mix, geographic data, and ad networks.

This integration aids in competitive analysis and lead generation by revealing advertising spend, successful campaigns, and potential partnership opportunities.

## **Enriching data with Adbeat**

1.  While in a Clay table, click `Add enrichment` and search for `Adbeat`.
2.  In the modal, you will be asked to `Select Adbeat account`.
    -   If you have your own account, click `+ Add account` and go through authentication. Otherwise, use the Clay provided key.

### `Action` Find the ad media mix and associated spend for a company

Provides detailed insights into how companies allocate their advertising budgets across different media channels within a specific time frame.

**Inputs**

-   **Company domain:** Website domain of the company you want to analyze (e.g., `apple.com`)
-   **Start date:** Beginning of the date range to analyze (`YYYY-MM-DD` format)
-   **End date:** End of the date range to analyze (`YYYY-MM-DD` format)
-   **Country (Optional):** Filter results to a specific country

**Output**

-   **Media Mix Percentages:** Breakdown of spend across programmatic, video, native, and direct advertising
-   **Total Spend Values:** Monetary spend on each advertising channel and overall total

### `Action` Find top ads published by a company

Retrieve detailed data about a company's top performing digital ads, including creative content, network placement, estimated spend, and impression metrics.

**Inputs**

-   **Company domain:** The advertiser's website domain (e.g., `apple.com`)
-   **Start date:** Beginning of the date range to analyze (YYYY-MM-DD format or natural language like "last month")
-   **End date:** End of the date range to analyze (YYYY-MM-DD format or natural language like "today")

**Output**

-   **Ad Hash:** Unique identifier for the ad
-   **Ad Info:** Size, type, creative URL, and text content
-   **Network:** The advertising network where the ad was placed
-   **Sum Ad Spend:** Estimated total spend on the ad during the specified period
-   **Sum Impressions:** Total number of times the ad was shown
-   **Preview:** Various size options to view the ad creative

### `Action` Find top ad networks used by a company

Provides detailed insights into a company's advertising strategy by identifying which ad networks they use and analyzing their ad spend distribution.

**Inputs**

-   **Company domain:** Domain name of the advertiser you want to analyze (e.g., `apple.com`)
-   **Start date:** Beginning of the date range to analyze (YYYY-MM-DD format or natural language like "last month")
-   **End date:** End of the date range to analyze (YYYY-MM-DD format or natural language like "today")
-   **Country (Optional):** Filter results to ads shown in a specific country

**Output**

-   **Network:** The advertising network identifier (e.g., `google-dv-360`, `medianet`)
-   **Ad Type:** The type of creative being served through the network
-   **Sum Ad Spend:** Estimated total ad spend on the network during the specified period

### `Action` Find top advertising geographies for a company

Analyze where a company is focusing its advertising efforts geographically and how much they're spending in different regions.

**Inputs**

-   **Company domain:** The website domain of the company you want to analyze (e.g., `apple.com`)
-   **Start date:** The beginning of the date range for analysis
    -   YYYY-MM-DD format (e.g., `2020-09-09`)
    -   Natural language (e.g., `last month`)
-   **End date:** The end of the date range for analysis
    -   YYYY-MM-DD format (e.g., `2020-12-31`)
    -   Natural language (e.g., `today`)

**Output**

-   **Geo Data Array:**
    -   Country: Two-letter country code
    -   DMA: Designated Market Area (specific market region)
    -   Sum Ad Spend: Total advertising spend in the region
    -   Sum Impressions: Total number of ad impressions in the region
-   **Country Breakdown:**
    -   Percentages: Breakdown of spend distribution by country
    -   Totals: Advertising spend and impressions by country
-   **Total Spend:** Overall advertising spend across all regions

### `Action` Find top ad publishers used by a company

Uncovers a company's primary advertising partners and reveals details about its ad spend, volume, and impressions.

**Inputs**

-   **Domain:** Company website domain or company's Adbeat advertiser URL

**Output**

-   Publisher domain/name
-   Total ad spend on publisher
-   Number of impressions
-   Number of unique ads placed
-   Publisher performance metrics

### `Action` **Find lookalike companies based on advertising data**

Find similar companies based on their advertising behavior and strategies to expand prospecting and lead generation efforts.

**Inputs**

-   **Company domain:** The website domain of the company you want to find similar advertisers for (e.g., `geico.com`)
-   **Country (Optional):** Filter results to show similar advertisers from a specific country

**Output**

-   **Similar Advertisers:** Array of company domains that have similar advertising patterns

### `Action` Find cumulative ad spend for a company

Get detailed account-level ad spend reports to understand a company's advertising investment and prioritize prospects based on their marketing budget.

**Inputs**

-   **Company domain:** Domain name of the advertiser to search (e.g., `apple.com`)
-   **Start date:** Beginning of the desired date range (YYYY-MM-DD format or natural language like "last month")
-   **End date:** End of the desired date range (YYYY-MM-DD format or natural language like "today")
-   **Country (Optional):** Filter results to ads shown in a specific country

**Output**

-   **Advertiser:** Company domain
-   **Sum Ad Spend:** Total advertising spend during the specified period

### `Action` Find top YouTube channels a company is advertising on

Uncovers which YouTube channels a company targets with its advertising to provide insights into their video marketing strategy.

**Inputs**

-   **Company domain (Required):** Company domain of advertiser to search (e.g., `apple.com`)
-   **Start date (Required):** Start date of the desired date range (Format: `YYYY-MM-DD` or natural language like `last month`)
-   **End date (Required):** End date of the desired date range (Format: `YYYY-MM-DD` or natural language like `today`)
-   **Country of search (Optional):** Search for ads shown in a specific country

**Output**

-   **Channel:** YouTube channel URL (e.g., `youtube.com/channel/UCtQMmwBJGvINGU0lZ_GrZKQ`)
-   **Publisher Name:** Name of the YouTube channel (e.g., `PharrellWilliamsVEVO`)
-   **Sum Ad Spend:** Total advertising spend on the channel in USD

### `Action` **Find companies spending the most on an ad publisher**

Get a list of companies advertising on a specific publisher's website, including their ad spend, impression data, and number of unique ads.

**Inputs**

-   **Publisher domain:** Domain of the publisher website you want to analyze (e.g., `yahoo.com`)
-   **Start date:** Beginning of the date range for analysis (YYYY-MM-DD or natural language like "last month")
-   **End date:** End of the date range for analysis (YYYY-MM-DD or natural language like "today")
-   **Country (Optional):** Filter results by specific country

**Output**

-   **Advertiser domain:** Domain of the advertising company
-   **Total ad spend:** Amount spent on advertising
-   **Total impressions:** Number of ad impressions
-   **Number of unique ads:** Count of distinct advertisements
