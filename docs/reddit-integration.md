---
title: Reddit integration
description: Monitor Reddit mentions and comments.
last_synced: 2026-04-26T01:40:31.604Z
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

-   **Subreddits (required):** The subreddits to search. Accepts a subreddit name (e.g., `sales`), an `r/` prefix (e.g., `r/sales`), or a full URL (e.g., `https://www.reddit.com/r/sales/`). At least one subreddit must be provided or the source will not run.
-   **Keywords (required):** The search terms to look for. The combined query must be under 512 characters.
-   **Keyword logic (Optional):** Whether posts must match any keyword (OR) or all keywords (AND). Defaults to OR (any keyword).
-   **Time period (Optional):** Limit results to posts from a specific window — Hour, Day, Week, Month, or Year. Defaults to all time.
-   **Max number of results (Optional)**

**How keyword search works**

Keywords are search terms sent to Reddit's search engine — they are not exact-match filters. Reddit returns posts that are relevant to your keywords, which may include posts whose title or body do not contain your exact keyword verbatim.

The **Keywords** output column shows which of your search terms appeared literally in the returned post's title or body. If Reddit returns a post where none of your keywords appear verbatim, the **Keywords** column shows **Post** — indicating the result was returned by Reddit's relevance search without an exact keyword match in the post text.

**Outputs**

-   **Post ID**
-   **Title**
-   **Body Text**
-   **Author**
-   **Subreddit**
-   **Created At** — Unix timestamp in milliseconds
-   **Created At Date**
-   **URL**
-   **Number of Comments**
-   **Score**
-   **Keywords** — Which of your search terms appeared verbatim in the post's title or body. Shows **Post** if none of your keywords matched literally.

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
