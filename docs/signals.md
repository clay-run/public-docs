---
title: Signals in Clay
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

1.  Click `Tools`, then select one of the `Monitor for...` options—new hires, job changes, or promotions.
2.  Select the **company table** you want to monitor, then select a **view** from that table — the signal will only check rows visible in that view (not the entire table). Identify the correct company identifiers (website, LinkedIn URL, etc.).
    -   **Note:** The table and view cannot be changed after the signal is saved. To monitor a different set of companies, create a new signal.
3.  Configure filters for the Signal.
4.  Set the frequency that the signal should run.
5.  Optionally, add enrichments to your table to gather additional useful data.
6.  Optionally, `Add sample results`.
    -   This lets you preview how the data will appear after any changes actually happen.
7.  Click `Save and run X rows` to finish the Signal.

### Edit an existing Signal

1.  Click on the column title with the Signal.
    -   It'll have a `📡` icon and is named `Event: [Signal Type]` by default (e.g., `Event: Job change`, `Event: New hire`).
2.  Click `Edit signal`.
3.  Modify any settings as needed and click `Save and re-run` (or `Save and run` if the signal has never run before, `Save only` for scheduled signals, or `Save` for non-scheduled signals).

## FAQs

### Can I set a signal on the first of the month?

Currently, signals can only be adjusted by frequency, not set to run at specific times.

### Does my Signal run automatically when new rows are added to my table?

No. Signals run on a fixed schedule — Daily, Weekly, Biweekly, Monthly, or Quarterly — not when new rows arrive in your table. If new companies or contacts are added via a webhook or other source, the Signal will pick them up on the **next scheduled run**, not immediately.

To trigger the Signal right away after new rows arrive, open the signal column header → **Edit signal** → click **Save and run** (or **Save and re-run** if the signal has run before).

### How do I run a signal on a filtered or growing list of companies from another table?

Use [Send Table Data](send-table-data.md) with a run condition to push qualifying rows to a destination table, then set up your signal to monitor that destination table:

1.  In your source table, add a **Send Table Data** column. Include the **company domain** in the columns you send — the signal needs a company domain or company name to look up company information.
2.  Optionally add a [run condition](conditional-runs.md) so only qualifying rows (for example, companies with a score of 50 or above) are sent. Enable **Update existing rows on re-run** to avoid duplicates as your source table grows.
3.  In the destination table, click the **"rows from: …"** source cell and use **Add to column** to extract the company domain into its own standalone column.
4.  Set up your signal in the destination table, selecting the company domain column as the identifier.

The signal runs on its scheduled cadence and checks all rows in the destination table — including rows that arrived via Send Table Data — **on the next scheduled run**, not immediately when they arrive.

**Why is "Company Record" showing `ERROR_MISSING_INPUT`?** The company record is not a field you can map inside Send Table Data — it populates automatically once a valid company domain or name is present in a table column and wired as the signal's identifier. If you see this error, confirm that: (1) the company domain is included in what you are sending, and (2) you have used **Add to column** to extract it from the **"rows from: …"** source cell into a standalone column in the destination table.

### What plans are Signals available on?

Most Signals are available on any paid plan.

### Why is my Signal returning 0 results?

Signals require a connected data source to run against — either a source table containing the companies or contacts you want to monitor, or an audience segment. Without a linked source table or audience segment (or if the linked table is empty or has been deleted), the Signal has nothing to check and will return 0 results. Confirm that your Signal is connected to an active Clay table with valid company identifiers (domain or LinkedIn URL) or contact LinkedIn URLs, or to a populated audience segment.

### How do I update or replace my master source table without breaking my signal workflows?

Signal columns reference their source table by its internal ID, not its name. Renaming a table won't break any connected signals — but replacing it with a different table will disconnect them unless you update each signal to point to the new one.

**Option 1 (recommended) — Update the rows inside the same table:**

The safest approach is to replace the data inside your existing source table so its ID stays the same:

1.  In your existing master source table, delete the old rows.
2.  Re-import your updated account list into the same table (via CSV, CRM sync, or any source).
3.  In each signal table, re-run the signal column (click the 📡 column header → run) so it picks up the new account list on its next cycle.

Because the table ID hasn't changed, all downstream signal workflows remain connected automatically.

**Option 2 — Switch to a different source table (requires rebuilding each signal):**

The signal's Company Table, View, and Company Identifier fields are locked after the signal is created and cannot be updated via **Edit signal**. If Option 1 is not feasible — for example, if you need to monitor a fundamentally different set of companies — you will need to rebuild each affected signal.

**To preserve your enrichment columns when rebuilding**, save the existing signal results table as a template first: click the table title → scroll to **Share as template** → toggle it on and copy the link. Open the link to create a new table — the new table will include all your enrichment column configurations. Then set up your signal from scratch in your source company table (via **Tools** → the relevant signal type), targeting the new source table.

### How do I extend my signal to cover more companies?

A signal monitors only the companies visible in the **view** you selected from your source table when setting it up. Once the signal is saved, the table and view selection are locked and cannot be changed.

