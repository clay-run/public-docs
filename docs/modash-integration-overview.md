---
title: Modash integration
source_url: https://university.clay.com/docs/modash-integration-overview
description: Discover and analyze social media creators.
last_synced: 2026-04-26T01:40:23.430Z
upstream_hash: ae0f55eb723db06293982e64b85f594eca965068efc9132e671da0fe4d2a32b5
---

# Modash integration

Discover and analyze social media creators.

Modash is an influencer marketing platform for discovering and analyzing social media creators.

With this integration, you can utilize Modash's creator data and analytics capabilities directly within your Clay table.

## Creating a table with Modash

1.  In your workspace, click `Create new` → `Table...`.
2.  Search for `Modash` and select `Find social media influencers with Modash`.
3.  Enter inputs for:
    1.  **Social platform:** Select Instagram, TikTok, or YouTube.
    2.  **Bio key phrase (Optional):** Find influencers who mention a specific phrase in their bio.
    3.  **Mentions (@accounts, #hashtags, keywords) (Optional):** Find influencers using specific mentions in their captions.
    4.  **Lookalike influencer (Optional)**: Find creators similar to your ideal influencer.
    5.  **Minimum followers:** Set the minimum follower count.
    6.  **Maximum followers (Optional):** Set an upper limit on follower count.
    7.  **Language (Optional):** Filter by the creator's primary content language.
    8.  **Audience location (Optional):** Filter by where the creator's audience is based
    9.  **Audience age (Optional):** Target influencers whose audience has at least 30% of followers within each of the selected age ranges.
    10.  **Audience gender (Optional):** Target influencers whose audience is predominantly (>50%) of the selected gender.
    11.  **Maximum number of results:** The maximum number of influencer search results to return. 1 credit per influencer & must be between 1 and 1500.
    12.  **Advanced filters (Optional):** Additional filtering options (note: may reduce the number of results).

## **Enriching data with Modash**

1.  While in a Clay table, click `Add enrichment` and search for `Modash`.
2.  Under `Integrations`, select one of the Modash options.
3.  In the modal, you will be asked to `Select Modash account`.
    -   If you have your own account, click `+ Add account` and go through authentication. Otherwise, use the Clay provided key.

### `Action` Enrich influencer details

Use this action to enrich social media influencers data with Modash.

**Inputs**

-   **Social platform**
-   **Username**

### `Action` Find audience overlap between two creators

Use this action to enrich social media influencers data with Modash.

**Inputs**

-   **Social platform**
-   **Source influencer:** One of the creators you want to compare.
-   **Target influencer:** One of the creators you want to compare.

### `Action` Find social profiles by creator email

Use this action to find a list of social profiles matching a particular email address.

**Inputs**

-   **Email address**

### `Action` Influencer contacts

Use this action to find the relevant contacts of a social media influencer.

**Inputs**

-   **Social platform**
-   **Username**

### `Action` Find creator personal email

Use this action to find creator email address from Instagram, TikTok, or YouTube profile.

**Inputs**

-   **Social platform**
-   **Username**

### `Action` Find lookalike creator profiles

**Find up to 40 related accounts** for a social media profile, including similar-audience profiles or influencer lookalikes.

**Inputs**

-   **Social platform**
-   **Username**

### **Run settings**

-   **Auto-update**
-   **Only run if:** The enrichment will only run if conditions are met. ([Learn more about conditional formulas here!](https://www.clay.com/university/lesson/ai-formulas-conditional-runs-clay-101))
