---
title: "Guide: Ways to save Clay credits"
description: Make the most out of your Clay credits.
last_synced: 2026-04-26T01:39:44.229Z
---

# Guide: Ways to save Clay credits

Make the most out of your Clay credits.

## Guide: Ways to Save Clay Credits

Clay credits are valuable resources that help you save both time by automating manual work and money on go-to-market resources. By optimizing how you use credits, you can ensure your workflows remain efficient while delivering the results you need growth. This guide outlines a few best practices to help you get the most out of your credits.

## Pause enrichments for new entries by turning off auto-run

**How does this save credits?**

By default, auto-run is **on** for every new table — Clay automatically enriches each row as soon as it arrives. While this is useful for production workflows, it can consume credits faster than expected when you're still building or testing: add a large batch of rows before your setup is finalized and all enrichments fire immediately.

The best practice is to **turn off table-level auto-run while building your table**. Once your setup is finalized and tested, turn it back on when you're ready to process your full list.

**How do you implement this?**

To disable auto-run for the entire table (the master switch):

1.  Click the `⛭` icon in the top toolbar to open Run Settings.
2.  Toggle **Auto-run** off. The toggle shows **"Manual"** when disabled.

With table-level auto-run off, no columns will run automatically when rows are added — regardless of individual column settings. You can still trigger enrichments manually by clicking individual cells.

**Recommended testing workflow:**

1.  Turn table-level auto-run **OFF** before adding any rows.
2.  Add a small sample (5–10 rows).
3.  Manually click individual cells to test enrichments.
4.  Refine your configuration until results look right.
5.  Turn auto-run back **ON** when you're ready to process the full list.

To turn off auto-run for a single column instead of the whole table, click the column name → **Edit column** → toggle **Auto-run** off under **Run settings** → **Save**.

See [Table management settings](table-management-settings.md) for full details on table-level and column-level auto-run controls.

## Leveraging your API Keys

**How does this save credits?**

If you are on a paid plan and have credits with other data providers, Clay allows you to integrate your own API keys, giving you the flexibility to use those resources directly within your workflows.

**How do you use your own API key?**

You can access adding your API key two ways:

1.  Profile picture  > Settings > Navigation Bar
2.  Go to your profile picture in the top right corner, navigate to Settings, and head over to the Connections section. From there, you can add your API keys to the Clay panel.
3.  Enrichment Panel > Account > Add Account
4.  When setting up an enrichment that accepts an API key, you can add an account linked to your API key. By default, Clay's API key will be selected, but if you want to use your own, simply switch to your account by selecting **Add Account**.

Some common API keys you can swap out:

-   **OpenAI API keys**
-   **Anthropic**
-   **Apollo** (_Make sure to use the correct API key for the specific service you are integrating)_
-   **Email Providers** (e.g., Findymail, Prospeo)**‍**
-   **Email Verifiers** (e.g., Debounce, NeverBounce)

You can add your own API keys when you select the account your enrichment runs on (Paid Feature)

## Choose cost-effective AI models for Use AI and Claygent columns

**How does this save credits?**

When you add a **Use AI** or **Claygent** column, the model you select directly sets the credit cost per row. Clay's default recommendation is **Argon** (3 credits/row for Claygent tasks), which excels at deep research and complex analysis. For simpler tasks — such as formatting, basic classification, or straightforward lookups — switching to a lower-cost model can dramatically reduce per-row spend without sacrificing quality for those use cases.

**How do you implement this?**

When configuring an AI column, open the **Model** dropdown in the column settings and select a more cost-effective option. For example, **GPT 4.1 Nano** costs 0.1 credits/row for content generation (Use AI) and 0.5 credits/row for web research (Claygent) — compared to **Neon** at 2 credits/row and **Argon** at 3 credits/row for Claygent tasks.

As a general rule: match the model to the task complexity. Reserve higher-credit models like Argon for multi-step research tasks where quality matters most; use lower-cost models like GPT 4.1 Nano for high-volume, simpler tasks where efficiency is the priority.

See [How AI is priced](ai-pricing.md) for the full model pricing comparison.

## Qualify leads before enriching

**How does this help conserve credits?**