To cover more companies with the existing signal:

-   **Add more rows to the source table.** New companies added to the source table will be picked up automatically on the signal's next scheduled run, as long as they appear in the selected view.
-   **Broaden the selected view's filters.** In the source company table, edit the filters on the view the signal is using so it includes more rows — the signal will check those additional rows on the next run.

To monitor a completely different set of companies (using a different view), create a new signal.

### Why is the View field empty or locked when I open Edit Signal?

When editing an existing company-based signal (New Hire, Job Posting, etc.), the **Company Table**, **View**, and **Company Identifier** fields are permanently locked — they cannot be changed after the signal is first created. If the **View** dropdown appears empty or unselectable, this typically means the source company table the signal was originally built on has since been deleted.

Because these source fields cannot be re-pointed after creation, the fix is to rebuild the signal:

1.  Open your current company table → click **Tools** → select the signal type (e.g., **Monitor for new hires**).
2.  Configure your filters and set the desired run frequency.
3.  Click **Save and run**.

You can then delete the old signal. Rebuilding does not reprocess previously seen results.

**Tip — preserve your enrichment columns during a rebuild:** If your existing signal results table has enrichment columns you've built out, save the table as a template before rebuilding. Click the table title → scroll to **Share as template** → toggle it on and copy the link. Open the link to create a new table — the new table will include all your enrichment column configurations, so you don't have to rebuild them from scratch.

### I want to find job postings by location or title — is that a Signal?

No. Signals monitor changes at companies or contacts already in your data source (new hires joining, contacts getting promoted, contacts changing jobs, etc.). They are not a way to search for job postings from scratch.

