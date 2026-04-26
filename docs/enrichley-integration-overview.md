---
title: Enrichley integration overview
source_url: https://university.clay.com/docs/enrichley-integration-overview
last_synced: 2026-04-26T01:39:56.199Z
upstream_hash: 251dedbe80e8bdce802187bc7e0446c9da109cb1f3018498c0e23288875676bd
---

# Enrichley integration overview

Verify and validate risky emails to ensure accuracy and deliverability.

### What is Enrichley?

Enrichley in Clay validates work emails to ensure they’re safe, reducing bounces, protecting your sender reputation, and improving deliverability.

We'll cover how to connect Clay to Enrichley, and then we'll go over how to validate an email with Enrichley.

### Connecting Clay with Enrichley

There are two options to connect Enrichley to Clay.

### Option 1: Use the Clay-managed Enrichley account

By default, Enrichley enrichments will use the Clay-managed Enrichley account. This means that any new enrichment will charge the 1 credit

Simply pull up any Enrichley enrichment within Clay to use the Clay-managed Enrichley account.

### Option 2: Use your own Enrichley API key

If you are currently on a paid plan, you can use your own Enrichley account within Clay through an API key.

**Important:** API key usage is only available on paid plans. Please upgrade to access the API key.

You can add your Enrichley API key to Clay within the enrichment panel. Below is an example of where to add your API key.

### How do you use Enrichley to validate your emails?

Enrichley’s **Validate Email** action helps you determine if the email address you’re sending to has a valid inbox. Follow the steps below to validate your emails with Enrichley.

**Step 1: Select input Enrichley API key to create account**

You can use either the Clay-managed Enrichley account or bring your own key.

If you use the Clay-managed Enrichley account, you will be charged at 1 credit per enriched cell.

**Step 2: Select the email you want to verify**

For this step, input the email address you want to verify

**Step 3 (Optional): Select Auto-update**

By default, Enrichley will auto-update the integration every 24 hours. Make sure to toggle this step off if you do not want to auto-update. However if you do so, you might run into stale data problems.

**Step 4 (Optional): Select conditional run criteria**

If you want to only run this enrichment under set circumstances, you are able to input formulas where the column runs only if the formula is true. Learn more about conditional runs in [this Clay University lesson](https://www.clay.com/university/lesson/ai-formulas-conditional-runs-clay-101#:~:text=Conditional%20runs%20\(which%20make%20use,personal%20emails%20for%20all%20rows\).).

**Step 5: Choose data to add as columns to table**

Select which data from the enrichment you’d like to add as columns to your table. Even if you choose not to add columns at this point, the enriched data will still be available and accessible for later use.
