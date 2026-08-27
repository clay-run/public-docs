---
title: Monitor for news & fundraising
description: Set up signals for significant events at monitored companies, like
  fundraising events.
last_synced: 2026-04-26T01:40:23.757Z
---

# Monitor for news & fundraising

Set up signals for significant events at monitored companies, like fundraising events.

News & Fundraising Signals alert you to significant events at monitored companies, helping you spot timely engagement opportunities.

-   Track potential customers' growth, funding rounds, and key announcements.
-   Stay informed about client developments to anticipate their needs.
-   Keep company intelligence up-to-date through automated news monitoring.

**_Cost:_** _Each result consumes 1 action plus 6 data credits._

## Monitoring news & fundraising

Follow these steps to set up News & Fundraising Signals in your table:

1.  Click `Tools`, then select `Monitor for news & fundraising`.
2.  Select the table with companies you want to monitor.
3.  Choose the column containing company domains and select your preferred news topics.
4.  Set the Signal's frequency.
5.  Add enrichments for extra data if needed.
6.  Optionally, `Add sample results`.
    -   This lets you preview how the data will appear after any changes actually happen.
7.  Click `Save and run X rows` to complete setup.

**Note:** Signal events are written as new rows to a newly-created output table — the existing table you select is used as the source input (the people or companies to monitor), and a fresh output table is created to capture matching events. The existing table is not written to.

## FAQs

### Why did my signal miss a recent funding announcement even after re-running?

The **Earliest publish date** setting in a News & Fundraising signal controls which articles the signal considers — it only returns articles published on or after that date.

When **Auto-advance after each run** is switched on (the default), the signal automatically moves the **Earliest publish date** forward to the current date after every run. This means:

-   Each re-run starts from the date of the previous run, so the signal never looks back at articles published before its last execution.
-   If a funding round was announced yesterday but your signal already ran (and auto-advanced) today, re-running the signal will still skip that announcement — the date window has already moved past it.

**To capture an announcement your signal missed:**

1.  Click the signal column header (the `📡` icon).
2.  Click **Edit signal**.
3.  In the **Filters** section, manually set **Earliest publish date** to a date *before* the announcement was published (for example, two days ago).
4.  Click **Save and re-run**.

After that run, Clay will advance the date again automatically if **Auto-advance after each run** is still enabled. If you prefer to look back a fixed window on every run, turn off **Auto-advance after each run** and manage the date manually.

### Why is my News signal returning fewer results than expected?

Check the **Max news results per domain** and **Max news results total** settings in the **News filters** section of your signal.

**Max news results per domain** — limits how many articles are returned for each company domain per run. When this is set to 1, the signal returns at most one article per company, even if multiple relevant articles were published during the search window. Increase this number to get more articles per company, or leave the field blank to remove the per-domain cap.

**Max news results total** — caps the total number of articles returned across all company domains in a single run. When left blank, the signal defaults to a maximum of 50 articles per run. Enter a higher number to allow more total results.

To review or update either setting:

1.  Click the signal column header (the `📡` icon).
2.  Click **Edit signal**.
3.  In the **News filters** section, review the values for **Max news results per domain** and **Max news results total**.
4.  Adjust the values and click **Save and re-run**.

### Why is my signal returning articles where my target company isn't the main subject?

This is expected behavior. When a News & Fundraising signal is configured with a company domain (e.g., `santander.com`), the signal fires any time that domain appears among the article's associated companies — not only when your company is the **primary subject** of the article.

For example, if your company is mentioned as a lender, investor, or partner in an article about a different company, that article will still surface in your results. The topic filter (e.g., "Fundraising") only controls **which types of news events** to watch for — it does not restrict results to articles where your target company is the lead subject.

Article results include a `newsData.domains` array containing all company domains associated with the article. The first entry, `newsData.domains[0]`, is typically the article's primary company.

### How do I get only articles where my target company is the primary subject?

Add a filter at the **results table level** using one of these approaches:

-   **Quick option:** Filter where `newsData.domains[0]` matches your target company's domain. Since `domains[0]` is usually the article's primary company, this narrows results to articles primarily about your target.
-   **More accurate option:** Add an AI column with a prompt such as "Is this article primarily about [Company Name]? Answer yes or no." Then filter the table to only pass through "yes" rows before alerting or acting on the results.

The AI column approach gives the most reliable results when precision matters.
