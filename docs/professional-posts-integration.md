---
title: Professional Posts integration
source_url: https://university.clay.com/docs/professional-posts-integration
description: Track LinkedIn engagement and retrieve professional posts, comments,
  shares, and reactions using Clay's Professional Posts enrichments.
last_synced: 2026-06-01T00:00:00.000Z
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

## Getting posts for specific people in your people table

If you already have a people table with LinkedIn URLs, the simplest path is to add the enrichment directly to that table:

1.  In your people table, click `Add enrichment` and search for **Get a person's professional posts and shares**.
2.  Map the **Professional URL** field to the column containing each person's LinkedIn URL.
3.  Optionally set **Max posts and shares** (up to 25).
4.  Run the enrichment — results appear as a new column in the same table.

**Optional: Expand posts to rows.** If you want each post to be its own row (rather than all posts for one person in a single cell), right-click the posts output column header and select **Expand to rows**. This creates one row per post, making it easier to work with downstream.

## Getting posts for specific people in a new table

If you want posts in a separate table — for example, to keep your people table focused — use [Send Table Data](send-table-data.md) to pass people from your existing table into a new one:

1.  Create a new table in your workbook (click `+ Add` at the bottom) to hold your posts results.
2.  In your people table, go to `Exports → Send table data`. Select the new table as the destination, choose `Send row`, and map the LinkedIn URL column. See [Send Table Data](send-table-data.md) for full configuration details.
3.  In the new table, click `Add enrichment`, search for **Get a person's professional posts and shares**, and map **Professional URL** to the LinkedIn URL column.
4.  Run the enrichment.

## Analyzing extracted data

Once you've retrieved posts or engagement data, you can use Clay's built-in tools to analyze it further:

-   Use **formulas** to evaluate timestamps and filter activity within a specific timeframe (e.g., the last 30 days).
-   Use **Claygent** to classify post content by type or topic (e.g., identifying video posts or product announcements).
-   Use the **[PhantomBuster integration](phantombuster-integration-overview.md)** for advanced LinkedIn scraping scenarios not covered by native enrichments. Set up a LinkedIn phantom (such as the LinkedIn Activity Extractor) inside PhantomBuster, then use Clay's PhantomBuster "Pull Data" action to bring results into your table.

## Privacy limitations

LinkedIn's privacy policies restrict what data can be accessed:

-   **Inbox replies cannot be tracked.** Retrieving LinkedIn message replies requires direct account access, which Clay does not support.
-   **Company follower lists are not available.** It is not possible to retrieve a list of users who follow a specific company on LinkedIn. (Follower *counts* may be available through profile enrichments, but not the list of who follows.)
-   **Incomplete engagement data.** Some posts may return no comments or reactions despite having visible engagement on LinkedIn. This is due to LinkedIn's per-user and per-post privacy settings, which vary across accounts.

## Common questions

### Which enrichment should I use to get posts from specific people?

Use **Get a person's professional posts and shares**. This enrichment takes a person's LinkedIn profile URL and returns their recent posts and shares. You can add it directly to any people table that has a LinkedIn URL column.

**Find professional posts** is different — it's a keyword-based search that finds posts across LinkedIn matching your filters (company, topic, timeframe). It does not search by specific person.

### Why can't I find "Find professional posts" under "Add enrichment"?

**Find professional posts** is a **source**, not an enrichment. To use it, click `+ Add` at the bottom of your workbook to create a new table, then search for "Find professional posts" — it will appear under **Sources**. Alternatively, click `Tools → Import` in an existing table.

Enrichments (found via `Add enrichment`) work on each row individually and require a specific input per row, such as a LinkedIn URL. Sources populate an entire table with matching results.

### Can I get posts from employees of a specific company without knowing their LinkedIn URLs?

Yes — use the **Find professional posts** source. Set the Companies filter to **Posted by companies' employees** and enter the company domain or LinkedIn company URL. This returns recent posts from any employees at that company matching your keyword and timeframe filters, without needing individual LinkedIn URLs.

If you want posts only from specific individuals (not all employees), use **Get a person's professional posts and shares** with their LinkedIn URLs instead.
