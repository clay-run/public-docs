---
title: Professional Posts integration
source_url: https://university.clay.com/docs/professional-posts-integration
description: Find, enrich, and analyze professional posts from LinkedIn company pages and individual profiles.
last_synced: 2026-05-20T15:30:00.000Z
---

# Professional Posts integration

Find, enrich, and analyze professional posts from LinkedIn company pages and individual profiles.

The Professional Posts integration lets you pull LinkedIn posts into Clay for social listening, lead qualification, and engagement workflows. No API key is required — Clay manages the connection.

## Getting posts from a company

To pull posts published by a specific company, use the **Find professional posts** source action.

1.  In a workbook, click `+ Add` at the bottom.
2.  Search for `Find professional posts` and select it under **Sources**.
3.  Under **Companies filter**, select **Posted by companies**.
4.  In the **Company domains or profile URLs** field, enter the company's domain (e.g. `clay.com`) or its LinkedIn company page URL (e.g. `linkedin.com/company/grow-with-clay`). You can enter up to 5 values.
5.  Optionally add **Keywords** (up to 5) to filter posts by topic.
6.  Set a **Time frame** — **Last 24 hours** or **Last week** (default).
7.  Set **Max number of results** (default: 100, max: 1,000).
8.  Click **Continue** to preview results, then **Import** to add them as rows.

**Note:** The **Companies filter** also supports **Mentions companies** (posts that tag the company) and **Posted by companies' employees** (posts from people who work at the company).

## Getting posts from a person

To pull posts from a specific person's LinkedIn profile, add the **Get a person's professional posts and shares** enrichment to an existing table.

1.  In a Clay table, click `Add enrichment` and search for `Get a person's professional posts and shares`.
2.  Under **Integrations**, select the action.
3.  Map **Professional URL** to the column containing the person's LinkedIn profile URL (e.g. `https://www.linkedin.com/in/username`).
4.  Optionally set **Max posts and shares** (default: 10, max: 25).
5.  Select the data fields to add as columns and run.

## Other actions

The integration includes several additional actions for working with post data:

| Action | What it does |
| --- | --- |
| **Get a person's professional post comments** | Comments a person has left on posts |
| **Get a person's professional post reactions** | Reactions a person has given to posts |
| **Enrich professional post** | Adds metadata (engagement stats, author details) to a specific post |
| **Get comments on a professional post** | Comments received on a given post |
| **Get reactions on a professional post** | Reactions received on a given post |
| **Get shares on a professional post** | Shares for a given post |
| **Get interactions with professional posts** | Source action to build a table of people who interacted with specific posts |

## Searching posts by keyword

To discover posts across LinkedIn by topic — without filtering to a specific company or person — use **Find professional posts** and leave the Companies filter and People filter blank. Add one or more **Keywords** to find posts containing those terms.

## Common questions

### Why can't I find "Find Recent Posts by User or Company with Companies, People, Jobs"?

That enrichment name does not exist in Clay. To get posts from a company, use **Find professional posts** (described above). To get posts from a person's profile, use **Get a person's professional posts and shares**.

### Can I get all posts from a company page going back months?

The **Find professional posts** source returns posts from the **last week** by default, or **last 24 hours** if selected. Posts older than one week are not available through this integration.

### Do I need my own API key?

No. Clay manages the connection — no external account or API key required.
