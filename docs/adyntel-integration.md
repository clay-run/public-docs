---
title: Adyntel integration
source_url: https://university.clay.com/docs/adyntel-integration
description: Analyze ad content, campaign duration, media types, and ad counts
last_synced: 2026-04-27T18:09:11.856Z
upstream_hash: 13503e8eb2706f3940369f32a5863a7bb5f376038edfa6fb3540372001da6bb4
---

# Adyntel integration

Analyze ad content, campaign duration, media types, and ad counts

Adyntel Integration allows users to gather comprehensive advertising data from major platforms like Meta, LinkedIn, and Google, helping businesses understand their advertising landscape and optimize strategies.

With this integration, you can analyze ad content, campaign duration, media types, and ad counts to personalize marketing efforts and enhance lead generation campaigns.

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
