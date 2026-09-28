---
title: Adyntel integration
description: Import ads that match a keyword, or look up the ads a company is currently running.
last_synced: 2026-09-28T16:43:58.017Z
---

# Adyntel integration

Import ads that match a keyword, or look up the ads a company is currently running.

Adyntel is an ad intelligence tool for finding and analyzing the ads that companies run on major advertising platforms. With this integration, you can build a table of ads matching a keyword, or take companies you already have and pull back the ad copy, creative, landing pages, and campaign dates behind their live campaigns.

## **Creating a table with Adyntel**

1.  In a workbook, click `+ Add` at the bottom.
2.  Search for `Adyntel` and select from the results.
3.  In the modal, you will be asked to `Select Adyntel account`.
    -   If you have your own account, click `+ Add account` and go through authentication. Otherwise, use the Clay provided key.

**Note:** The keyword ad-search sources import one row per ad and are scheduled to re-run once a day by default. Each ad is tracked by its own ID, so a re-run only adds ads Clay hasn't imported before — you won't get duplicate rows for ads that are still running. To import once and stop, set `Run this source` to `Manually` in the source's `Run settings`.

### `Source` Find Meta ads by keyword with Adyntel

Search the Meta ad library for ads matching a keyword and import them along with the companies running them.

**Inputs**

-   **Keywords:** One or more keywords to search the ad library for, for example `webinar` or `ai sdr`. Each keyword runs its own search, and matching ads are combined and deduplicated. You can include up to 20 keywords per import.
-   **Country (optional):** Limit results to ads shown in one country. If this is not added, the search covers all countries.
-   **Limit (optional):** The maximum number of ads to import. Defaults to 100, and the maximum is 1,000.

### `Source` Find LinkedIn ads by keyword with Adyntel

Search for LinkedIn ads matching a keyword and import them along with the companies running them, optionally filtered by country or date range.

**Inputs**

-   **Keywords:** One or more keywords to search the ad library for, for example `webinar` or `ai sdr`. Each keyword runs its own search, and matching ads are combined and deduplicated. You can include up to 20 keywords per import.
-   **Country (optional):** Limit results to ads shown in one country. If this is not added, the search covers all countries.
-   **Date range (optional):** Filter returned ads by the date they ran — `Last 30 days`, `Current month`, `Current year`, `Last year`, or `Custom date range`. If this is not added, the search covers ads from any date.
-   **Start date (optional):** The start of the custom date range. Only used when `Date range` is set to `Custom date range`.
-   **End date (optional):** The end of the custom date range, which has to be before today. A custom range can span up to 364 days. Only used when `Date range` is set to `Custom date range`.
-   **Limit (optional):** The maximum number of ads to import. Defaults to 100, and the maximum is 1,000.

## **Enriching data with Adyntel**

1.  While in a Clay table, click `Add enrichment` and search for `Adyntel`.
2.  Under `Integrations`, select one of the Adyntel options.
    -   If you have your own account, click `+ Add account` and go through authentication. Otherwise, use the Clay provided key.

### `Action` Get Meta ads

View Facebook and Instagram ads that a company is currently running, including ad copy, images, advertiser details, and landing pages.

**Inputs**

-   **Facebook page URL (Optional):** The company's Facebook page URL (must start with `https://`)
-   **Company domain (Optional):** Company website domain (format: `company.com` without `https://` or `www`)
-   **Media type (Optional):** Filter results by media type
    -   Image
    -   Meme
    -   Image and Meme
    -   Video
    -   All (default)
-   **Active status (Optional):** Filter by ad status
    -   Active (default)
    -   Inactive
    -   All (active and inactive)
-   **Country (Optional):** Filter results by specific country

**Output**

-   **Total number of ads being run**
-   **Landing pages associated with the ads**
-   **Up to 10 specific ad details including:**
    -   Ad copy
    -   Ad images
    -   Advertiser name
    -   Ad URL
    -   Ad spend (when available)
    -   Creation date
    -   Platform (Facebook/Instagram)

### `Action` Get LinkedIn ads

Uncover and analyze LinkedIn ad campaigns run by companies based on their website domains or LinkedIn page IDs.

**Inputs**

-   **LinkedIn company org ID (Optional):** The LinkedIn company org ID to find ads for (e.g., `15564` from `https://www.linkedin.com/company/15564`). One of LinkedIn company org ID or company domain is required.
-   **Company domain (Optional):** The company domain to find ads for (e.g., `clay.com`). One of LinkedIn page ID or company domain is required. **_Note:_** _Using the LinkedIn page ID is more accurate than domain._

**Output**

-   **Total ads:** The total number of ads found for the company
-   **Ads:** An array of up to 10 ad details including:
    -   Creative type
    -   Ad ID
    -   Type
    -   Advertiser name and logo
    -   Ad copy/commentary
    -   Ad image
    -   Headline
    -   View details link (URL to view the ad on LinkedIn)

### `Action` Get Google ads

Retrieve and analyze detailed data on companies' Google Ads campaigns to understand their advertising strategies and campaign effectiveness.

**Inputs**

-   **Company domain:** The company domain to match (e.g., `clay.com`)
-   **Media type (Optional):** Filter results for a specific type of media:
    -   Text
    -   Image
    -   Video
    -   All (Default)

**Output**

-   **Total ad count:** Number of ads found
-   **Continuation token:** Token for pagination
-   **Country code:** Where ads were seen
-   **Detailed information for up to 10 ads:**
    -   Advertiser ID and name
    -   Creative ID
    -   Ad format (Image, Text, Video)
    -   Original ad URL
    -   Start date
    -   Last seen date
    -   Ad content variants including:
        -   Content
        -   Dimensions (height/width)
        -   Media URLs

### **Run settings**

-   **Auto-update**
-   **Only run if:** The enrichment will only run if conditions are met. ([Learn more about conditional formulas here!](https://www.clay.com/university/lesson/ai-formulas-conditional-runs-clay-101))
