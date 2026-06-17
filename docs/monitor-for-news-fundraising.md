---
title: Monitor for news & fundraising signals
source_url: https://university.clay.com/docs/monitor-for-news-fundraising
description: Monitor companies for news and fundraising events and track these
  as signals.
last_synced: 2026-04-26T01:40:20.000Z
---

# Monitor for news & fundraising signals

Monitor companies for news and fundraising events and track these as signals.

Clay's **News & Fundraising Signals** let you monitor companies for news coverage and funding activity in real time. Once configured, the signal watches your list of companies and surfaces relevant events as they happen.

## Setting up a signal

Follow these steps to set up News & Fundraising Signals in your table:

1.  In a Clay table, click `Add column`.
2.  Under the `Signals` section, select the `News & Fundraising Signals`.
3.  Select `Topic Filter`: Select what kind of news to look for (e.g., funding, hiring, etc.).
4.  Select `Signal Input Field`: Choose the column whose values will be used as inputs to look for news (typically a company domain).
5.  Optionally, `Add Domain Exclusions`: Add domains to exclude from signal detection.
6.  Optionally, `Add sample results`.
    -   This lets you preview how the data will appear after any changes actually happen.
7.  Click `Save and run X rows` to complete setup.

## FAQs

### Why is my signal returning articles where my target company isn't the main subject?

This is expected behavior. When a News & Fundraising signal is configured with a company domain (e.g., `santander.com`), the signal fires any time that domain appears among the article's associated companies — not only when your company is the **primary subject** of the article.

For example, if your company is mentioned as a lender, investor, or partner in an article about a different company, that article will still surface in your results. The topic filter (e.g., "Fundraising") only controls **which types of news events** to watch for — it does not restrict results to articles where your target company is the lead subject.

Article results include a `newsData.domains` array containing all company domains associated with the article. The first entry, `newsData.domains[0]`, is typically the article's primary company.

### How do I get only articles where my target company is the primary subject?

Add a filter at the **results table level** using one of these approaches:

-   **Quick option:** Filter where `newsData.domains[0]` matches your target company's domain. Since `domains[0]` is usually the article's primary company, this narrows results to articles primarily about your target.
-   **More accurate option:** Add an AI column with a prompt such as "Is this article primarily about [Company Name]? Answer yes or no." Then filter the table to only pass through "yes" rows before alerting or acting on the results.

The AI column approach gives the most reliable results when precision matters.
