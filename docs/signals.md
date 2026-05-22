---
title: Signals in Clay
source_url: https://university.clay.com/docs/signals
description: Learn about Signals, a way to monitor changes to your contacts like
  promotions, job changes, or new hires.
last_synced: 2026-04-26T01:40:40.844Z
---

# Signals in Clay

Learn about Signals, a way to monitor changes to your contacts like promotions, job changes, or new hires.

Signals are automated tracking systems that notify you of important changes related to your contacts and target companies. They help you identify and act on key business opportunities at the right moment.

**Signals in Clay can track these types of events:**

-   [New hires](https://www.clay.com/university/guide/new-hire-signal-overview): Keep track of new hires at target companies within the last three months, enabling you to engage during the crucial decision-making window.
-   [Promotions](https://www.clay.com/university/guide/promotion-signal-overview): Monitor when contacts receive promotions within their current company, allowing you to engage during high-intent decision-making periods.
-   [Job changes](https://www.clay.com/university/guide/job-change-signal-overview): Track when your contacts move to new companies, helping you leverage existing relationships for new opportunities or prepare for shifts in account engagement.
-   [LinkedIn brand mentions](https://www.clay.com/university/guide/monitor-for-linkedin-brand-mentions): Track company mentions, identify partnerships, address feedback, find testimonials, and measure campaign impact.
-   [News & fundraising](https://www.clay.com/university/guide/monitor-for-news-fundraising): Alert you to significant events at monitored companies, helping you spot timely engagement opportunities.

Looking to monitor a specific enrichment? [Learn how to create Custom Signals.](https://www.clay.com/university/guide/custom-signals)

## Setting up a Signal

To start a signal, you'll **need a table with** companies or contacts you want to monitor. This **table should include** LinkedIn URLs for individuals or company identifiers (such as website or LinkedIn URLs).

**While in your table:**

1.  Click `Actions`, then select one of the `Monitor for...` options—new hires, job changes, or promotions.
2.  Select the table you want to monitor and identify the correct identifiers (website, LinkedIn URL, etc.)
3.  Configure filters for the Signal.
4.  Set the frequency that the signal should run.
5.  Optionally, add enrichments to your table to gather additional useful data.
6.  Optionally, `Add sample results`.
    -   This lets you preview how the data will appear after any changes actually happen.
7.  Click `Save and run X rows` to finish the Signal.

### Edit an existing Signal

1.  Click on the column title with the Signal.
    -   It'll have a `📡` icon and usually be called `Event`.
2.  Click `Edit column`.
3.  Modify any settings as needed and click `Save changes`.

## FAQs

### Can I set a signal on the first of the month?

Currently, signals can only be adjusted by frequency, not set to run at specific times.

### What plans are Signals available on?

Most Signals are available on any paid plan. The [LinkedIn social listening Signal](https://www.clay.com/university/guide/monitor-for-linkedin-brand-mentions) is only available to Pro and Enterprise customers.

### Why is my Signal returning 0 results?

Signals require a connected data source to run against — either a source table containing the companies or contacts you want to monitor, or an audience segment. Without a linked source table or audience segment (or if the linked table is empty or has been deleted), the Signal has nothing to check and will return 0 results. Confirm that your Signal is connected to an active Clay table with valid company identifiers (domain or LinkedIn URL) or contact LinkedIn URLs, or to a populated audience segment.

### I want to find job postings by location or title — is that a Signal?

No. Signals monitor changes at companies or contacts already in your data source (new hires joining, contacts getting promoted, contacts changing jobs, etc.). They are not a way to search for job postings from scratch.

To search for open job postings by location, job title, or other criteria, use the **Find Jobs** source when creating a new table. You can also [schedule it to run on a recurring basis](https://www.clay.com/university/guide/scheduled-sources) (daily, weekly, etc.) so your table stays up to date with the latest postings.
