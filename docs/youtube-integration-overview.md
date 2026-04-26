---
title: YouTube integration
source_url: https://university.clay.com/docs/youtube-integration-overview
description: Video-sharing platform offering content discovery, creation, and
  community engagement.
last_synced: 2026-04-26T01:40:57.806Z
upstream_hash: 6941e97cc8534d084c9181b1d6f7224d1cf0b1aba05ee4da027aac917e776c2c
---

# YouTube integration

Video-sharing platform offering content discovery, creation, and community engagement.

## **YouTube Overview**

The YouTube integration in Clay enables users to extract video transcripts directly from a YouTube URL, supporting multilingual and structured text analysis

## **Available Actions with the YouTube Integration**

### **`Action` Enrich YouTube Video**

### Input fields

-   **YouTube video URL**: The URL of the YouTube video to be processed (required for setup).
-   **Country of search**: The geographic region to focus the search on (optional). Defaults to “United States” if left blank.
-   **Language of search**: The preferred language for search results (optional).

### Output fields

-   **Video**: Contains metadata and details about the video, including title, description, unique video ID, category, keywords, author, likes, views, available formats, and a thumbnail URL.
-   **Channel**: Represents details about the channel associated with the video, such as name, unique channel ID, URL, thumbnail image, and subscriber count.
-   **Pagination**: Provides information to navigate through paginated results, such as the current page, total pages, and next/previous page links.
-   **Merchant Items**: Lists merchandise items related to the video or channel, including product names, descriptions, pricing, and purchase links.
-   **Search Parameters**: Displays the parameters used to filter or refine the search, such as keywords, search engine type, selected region, preferred language, and video ID.
-   **Recommended Videos**: Shows a recommended video based on the current content, including details such as title, URL, and a thumbnail image.
-   **Available Transcripts Languages**: Lists the languages available for the video transcripts, allowing you to select or take specific actions for each language.

### **`Action` Extract YouTube Video Transcript**

Use this action to retrieve the transcript of a YouTube video for analysis, research, or content repurposing.

### **Input fields**

-   **YouTube video URL**: Enter or select the YouTube URL of the video from which you want to extract the transcript.
-   **Transcript Structure** (Optional): Choose the desired format for the transcript (structured/unstructured).
-   **Transcript Language** (Optional): Specify the language for the transcript if available.
-   **Transcript Type** (Optional): Select the type of transcript, such as auto-generated or human-generated, if applicable.