To search for open job postings by location, job title, or other criteria, use the **Find Jobs** source when creating a new table. You can also [schedule it to run on a recurring basis](https://www.clay.com/university/guide/scheduled-sources) (daily, weekly, etc.) so your table stays up to date with the latest postings.

### How do I check for job openings at each company in my table?

If you have a table of company domains or names and want to pull active job openings for each one, use the **Find Active Job Openings** enrichment column — not a Signal.

**To set this up:**

1.  In your company table, click `Add enrichment` and search for `Find Active Job Openings`.
2.  Map your company domain to the input field. You can optionally filter by job title keywords, job description keywords, location, or days since posted.
3.  Enable **Auto-run** on the table (click the ⛭ icon → **Run Settings**) so the enrichment fires automatically whenever you add a new company row.
4.  To keep job openings refreshed over time, open Table Settings (⛭) → **Run Settings** → toggle on **Re-run columns on a schedule** → select the Find Active Job Openings column → set the frequency to Daily (or as often as you need fresh results).

This gives you both behaviors: new companies you add are enriched automatically, and existing companies are re-checked for new job openings on each scheduled cycle.

**Tip:** The same pattern works for finding people — use the **Find People at Company** enrichment with your company domain to return contacts at each account, then combine auto-run and scheduled re-runs to keep results current.

**Tip: Extracting individual job roles from the output.** Each Find Active Job Openings cell holds a **list** of job postings — a company with 5 open roles returns all 5 in one cell, not as 5 separate rows. To get a usable per-role breakdown: click into any populated cell in the column, then in the Cell details panel click **Take action on list** → **Write each item to new row in other table**, and pick a destination table. Each job posting becomes its own row in that table. See [Send table data](send-table-data.md) for full configuration details.

### Which enrichment should I use to filter job openings by a specific country or city?

Use **Find Active Job Openings**, not the PredictLeads **Find open jobs** enrichment, when you need to scope results to a particular country or city.

-   **Find Active Job Openings** has a `Locations` field that accepts comma-separated countries or cities (e.g., `Germany` or `Berlin, United States`).
-   The PredictLeads **Find open jobs** enrichment only has an `Only jobs tied to a location?` toggle, which excludes jobs with no location tag but cannot filter to a specific place.

### Why do I see the same company name appear multiple times in my Find Jobs results?

This is expected behavior. **Find Jobs returns one row per job posting**, not one row per company. If a company has three open roles matching your criteria, it will appear as three separate rows — one for each posting. Each row represents a distinct job, and you can see the specific job title and URL in the cell details.

If you want only one posting per company, apply **Auto-dedupe** to the imported table. In Table Settings (⛭ → **Edit table settings**), enable **Auto-dedupe rows**, select the company name or domain column as the deduplication key, and choose whether to keep the oldest or newest row. Clay will reduce the results to one row per unique company. See [Table management settings](table-management-settings.md) for details.

### Why did my signal use far more credits than I expected?

The credit rate shown in a signal's settings covers only the **signal monitoring** itself — checking your tracked contacts or companies for new matches. It does not include any enrichment columns in your results table.

When a signal fires and adds new matching rows to your table, every enrichment column with **auto-update** enabled runs automatically on those new rows. For example, if you have an AI enrichment column that costs 500 credits per row and the signal adds 60 new matches, that enrichment alone consumes 30,000 credits on top of the signal monitoring fee.

To avoid unexpected charges:

-   Check the per-row cost of each enrichment column in your results table before activating a signal.
-   Turn off auto-update on columns you don't want to fire automatically: open the column → `Run settings` → toggle off `Auto-update`.
-   To see the full per-column credit breakdown after a signal fires, click `History` in the lower right corner of your results table and select `Usage history`.

### Why did my Job Posting signal return fewer results than expected?

Check the **Limit results** setting inside the **Filter results** section of your signal configuration. By default, a Job Posting signal can return up to 1,250 job postings per run. If you previously entered a lower number — for example, 20 while testing — that value is saved and applies to every subsequent run.

To check or adjust it:

1.  Click the signal column header (the `📡` icon, named `Event: [Signal Type]` by default).
2.  Click **Edit signal**.
3.  Expand the **Filter results** section and review the **Limit results** field. Remove the value or enter a higher number.
4.  Click **Save and re-run**.

There is also a **Limit per company** option in the same section that caps how many job postings are returned for each individual company in your source table. Check this setting too if some companies appear to return fewer results than you expect.

**Important:** The credit cost for a Job Posting signal is based on the number of **companies checked** in your source table view — not the number of job postings returned. Setting a lower result limit reduces your output, but does not reduce the credits charged for that run.

### Does pausing or deleting a results table stop the signal from running?

No. Signals operate independently of the tables they populate. Pausing a results table, deleting rows from it, or deleting the table itself does not stop the signal from running on its scheduled cadence or consuming credits.

Credits for signal monitoring are charged based on the number of contacts or rows **checked** — not the number of matching results returned. A signal checking 5,000 contacts consumes credits for all 5,000 checks, even if no matches are found that run.

To stop a signal from consuming credits, you must pause or disable it directly from the signal's column settings — not by pausing the table it populates:

1.  Click the signal column header (the `📡` icon, named `Event: [Signal Type]` by default).
2.  Click `Edit signal`.
3.  Disable or pause the signal, then save.

You can review all active signals and their individual credit spend in the `Signals` tab of the [credit usage dashboard](/docs/credit-usage) (`Settings` → `Usage`).

### Why does my signal keep writing results to a new table instead of my existing one?

Signals always write their matching events to a **new dedicated results table** — one row per event. Whether you start signal setup from inside an existing table (via `Tools` → `Monitor for...`) or from the Signals section / Workbook overview, the existing table you select is used as the **input source** that supplies the companies or contacts to monitor; it is not the destination for the events. Clay creates a fresh output table to capture matching events.

Signals always add **new rows** for each matching event — one row per event, not a new column on existing rows. If your goal is to see signal data (such as a recent funding round) alongside your existing contacts, see the next FAQ.

### My table has contacts (people). How do I bring company-level signal data into it?

Signals track events at the **company level** — each fundraising round, new hire, or news item becomes a new row in the signal's results table. To surface that data inside a contacts table, use **company domain** as a shared key:

1.  Let the signal run in its own results table. Make sure the results table includes the company domain for each event (this is included by default for most signals).
2.  In your contacts table, click **Add enrichment** and search for **Lookup Single Row in Other Table**.
3.  Set the matching column to **company domain** — Clay will find the corresponding row in the signal results table for each contact's company.
4.  Map the signal columns you want to surface (e.g., event type, funding amount, news headline) as output fields.

This lets you see the latest signal event for each company directly in your contacts table without mixing signal event rows into your contacts.

### Why did my brand mentions signal stop working?

The social network brand mentions signal — along with related social listening actions — was discontinued in early March 2026. Clay's data partner for these actions updated their terms of use, and to remain aligned with their guidelines, Clay discontinued this feature.

If you had a brand mentions signal set up before the deprecation, it will show an error when run and cannot be re-enabled.

**Alternatives for monitoring brand mentions:**

-   **Monitor Professional Posts signal** — To find professional posts that mention your company (rather than posts that merely contain your company name as a keyword), use the **Monitor Professional Posts** signal. Set the **Companies filter** to **Mentions companies** and provide your company domain or professional profile URL as the identifier. Up to 5 domains or URLs are supported.
-   **Claygent** — Use Clay's AI web scraper to monitor brand mentions from publicly available sources on the web.
-   **Google News alerts** — Integrate through Clay to track brand mentions across news and web content.
-   **Third-party social listening tools** — Many social listening platforms can connect to Clay through API integrations, letting you route mention data into your Clay tables.

### Why did my job description keyword search return unexpected results?

Job description keywords use phrase matching — your search term must appear as a contiguous sequence of words in the job description. Hyphens in your search terms are treated as word separators, so "K-12" and "K 12" produce the same search (both look for the phrase "k 12" in the description). If you want to search for a compound term as a single unbroken token, enter it without separators (for example, use "k12" instead of "K-12").

For filtering that keywords alone cannot capture, run **Find Active Job Openings** first and then add a **Use AI** column to verify which results match your actual criteria.