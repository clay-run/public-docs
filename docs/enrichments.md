---
title: Enrichments
description: Learn how to run enrichments in Clay, including how enrichment search works, run settings, delay options, and custom rate limits.
last_synced: 2026-04-26T01:39:56.840Z
---

# Enrichments

Learn how to run an enrichment within Clay.

Enrichments in Clay transform your data by pulling in additional information from various sources. Clay's enrichment tools enhance your data quickly and efficiently. Use them to:

-   Verify email addresses
-   Gather company details
-   Find social media profiles

You can run enrichments in several ways:

-   Individually
-   Using pre-built templates
-   Creating powerful recipes to automate complex workflows

## Running an enrichment

1.  In a Clay table, click `Add enrichment` and search for an enrichment.
2.  Under `Integrations`, select an option.
3.  In the modal, select your account.
    -   Clay provides API keys for certain enrichments, but you can save [credits](https://www.clay.com/university/guide/credits) by using your own account—click `+ Add account` to set it up.

## Enrichment search

When you click `Add enrichment` and start typing, the search panel surfaces the most relevant options for your query.

**Curated results for popular queries.** For common searches like `email`, `phone`, `linkedin`, `salesforce`, and others, Clay shows curated results with waterfall options listed first — these multi-provider sequences maximize coverage at the lowest credit cost. For other queries, results are ranked by relevance.

**Row type labels.** Every result shows its type — **Waterfall**, **Enrichment**, **Template**, **Send & export**, and so on — so you can tell at a glance what you're selecting. Enrichments you created show "By me"; those from colleagues show the creator's name (for example, "By Jane Smith"); and Clay-built options show "By Clay."

**Institutional knowledge badges.** Some results carry badges that surface practical provider context contributed by Clay's Solutions and Partnerships teams — for example, "EMEA Coverage" or "SMB." Click a badge to filter the result list to providers tagged with that label.

## Run settings

Run settings give you control over when and how your enrichments execute. Access these settings by clicking into any enrichment column.

### Auto-update

When enabled, the enrichment will automatically re-run whenever its input values change. This keeps your data fresh without manual intervention.

-   Toggle **on** to automatically update results when input data changes
-   Toggle **off** to run the enrichment only when you manually trigger it

### Only run if

Use conditional logic to control when an enrichment runs. The enrichment only executes if your specified conditions are met.

1.  Enter a formula in the `Only run if` field.
2.  The enrichment runs when the formula evaluates to `true`.
3.  Click `Use AI` to generate conditional formulas automatically.

### Saving configuration changes

When you click **Save** after editing an enrichment column, a dropdown lets you choose how the change takes effect:

-   **Save and don't run** — Saves your updated settings without re-running existing rows. If [auto-run](table-management-settings.md) is enabled, new rows added after saving will still trigger this enrichment automatically; historical rows remain unchanged until you manually trigger a run.
-   **Save and run _N_ rows** — Saves your settings and immediately queues all rows in the table for a run using the updated configuration.

## Delay run

Delay when an enrichment runs after its conditions are met. This is useful when you need to wait for external systems to process data before continuing your workflow.

`Run immediately`

-   Runs the action as soon as run conditions are met.
-   Default behavior for all enrichments.

`Run after delay`

-   Waits a specified number of seconds before running (maximum 10 minutes).
-   Delay starts after run conditions are met.
-   Useful for syncing between external systems, like waiting for Salesforce to sync data to Outreach.

To configure a delay:

1.  Select `Run after delay`.
2.  Enter the number of seconds to wait (up to 600 seconds/10 minutes).
3.  Use a formula to set different delays per row.

**Need a delay longer than 10 minutes?** Chain multiple enrichment columns — each set to `Run after delay` (up to 600 seconds) — and use [conditional runs](conditional-runs.md) to gate each step on the previous column completing. For example, six chained delay columns each set to 600 seconds creates a 60-minute total delay.

**Need a delay of multiple hours, days, or weeks?** The chaining approach above maxes out at around 60 minutes. For longer waits — such as holding columns until a set number of days or weeks after a row was processed — use a date-based run condition instead: add a formula column that compares a timestamp in the current row against today's date plus your desired interval, then gate your downstream enrichments on that formula column using **Only run if → is not empty**. To keep the formula re-evaluating automatically each day, pair the formula column with a scheduled HTTP API column that fetches the current date once per day; the formula column updates automatically whenever the HTTP API column runs. For step-by-step instructions and example formulas, see [How do I use today's date in a formula?](formula-generator.md#how-do-i-use-todays-date-in-a-formula).

## Custom rate limit

Limit how many requests Clay sends to an external service within a given time window. This is useful when you need to stay within an API provider's rate limits while running enrichments at scale.

When supported by an enrichment, a **Custom rate limit** collapsible section appears at the bottom of the enrichment settings panel.

-   **Request limit** — The maximum number of requests to send within the time window.
-   **Duration (in ms)** — The length of the time window in milliseconds (between 1 and 900,000 ms / up to 15 minutes).

The request limit and duration together must average at least 1 request per second (for example, 60 requests per 60,000 ms is valid; 1 request per 2,000 ms is also valid).

**Tip — set slightly below the provider's documented maximum:** When a request hits a rate limit, Clay's retry fires immediately with no delay between the failed attempt and the next try. If your Request limit is set at exactly the provider's stated maximum, the retry can push you back over the limit right at the edge of the window. To leave headroom for retries, set your Request limit one step below the provider's cap — for example, if the provider allows 5 requests per 1,000 ms, try 4 requests per 1,000 ms.

**Note:** Custom rate limit is not available for Clay's built-in AI enrichments (Use AI, Claygent, etc.). It only appears for enrichments that support custom rate limiting, such as HTTP API and Apollo OAuth enrichments.

## Troubleshooting

### "The Save button is greyed out when I set up or edit an enrichment"

The Save button stays disabled until all required configuration is in place. The most common causes:

-   **Required input fields are not yet mapped.** Each enrichment has at least one required input field — for example, a company domain enrichment requires a company name input. If a required field hasn't been mapped to a column in your table, the Save button remains disabled. Look for any empty input fields in the enrichment panel and map each one to a column using the column picker (type `/` to open it).
-   **Enrichment column limit reached.** If your table has hit its enrichment column limit, the Save button is disabled for both new and existing enrichment columns. See [Column limits](table-columns-overview.md#column-limits) for how to check your count and free up space.
-   **Integration account not connected.** Some enrichments require an API key or account connection before you can save. Click **+ Add account** in the enrichment panel if no account is connected yet.

### "Is there a way to make one enrichment (column) run only after another has finished?"

You can use a boolean formula to check if an enrichment has finished, then use that in a conditional formula to control when another enrichment runs. [Learn more here](https://www.notion.so/Sources-1577e66eb01480eba5f5dd85343aeb07?pvs=21).

### "How can I tell how my credits are being used?"

You can track credit usage for your workspace in the [credit usage](https://www.clay.com/university/guide/credit-usage) dashboard. This shows detailed breakdowns of credit consumption by table, integration, and time period, helping you monitor and optimize your usage.

### "My enrichment column only ran on the first 10 rows — why didn't it run on all rows?"

There are two common causes:

**New column wizard preview.** When you set up a new enrichment column using the guided wizard, Clay automatically runs the column on the first 10 rows as a quick preview. The remaining rows are not queued and stay blank until you trigger a run manually. The same result occurs if you selected **Save and run 10 rows** from the save dropdown when adding or editing the column.

**Find Companies / Find People / Find Jobs source added to an existing table.** When one of these sources adds rows to an existing table, Clay automatically runs enrichments on only the **first 10 imported rows**, regardless of the table-level auto-run setting. The remaining rows are added to the table but do not trigger auto-run. This is intentional behavior to prevent large, unintended credit burns — a source adding many rows to a table with multiple enrichment columns could otherwise trigger a significant spend all at once. This 10-row cap only applies the first time the source is set up on the existing table; subsequent scheduled runs of the same source will run enrichments on all newly imported rows.

In either case, to process the remaining rows: right-click the enrichment column header and choose **Run column** → **Run N empty or out-of-date rows**.

### "My column is showing AI-generated suggestions instead of actual contact data (phone numbers, email addresses)"

If your column returns paragraphs of advice — such as strategy recommendations or notes like "For large-scale enrichment, use a two-stage approach..." — you added a **Use AI** or **Claygent** column rather than a dedicated data enrichment integration. **Use AI** generates text from the model's training data and does not query external sources. **Claygent** is an AI Web Researcher that can search Google and browse web pages live, but it is not connected to Clay's contact data providers and is not a reliable way to look up real phone numbers or email addresses.

To retrieve actual contact data, add a dedicated enrichment column instead:

-   **Work email addresses** — click `Add enrichment` and select `Work Email`. This pre-built waterfall cascades through multiple email providers in sequence. See [Work Email waterfall](work-email-waterfall.md) for full setup details.
-   **Phone numbers** — click `Add enrichment`, search for `Phone`, and select the waterfall option for your region under **Waterfalls** — `Mobile Phone (US and Canada)`, `Mobile Phone (EMEA)`, `Mobile Phone (APAC)`, or `Mobile Phone (Global)`. See [[Data test] Mobile phone providers by region](data-test-methodology-mobile-phone-region.md) for provider recommendations by region.
-   **Full profile data (job title, company, professional profile URL, and more)** — click `Add enrichment` and search for `Enrich Person` to browse provider-specific integrations. Each provider connects to a different data source — choose the one that fits your needs, or stack several as a [waterfall](building-a-data-waterfall.md) for broader coverage.

### "What accuracy or match rate can I expect from data enrichment in Clay?"

Clay does not publish a single universal accuracy percentage because match rates vary based on several factors:

-   **Data type** — Work emails, personal emails, mobile phone numbers, and company attributes each have different coverage rates.
-   **Geography** — Coverage for contacts in North America typically differs from EMEA or APAC regions.
-   **Input data quality** — More complete inputs (for example, a full name plus a verified company domain) generally produce higher match rates.
-   **Provider selection** — Clay connects to 150+ data providers, each optimized for different data types and regions.

**Using a single enrichment provider** on a challenging dataset typically yields match rates in the 40–60% range. **Using a waterfall** — which chains multiple providers in sequence and stops as soon as one returns a result — significantly increases coverage. For specific numbers by data type, see Clay's published data tests:

-   [[Data test] Personal email providers](data-test-methodology-personal-emails.md) — tested across 2,354 contacts; providers collectively returned emails for 53% of contacts, with 43% confirmed valid.
-   [[Data test] Mobile phone providers by region](data-test-methodology-mobile-phone-region.md) — accuracy and coverage scores across NAMER, EMEA, and APAC.
-   [[Data test] Work email providers](data-test-work-email-providers.md) — confidence scores comparing work email finders across SMB and enterprise datasets.

**Recommendation:** Run a proof-of-concept (POC) test on a sample of your actual accounts or contacts before committing to a full run. Results vary significantly depending on your industry, persona, and geographic mix — testing with your own data gives you the most accurate picture of expected coverage.