By adjusting the order of enrichments, you can save credits by enriching only the leads that meet specific criteria. If you have leads that can be disqualified early in the process, filtering them out ensures that only qualified contacts are enriched, preventing unnecessary credit usage.

**How do you implement this?**

You can set up **conditional runs** or use **AI formulas** to filter rows based on specific criteria (e.g., location, company size, or industry) to enrich only the contacts that are most relevant to your criteria.

Here is an example of a way to use AI formulas to filter out leads

## Test out your data

**How does this save credits?**

When using a new integration, it's best to start by testing a small sample—about 10 rows—before running the entire column. This allows you to identify and fix any errors in advance (ex. import errors, column filter error)

For AI enrichments, prompts may need several iterations to get right, so testing and refining your prompts before running the full enrichment will help ensure better results.

**How do you implement this?**

Before running an enrichment, you can test it on 10 rows or apply it to the entire column. This gives you flexibility in troubleshooting and improving your setup before committing fully.

## Conditional runs

**How does this save credits?**

Conditional formulas help you conserve credits by ensuring that enrichments only run when specific conditions are met. Instead of enriching every row, you can create rules that limit enrichments to only the most relevant rows, such as leads that meet certain criteria. This prevents unnecessary enrichments on disqualified or low-priority leads, allowing you to use credits more efficiently.

**How do you implement this?**

There are two ways to implement conditional runs:

**Method #1: Conditional Runs**

1.  Go to the **Run Settings** of any enrichment column.
2.  In the **"Only run if"** box, add your conditional formula to specify when the enrichment should run.
3.  **Tip:** Use the **"Use AI"** button to input plain language instructions, making it easier to define your conditions without needing complex formulas.

**Method #2: Filter Existing Rows**

You can also conditionally run columns through filtering rows.

Filtered views only enriches the rows you're viewing so this can be used as a way to run enrichments conditionally

## Look up existing data to avoid duplicate enrichments

If you've already enriched contacts in another table or your CRM, you can use **Lookup** columns to pull that existing data, saving credits by avoiding duplicate enrichments. Before running a new enrichment, check if the data already exists in your CRM or another Clay table. If it does, use a Lookup column to pull the data into your current table.

**How do you implement this?**

1) Pull Data from Your CRM  

2) Leverage Data from Other Tables

## Limit People source search results

**How does this save credits?**

When using Find People as a source, broad searches can return thousands of results—each becoming a row that triggers downstream enrichments. Importing more contacts than you need is one of the most common sources of unintended credit spend.

**How do you implement this?**

In your Find People column settings, use **Limit results** to cap the total number of contacts imported per search. Use **Limit per company** to set a maximum number of people per employer—especially important when your search covers large parent companies or investment portfolio companies that could expand results far beyond your intent. Add company-level filters such as company size or industry to narrow the match universe before rows are created.

See [Find People in Clay](find-people-overview.md) for the full list of filter and limit options.

## Use Sandbox Mode to test table changes safely

**How does this save credits?**

[Sandbox mode](sandbox-mode.md) lets you build and test table configurations—formulas, enrichments, waterfalls—on a small subset of rows without running them on your full table. Changes only go live when you explicitly publish them, so you can catch configuration mistakes and refine your setup before spending credits at scale.

**How do you implement this?**

Click the `Sandbox mode` button in the table toolbar. Clay duplicates the top 10 rows of your table into an isolated sandbox (expandable to 50 rows). Make and test your changes there; when ready, click **Review changes** and then **Publish** to apply the configuration to your full table.

## Audit and manage scheduled column runs

**How does this save credits?**

Scheduled columns automatically re-run enrichments on a daily, weekly, or monthly cadence—including full-table re-runs if **All columns** is selected. Columns set up for a past project and then forgotten continue consuming credits on every cycle.

**How do you implement this?**

Click the `⛭` icon in the top toolbar, go to **Run Settings**, and open the **Re-run columns on a schedule** section. Review which columns are included and disable the schedule for any you no longer need to auto-refresh. To reduce scope without fully disabling the schedule, switch from **All columns** to **Only selected columns** and select only the columns that genuinely require recurring updates.

See [Scheduled columns](scheduled-columns.md) for setup details.

**Note:** Scheduled column runs are available on paid plans.
