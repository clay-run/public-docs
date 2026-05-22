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

### Why did my signal use far more credits than I expected?

The credit rate shown in a signal's settings covers only the **signal monitoring** itself — checking your tracked contacts or companies for new matches. It does not include any enrichment columns in your results table.

When a signal fires and adds new matching rows to your table, every enrichment column with **auto-update** enabled runs automatically on those new rows. For example, if you have an AI enrichment column that costs 500 credits per row and the signal adds 60 new matches, that enrichment alone consumes 30,000 credits on top of the signal monitoring fee.

To avoid unexpected charges:

-   Check the per-row cost of each enrichment column in your results table before activating a signal.
-   Turn off auto-update on columns you don't want to fire automatically: open the column → `Run settings` → toggle off `Auto-update`.
-   To see the full per-column credit breakdown after a signal fires, click `History` in the lower right corner of your results table and select `Usage history`.

### Does pausing or deleting a results table stop the signal from running?

No. Signals operate independently of the tables they populate. Pausing a results table, deleting rows from it, or deleting the table itself does not stop the signal from running on its scheduled cadence or consuming credits.

Credits for signal monitoring are charged based on the number of contacts or rows **checked** — not the number of matching results returned. A signal checking 5,000 contacts consumes credits for all 5,000 checks, even if no matches are found that run.

To stop a signal from consuming credits, you must pause or disable it directly from the signal's column settings — not by pausing the table it populates:

1.  Click the signal column header (the `📡` icon, usually named `Event`).
2.  Click `Edit column`.
3.  Disable or pause the signal, then save.

You can review all active signals and their individual credit spend in the `Signals` tab of the [credit usage dashboard](/docs/credit-usage) (`Settings` → `Usage`).
