---
title: Enrichments
source_url: https://university.clay.com/docs/enrichments
description: Learn how to run an enrichment within Clay.
last_synced: 2026-04-26T01:39:56.840Z
upstream_hash: f18039c811ec06bcc928bd67fe45fec9253a88675a4f5b5475813ba887e3cdf6
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

## Troubleshooting

### "Is there a way to make one enrichment (column) run only after another has finished?"

You can use a boolean formula to check if an enrichment has finished, then use that in a conditional formula to control when another enrichment runs. [Learn more here](https://www.notion.so/Sources-1577e66eb01480eba5f5dd85343aeb07?pvs=21).

### "How can I tell how my credits are being used?"

You can track credit usage for your workspace in the [credit usage](https://www.clay.com/university/guide/credit-usage) dashboard. This shows detailed breakdowns of credit consumption by table, integration, and time period, helping you monitor and optimize your usage.
