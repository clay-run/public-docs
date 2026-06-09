---
title: Modash integration
description: Discover and analyze social media creators.
last_synced: 2026-05-11T17:47:40.000Z
---

# Modash integration

Discover and analyze social media creators.

Modash provides real-time creator data and analytics across Instagram, TikTok, and YouTube. With this integration, you can discover influencers, analyze their audience and content performance, and gather contact information — all within Clay.

## Creating a table with Modash

1.  In a workbook, click `+ Add` at the bottom.
2.  Search for `Modash` and select from the results.
3.  In the modal, you will be asked to `Select Modash account`.
    -   If you haven't already connected your Modash account, click `+ Add account` and go through authentication. Otherwise, use the Clay-provided key.

### `Source` Find Instagram creators (keyword search)

Find Instagram creators by keyword.

**Inputs**

-   **Search query:** Keyword or phrase (e.g., "vegan food NYC", "fitness coach").
-   **Number of results:** How many creators to return.

### `Source` Find Instagram creators (AI search)

Find Instagram creators using natural language descriptions of the content, aesthetic, or audience you're looking for.

**Inputs**

-   **Natural language query:** Describe your ideal creator (e.g., "woman with curly hair lifting weights").
-   **Filters (Optional):** Follower count range, location, gender, engagement rate, account type, language, has email, last posted within X days.
-   **Number of results:** Max 1,500 per search.

**Limitation:** Instagram AI Search only supports creators with **\>10,000 followers**.

**Note:** Profiles are refreshed on a ~4-week cadence. Follower counts and engagement rates may lag real-time by up to 4 weeks.

### `Source` Find TikTok creators (keyword search)

Find TikTok creators by keyword.

**Inputs**

-   **Search query:** Keyword or phrase (e.g., "makeup tutorial", "coding tips").
-   **Number of results:** How many creators to return.

### `Source` Find TikTok creators (AI search)

Find TikTok creators using natural language descriptions.

**Inputs**

-   **Natural language query:** Describe your ideal creator (max 1,024 characters or 64 words).
-   **Filters (Optional):** Same as Instagram AI Search (minus content type, since TikTok is video-only).
-   **Number of results:** Max 1,500 per search.

## Enriching data with Modash

1.  While in a Clay table, click `Add enrichment` and search for `Modash`.
2.  Under `Integrations`, select one of the Modash options.
3.  In the modal, you will be asked to `Select Modash account`.
    -   If you have your own account, click `+ Add account` and go through authentication. Otherwise, use the Clay-provided key.

### `Action` Get Instagram user info

Enrich an Instagram profile with follower count, engagement rate, bio, recent posts, and audience demographics.

**Inputs**

-   **Instagram handle or profile URL:** e.g., `@username` or `https://instagram.com/username`

### `Action` Get Instagram user feed

Pull the most recent posts from an Instagram profile, including captions, likes, comments, and media URLs.

**Inputs**

-   **Instagram handle or profile URL**

### `Action` Get Instagram media info

Get detailed stats for a specific Instagram post or reel, including likes, comments, views, and engagement rate.

**Inputs**

-   **Instagram post URL or shortcode:** e.g., `https://www.instagram.com/p/ABC123/` or `ABC123`

### `Action` Get Instagram media comments

Extract all comments from an Instagram post or reel.

**Inputs**

-   **Instagram post URL or shortcode**

### `Action` Get TikTok user info

Enrich a TikTok profile with follower count, video count, likes, bio, and audience demographics.

**Inputs**

-   **TikTok handle, profile URL, or user ID**

### `Action` Get TikTok media info

Get detailed stats for a specific TikTok video, including views, likes, comments, shares, and play duration.

**Inputs**

-   **TikTok video URL or video ID**

### `Action` Get TikTok comments

Extract all comments from a TikTok video.

**Inputs**

-   **TikTok video URL or video ID**

### `Action` Get YouTube channel info

Enrich a YouTube channel with subscriber count, video count, total views, and recent uploads.

**Inputs**

-   **YouTube channel URL or channel ID**

### `Action` Get YouTube uploaded videos

Pull the most recent videos from a YouTube channel, including titles, views, likes, and publish dates.

**Inputs**

-   **YouTube channel URL or channel ID**

### `Action` Get YouTube video info

Get detailed stats for a specific YouTube video, including views, likes, comments, and engagement rate.

**Inputs**

-   **YouTube video URL or video ID**

### `Action` Get YouTube video subtitles

Extract the full transcript/subtitles from a YouTube video.

**Inputs**

-   **YouTube video URL or video ID**

### Run settings

-   **Auto-update:** Re-run enrichment when source data changes.
-   **Only run if:** The enrichment will only run if conditions are met. [Learn more about conditional formulas](https://www.clay.com/university/lesson/ai-formulas-conditional-runs-clay-101).

## Best practices

### For AI Search

-   **Write descriptive queries:** Instead of "fitness", try "female fitness coaches who post workout routines for beginners".
-   **Use filters strategically:** Narrow by follower count, location, or engagement rate to get more relevant results.
-   **Keep pageSize constant:** When requesting large result sets (>50), Modash paginates automatically. Don't change the page size mid-search or you may get duplicate/missed results.

### For enrichments

-   **Handle URLs flexibly:** Clay automatically parses handles from full URLs, so you can pass `https://instagram.com/username` instead of just `@username`.
-   **Use conditional runs:** Save credits by only enriching profiles that meet certain criteria (e.g., follower count > 10K).
-   **Combine with AI formulas:** After pulling comments or transcripts, use Clay's AI formulas to analyze sentiment, extract themes, or summarize content.
