---
title: Custom Signals
description: Create unique signals to monitor changes to your team's data sources.
last_synced: 2026-04-26T01:39:50.046Z
---

# Custom Signals

Create unique signals to monitor changes to your team's data sources.

Custom Signals let you monitor data sources for specific changes on a regular schedule. You can:

-   Monitor websites, social media platforms, and other digital sources.
-   Track technology adoption, hiring profiles, and new feature rollouts.
-   Monitor compliance changes (e.g., when a company adds GDPR compliance to their trust center).
-   Set up RSS feeds for web mentions.
-   Schedule automated runs using Clay's AI tool to create your own unique signals.

## Creating a custom signal

1.  To create a custom signal:
    -   **In a workbook**: Click `+ Add` → `Custom signal`.
    -   **In a table**: Click `Tools` → `Import` → `Custom signal`.
2.  Select a source to monitor.
    -   Next to each source, you'll see the estimated cost per result.
3.  Configure your source.
    -   Some sources require an account, while others use a Clay-provided account.
4.  Set how frequently you want your signal to run.
5.  Optionally, add enrichments (such as Slack notifications or Salesforce updates that trigger when the signal runs).
6.  Click `Save`.

## Editing a custom signal

1.  Click the column title of the signal (signals will have a toggle next to their titles)
2.  Click `Edit column`.
3.  Adjust any of the configurations or the frequency to run and click `Save`.

**Clay offers several pre-created Signals for common use cases:**

-   [New hires](https://www.clay.com/university/guide/new-hire-signal-overview): Keep track of new hires at target companies within the last three months, enabling you to engage during the crucial decision-making window.
-   [Promotions](https://www.clay.com/university/guide/promotion-signal-overview): Monitor when contacts receive promotions within their current company, allowing you to engage during high-intent decision-making periods.
-   [Job changes](https://www.clay.com/university/guide/job-change-signal-overview): Track when your contacts move to new companies, helping you leverage existing relationships for new opportunities or prepare for shifts in account engagement.
-   [News & fundraising](https://www.clay.com/university/guide/monitor-for-news-fundraising): Alert you to significant events at monitored companies, helping you spot timely engagement opportunities.

## FAQs

### How do Custom Signals with data sources like HG Insights work?

When you select an external data source — such as **Source Companies by product usage with HG Insights** — as the source for your Custom Signal, the signal actively queries that provider on each scheduled run to discover companies that match your criteria. You do not need a pre-existing list of companies to get started.

On each run, the signal queries the provider (for example, HG Insights) for companies matching your configuration, then compares the results against companies already in your signal's results table. Any newly identified companies are added as new rows. Companies already present in the table are not duplicated.

This means your signal automatically surfaces net-new companies on each run — for example, companies that HG Insights has newly identified as using your target technology since the last time the signal ran. Each newly detected company gets added as a row in your Clay table, where you can trigger enrichment columns, Slack notifications, or outreach workflows.

The preview shown in the signal wizard (labeled "This is a preview showing up to 10 sample results") displays example companies that match your current configuration. It is illustrative — it does not represent results that are already being continuously tracked.

### What does the recurring credit cost in the signal wizard mean?

Credits for a Custom Signal using HG Insights as the source are charged per company result that HG Insights returns on each run. If HG Insights returns no companies on a given run, no source-query credits are charged for that run.

One important nuance: credits are charged for every company HG Insights returns in the query, including companies already present in your results table from a previous run. Those existing companies are not added as duplicate rows, but they do count toward the run's credit cost.

The estimate shown in the wizard reflects the expected total cost per run based on the number of company results your configuration is likely to return. Changing the run cadence (daily, weekly, monthly) does not change the per-result credit rate — it only changes how often the signal queries HG Insights.

To manage your credit spend:
-   Reduce the **Max companies** input in your signal configuration to limit how many results HG Insights can return per run.
-   Review any enrichment columns in your results table — each enrichment with **Auto-update** enabled will also run automatically on newly added rows and will consume additional credits on top of the source query cost. Turn off **Auto-update** on enrichment columns you don't want to fire automatically.
-   To see your full credit breakdown after a signal run, click `History` in the lower right corner of your results table and select `Usage history`.

## Guide: Turning enrichments into signals

You may occasionally need to monitor changes in an enrichment. Below is a step-by-step guide on creating a signal for any enrichment. **In this guide, we'll start with a list of companies and add enrichments to monitor.**

### Table 1: Setting up an enrichment

1.  Start with a list of companies (Create a new table or in an existing table, click `Tools` → `Import`)
2.  If you don't already have one, create the enrichment you want to turn into a signal.
3.  Set up a [scheduled run](https://www.clay.com/university/guide/scheduled-columns) for your enrichment by clicking the `⚙️` → enable `Re-run columns on a schedule`.
4.  Under `Tools` → click `Send table data` and include the enrichment in the columns that are sent. Send this data to a new table that we'll call "Run history".
    -   Make sure the **company name** or **company domain** is part of the data sent to the new table, as these will be essential in the upcoming steps.
5.  Toggle off `Update existing rows on re-run` to create new rows for each recurring run.

### Table 2: Setting up a run history table

1.  Go into the "Run history" table and pull out the company name/domain and the output of the enrichment as columns from the source.
2.  Click the columns dropdown in the upper left corner of the table and unhide `Created At`.

### Table 3: Identify the difference between runs

1.  In a third table, which we'll call the "Lookup" table, click `Tools` → `Lookup Multiple Rows in Other Table`.
2.  Set up the lookup to check the "Run history" table and use the company name or domain as the identifier.
3.  Set up a [scheduled run](https://www.clay.com/university/guide/scheduled-columns) for this lookup by clicking `⚙️` in the bottom right corner → enable `Re-run columns on a schedule`.
    -   This should run at the same schedule as the first table.
    -   **Note:** To coordinate run timing between the two tables, enable the second table's schedule a few minutes after the first. You can use the **Custom** frequency option to set a specific day, time of day, and timezone for each table's schedule — see [Scheduled columns](https://www.clay.com/university/guide/scheduled-columns) for details.
4.  Click `Tools` → `Use AI`. Generate a prompt that references the output from the `Lookup Multiple Rows in Other Table` and identifies the difference between the two most recent runs, using `Created At`.  
    -   This prompt will provide two outputs: any new information returned from the 2nd run that wasn't in the 1st run, and a True/False boolean indicating if there is any new information.**‍**
    -   **Note:** If your data is structured or numerical, you can use a formula to detect changes. However, if there's significant variability between outputs, you'll likely want to use an AI action to holistically determine the difference between runs.
5.  Take the result from `Use AI` and write it to a fourth table (the "Signal" table), using `Tools` → `Send table data`.  
    -   You can do this using run conditions.  
        -   For a numerical output, the run condition should be if the change is not 0.  

        -   For a text output (string), the run condition should be if the boolean generated from the AI action is True.

### Table 4: Store the signal

1.  Go into the "Signal" table and pull out the company name/domain and the output from the AI action that described the difference between runs.
2.  Click the columns dropdown in the upper left corner of the table and unhide `Created At`. This date will serve as a timestamp showing when the signal was detected.
