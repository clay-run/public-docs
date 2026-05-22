---
title: Professional Posts integration
source_url: https://university.clay.com/docs/professional-posts-integration
description: Track LinkedIn engagement and retrieve professional posts, comments,
  shares, and reactions using Clay's Professional Posts enrichments.
last_synced: 2026-05-22T20:28:00.000Z
---

# Professional Posts integration

Track LinkedIn engagement and retrieve professional posts, comments, shares, and reactions using Clay's Professional Posts enrichments.

Clay's Professional Posts integration lets you pull LinkedIn activity data directly into your tables. There are two distinct use cases:

-   **Activity enrichments** — retrieve what a specific person has recently posted, commented on, or reacted to. Input: a LinkedIn profile URL.
-   **Interaction enrichments** — retrieve who has engaged with a specific post (who commented, reacted, or shared it). Input: a LinkedIn post URL.

## Setting up the Professional Posts integration

1.  In a Clay table, click `Add enrichment` and search for `Professional Posts`.
2.  Under `Integrations`, select one of the Professional Posts options.
3.  No additional account setup is required — Clay provides access by default.

## Activity enrichments (what a person has posted or done)

These actions take a **LinkedIn profile URL** as input and return that person's recent LinkedIn activity.

### `Action` Get a person's professional posts and shares

Retrieve a person's most recent posts and shares.

**Inputs**

-   **Professional URL:** The LinkedIn profile URL of the person (e.g., `https://www.linkedin.com/in/username`).
-   **Max posts and shares** *(optional)*: Maximum number of results to return (up to 25).

### `Action` Get a person's professional post comments

Retrieve posts a person has recently commented on.

**Inputs**

-   **Professional URL:** The LinkedIn profile URL of the person.
-   **Max comments** *(optional)*: Maximum number of results to return (up to 25).

### `Action` Get a person's professional post reactions

Retrieve posts a person has recently reacted to (liked, loved, etc.).

**Inputs**

-   **Professional URL:** The LinkedIn profile URL of the person.
-   **Max reactions** *(optional)*: Maximum number of results to return (up to 25).

## Interaction enrichments (who engaged with a specific post)

These actions take a **LinkedIn post URL** as input and return the people who engaged with that post.

### `Action` Get comments on a professional post

Retrieve the top comments on a specific LinkedIn post.

**Inputs**

-   **Post URL:** The URL of the LinkedIn post (e.g., `https://www.linkedin.com/posts/clay-hq_...` or `https://www.linkedin.com/feed/update/urn:li:ugcPost:...`).
-   **Max comments** *(optional)*: Maximum number of results to return.

### `Action` Get reactions on a professional post

Retrieve the top reactions (like, love, etc.) on a specific LinkedIn post.

**Inputs**

-   **Post URL:** The URL of the LinkedIn post.
-   **Max reactions** *(optional)*: Maximum number of results to return.

### `Action` Get shares on a professional post

Retrieve the top shares of a specific LinkedIn post.

**Inputs**

-   **Post URL:** The URL of the LinkedIn post.
-   **Max shares** *(optional)*: Maximum number of results to return.

> **Note:** Share data is only available for activity-type posts (URLs containing `urn:li:activity:`). UGC posts (URLs containing `urn:li:ugcPost:`) do not return share data.

## Additional enrichments

### `Action` Enrich professional post

Enrich a LinkedIn post URL with the post's content and metadata (author, text, timestamp, engagement counts).

**Inputs**

-   **Post URL:** The URL of the LinkedIn post.

### `Source` Find professional posts

Search and discover LinkedIn posts based on keywords and filters. Use this as a table source to build a list of relevant posts.

### `Source` Get interactions with professional posts

Get comments, reactions, or shares for a list of professional posts in bulk. Use this as a source when you have a list of post URLs and want to retrieve all their interactions at once.

> **Note:** As with the action variant, share data is only available for activity-type posts, not UGC posts.

## Analyzing extracted data

Once you've retrieved posts or engagement data, you can use Clay's built-in tools to analyze it further:

-   Use **formulas** to evaluate timestamps and filter activity within a specific timeframe (e.g., the last 30 days).
-   Use **Claygent** to classify post content by type or topic (e.g., identifying video posts or product announcements).
-   Use the **[PhantomBuster integration](https://docs.clay.com/docs/phantombuster-integration-overview)** for advanced LinkedIn scraping scenarios not covered by native enrichments. Set up a LinkedIn phantom (such as the LinkedIn Activity Extractor) inside PhantomBuster, then use Clay's PhantomBuster "Pull Data" action to bring results into your table.

## Privacy limitations

LinkedIn's privacy policies restrict what data can be accessed:

-   **Inbox replies cannot be tracked.** Retrieving LinkedIn message replies requires direct account access, which Clay does not support.
-   **Company follower lists are not available.** It is not possible to retrieve a list of users who follow a specific company on LinkedIn. (Follower *counts* may be available through profile enrichments, but not the list of who follows.)
-   **Incomplete engagement data.** Some posts may return no comments or reactions despite having visible engagement on LinkedIn. This is due to LinkedIn's per-user and per-post privacy settings, which vary across accounts.
