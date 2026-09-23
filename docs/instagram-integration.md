---
title: Instagram integration
description: Easily gather Instagram data to use in your Clay tables.
last_synced: 2026-04-26T01:40:11.309Z
---

# Instagram integration

Easily gather Instagram data to use in your Clay tables.

## **Creating a table with Instagram (Find account followers)**

Create table of followers from any public Instagram account.

1.  In a workbook, click `+ Add` at the bottom.
2.  Search for `Instagram` and select from the results.
3.  Add your own account or use the provided Clay-managed account.
4.  Enter inputs for:**‍**
    -   **Handle**
    -   **Max number of results (Optional): Between 1-2500**

## Finding a person's Instagram or Facebook profile URL

To look up an individual person's Instagram or Facebook profile URL using information you already have (such as their email address, LinkedIn URL, or name):

-   **From a creator email** — use the Influencer Club **Find social profiles by creator email** enrichment. Enter the creator's email address to get their Instagram, TikTok, YouTube, Twitch, OnlyFans, Linktree, and Patreon profile URLs. See [Influencer Club integration](influencer-club-integration-overview.md) for setup details.
-   **Instagram (Person) waterfall** — uses Clearbit to return a person's Instagram profile URL from person identifiers such as name or work email. In your table, click **Tools → Enrich**, search for `Instagram (Person)`, map your identifier columns, and click **Save**.
-   **Facebook (Person) waterfall** — cascades across People Data Labs, Clearbit, and Swordfish to return a person's Facebook profile URL from person identifiers. In your table, click **Tools → Enrich**, search for `Facebook (Person)`, map your identifier columns, and click **Save**.
-   **Claygent** — add a Claygent column and prompt it to search the web for the person's Instagram or Facebook profile using their email or LinkedIn URL as inputs. See [Claygent](claygent-builder.md) for setup details.

## Finding a company's Facebook page

To find a company's Facebook page URL, use [Claygent](claygent-builder.md) with web search enabled. Prompt it to locate the Facebook page for a company by name or domain — for example:

> "Find the official Facebook page URL for {Company Name} at {Company Domain}."

**Note:** Facebook page follower counts are not returned when Claygent visits a Facebook page. For historical Facebook likes data, see the [Aviato integration](aviato-integration.md).
