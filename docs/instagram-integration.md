---
title: Instagram integration
description: Easily gather Instagram data to use in your Clay tables.
last_synced: 2026-04-26T01:40:11.309Z
---

# Instagram integration

Easily gather Instagram data to use in your Clay tables.

Instagram is a powerful social media platform.With this integration, you can automatically find a company's Instagram URL using their name or domain.

## **Creating a table with Instagram (Find account followers)**

Create table of followers from any public Instagram account.

1.  In a workbook, click `+ Add` at the bottom.
2.  Search for `Instagram` and select from the results.
3.  Add your own account or use the provided Clay-managed account.
4.  Enter inputs for:**‍**
    -   **Handle**
    -   **Max number of results (Optional): Between 1-2500**

### `Action` Find company profile

1.  While in a Clay table, click `Add enrichment` and search for Instagram.
2.  Under `Integrations`, select `Find company profile`.
3.  Enter inputs for:**‍**
    -   **Company Domain (Optional)**
    -   **Company Name (Optional)**
4.  Run settings
    -   **Auto-update**
    -   **Only run if:** The enrichment will only run if conditions are met. ([Learn more about conditional formulas here!](https://www.clay.com/university/lesson/ai-formulas-conditional-runs-clay-101))

**Tip:** The **Raw** output includes a **Displayed subtext** field that shows the account's approximate follower count as it appears in Google search results (for example, "10.2M+ followers"). You can also visit a discovered Instagram profile URL with [Claygent](claygent-builder.md) to retrieve the account's current follower count directly from the page.

## Finding a company's Facebook page

The Instagram enrichment does not return Facebook page URLs. To find a company's Facebook page URL, use [Claygent](claygent-builder.md) with web search enabled. Prompt it to locate the Facebook page for a company by name or domain — for example:

> "Find the official Facebook page URL for {Company Name} at {Company Domain}."

**Note:** Facebook page follower counts are not returned when Claygent visits a Facebook page. For historical Facebook likes data, see the [Aviato integration](aviato-integration.md).
