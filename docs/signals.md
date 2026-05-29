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

Most Signals are available on any paid plan.

### Why is my Signal returning 0 results?

Signals require a connected data source to run against — either a source table containing the companies or contacts you want to monitor, or an audience segment. Without a linked source table or audience segment (or if the linked table is empty or has been deleted), the Signal has nothing to check and will return 0 results. Confirm that your Signal is connected to an active Clay table with valid company identifiers (domain or LinkedIn URL) or contact LinkedIn URLs, or to a populated audience segment.

### I want to find job postings by location or title — is that a Signal?

No. Signals monitor changes at companies or contacts already in your data source (new hires joining, contacts getting promoted, contacts changing jobs, etc.). They are not a way to search for job postings from scratch.

To search for open job postings by location, job title, or other criteria, use the **Find Jobs** source when creating a new table. You can also [schedule it to run on a recurring basis](https://www.clay.com/university/guide/scheduled-sources) (daily, weekly, etc.) so your table stays up to date with the latest postings.

### How do I check for job openings at each company in my table?

If you have a table of companies and want to pull active job openings for each one, use the **Find Active Job Openings** enrichment column — not a Signal.

**To set this up:**

1.  In your company table, click `Add enrichment` and search for `Find Active Job Openings`.
2.  Map your company LinkedIn URL or company domain to the input field (also accepts a Sales Navigator URL or Sales Navigator Company ID — LinkedIn URL gives the highest accuracy). You can optionally filter by job title keywords or location.
3.  Enable **Auto-run** on the table (click the ⛭ icon → **Run Settings**) so the enrichment fires automatically whenever you add a new company row.
4.  To keep job openings refreshed over time, open Table Settings (⛭) → **Run Settings** → toggle on **Re-run columns on a schedule** → select the Find Active Job Openings column → set the frequency to Daily (or as often as you need fresh results).

This gives you both behaviors: new companies you add are enriched automatically, and existing companies are re-checked for new job openings on each scheduled cycle.

**Tip:** The same pattern works for finding people — use the **Find People at Company** enrichment with your company LinkedIn URL or domain to return contacts at each account, then combine auto-run and scheduled re-runs to keep results current.

### Which enrichment should I use to filter job openings by a specific country or city?

Use **Find Active Job Openings**, not the PredictLeads **Find open jobs** enrichment, when you need to scope results to a particular country or city.

-   **Find Active Job Openings** has a `Locations` field that accepts comma-separated countries or cities (e.g., `Germany` or `Berlin, United States`).
-   The PredictLeads **Find open jobs** enrichment only has an `Only jobs tied to a location?` toggle, which excludes jobs with no location tag but cannot filter to a specific place.

### Why do I see the same company name appear multiple times in my Find Jobs results?

This is expected behavior. **Find Jobs returns one row per job posting**, not one row per company. If a company has three open roles matching your criteria, it will appear as three separate rows — one for each posting. Each row represents a distinct job, and you can see the specific job title and URL in the cell details.

To cap how many postings are returned per company, open the **Limit results** section in the Find Jobs settings and set a **Limit per company** value (maximum: 100). Setting this to 1, for example, returns only the most recent matching posting per company, which keeps each company to a single row and makes it easier to treat the table as a company list.

### Why did my signal use far more credits than I expected?

The credit rate shown in a signal's settings covers only the **signal monitoring** itself — checking your tracked contacts or companies for new matches. It does not include any enrichment columns in your results table.

When a signal fires and adds new matching rows to your table, every enrichment column with **auto-update** enabled runs automatically on those new rows. For example, if you have an AI enrichment column that costs 500 credits per row and the signal adds 60 new matches, that enrichment alone consumes 30,000 credits on top of the signal monitoring fee.

To avoid unexpected charges:

-   Check the per-row cost of each enrichment column in your results table before activating a signal.
-   Turn off auto-update on columns you don't want to fire automatically: open the column → `Run settings` → toggle off `Auto-update`.
-   To see the full per-column credit breakdown after a signal fires, click `History` in the lower right corner of your results table and select `Usage history`.
