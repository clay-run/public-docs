---
title: Enrichments
source_url: https://university.clay.com/docs/enrichments
description: Learn how to run enrichments in Clay, including run settings, delay options, and custom rate limits.
last_synced: 2026-04-26T01:39:56.840Z
---

# Enrichments

Learn how to run an enrichment within Clay.

Enrichments in Clay transform your data by pulling in additional information from various sources. Whether you need to verify email addresses, gather company details, or find social media profiles, Clay's enrichment tools enhance your data quickly and efficiently.

You can run enrichments individually, use pre-built templates, or create powerful recipes to automate complex workflows.

## Running an enrichment

1.  In a Clay table, click `Add enrichment` and search for an enrichment.
2.  Under `Integrations`, select an option.
3.  In the modal, select your account.
    -   Clay provides API keys for certain enrichments, but you can save [credits](https://www.clay.com/university/guide/credits) by using your own account—click `+ Add account` to set it up.

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

## Custom rate limit

Limit how many requests Clay sends to an external service within a given time window. This is useful when you need to stay within an API provider's rate limits while running enrichments at scale.

When supported by an enrichment, a **Custom rate limit** collapsible section appears at the bottom of the enrichment settings panel.

-   **Request limit** — The maximum number of requests to send within the time window.
-   **Duration (in ms)** — The length of the time window in milliseconds (between 1 and 900,000 ms / up to 15 minutes).

The request limit and duration together must average at least 1 request per second (for example, 60 requests per 60,000 ms is valid; 1 request per 2,000 ms is also valid).

**Note:** Custom rate limit is not available for Clay's built-in AI enrichments (Use AI, Claygent, etc.). It only appears for enrichments that support custom rate limiting, such as HTTP API and Apollo OAuth enrichments.

## Troubleshooting

### "Is there a way to make one enrichment (column) run only after another has finished?"

You can use a boolean formula to check if an enrichment has finished, then use that in a conditional formula to control when another enrichment runs. [Learn more here](https://www.notion.so/Sources-1577e66eb01480eba5f5dd85343aeb07?pvs=21).

### "How can I tell how my credits are being used?"

You can track credit usage for your workspace in the [credit usage](https://www.clay.com/university/guide/credit-usage) dashboard. This shows detailed breakdowns of credit consumption by table, integration, and time period, helping you monitor and optimize your usage.

### "My enrichment column only ran on the first 10 rows — why didn't it run on all rows?"

When you set up a new enrichment column using the guided wizard, Clay automatically runs the column on the first 10 rows as a quick preview. The remaining rows are not queued and stay blank until you trigger a run manually. The same result occurs if you selected **Save and run 10 rows** from the save dropdown when adding or editing the column.

To run the column on all remaining rows, right-click the column header and choose **Run column** → **Run N empty or out-of-date rows**.
