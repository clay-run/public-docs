---
title: Reddit integration
source_url: https://university.clay.com/docs/reddit-integration
description: Monitor Reddit mentions and comments.
last_synced: 2026-04-26T01:40:31.604Z
upstream_hash: 3e6338fd0d2a147eea8f4c6d11bd29701cb6893a849f2d6d2f5b4936f65573d1
---

# Reddit integration

Monitor Reddit mentions and comments.

Reddit is a social media platform for content sharing and discussion.

This integration allows you to find Reddit mentions and comments.

## **Creating a table with Reddit**

1.  In a workbook, click `+ Add` at the bottom.
2.  Search for `Reddit` and select from the results.
3.  In the modal, you will be asked to `Select Reddit account`.
    1.  If you haven't already connected your Reddit account, click `+ Add account` and go through authentication.

### `Source` Find mentions on Reddit

Find posts on Reddit that mention specific keywords like your company, products, etc. Note that this source may take longer to return results due to the large amount of data being processed.

Inputs:

-   **Keywords:** Max 8 keywords
-   **Keyword logic (Optional):** Specify whether searches should match all keywords or any of them.
-   **Subreddits:** Limit searches to specific Subreddits.
-   **Time period (Optional)**
-   **Max number of results (Optional)**

## **Enriching data with Reddit**

1.  While in a Clay table, click `Add enrichment` and search for `Reddit`.
2.  Under `Integrations`, select one of the Reddit options.
3.  In the modal, you will be asked to `Select Reddit account`.
    1.  If you haven't already connected your Reddit account, click `+ Add account` and go through authentication.

### `Action` Find post comments

Get comments from a specific Reddit link.

**Inputs**

-   **Post ID**
-   **Subreddit**
-   **Max number of results (Optional)**

### **Run settings**

-   **Auto-update**
-   **Only run if:** The enrichment will only run if conditions are met. ([Learn more about conditional formulas here!](https://www.clay.com/university/lesson/ai-formulas-conditional-runs-clay-101))
