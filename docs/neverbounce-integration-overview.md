---
title: Neverbounce integration
source_url: https://university.clay.com/docs/neverbounce-integration-overview
last_synced: 2026-04-26T01:40:24.081Z
upstream_hash: cebac03fa2f67c637d6ffc20717cb573ce9a3f471fd53a61f45b556386dd1a66
---

# Neverbounce integration

Email verification and cleaning service ensuring deliverability and inbox placement.

### What is NeverBounce?

NeverBounce in Clay validates work emails to ensure they’re safe, reducing bounces, protecting your sender reputation, and improving deliverability.

We'll cover how to connect Clay to RocketReach, and then we'll go over how to validate an email with NeverBounce.

### Connecting Clay with NeverBounce

**Important:** API key usage is only available on paid plans. Please upgrade to access the API key.

You can add your NeverBounce API key to Clay within the enrichment panel. Below is an example of where to add your API key within the enrichment panel.

### How do you validate an email with NeverBounce?

Neverbounce’s **Validate Email** action helps you determine if the email address you’re sending to has a valid inbox. Follow the steps below to validate your emails with NeverBounce.

**Step 1: Select input NeverBounce API key to create account**

If you haven’t already created a NeverBounce account within Clay, you can add an API key tied to an account. Note that you must bring your own API key for this step

**Step 2: Select the email you want to verify**

For this step, input the email address you want to verify

**Step 3 (Optional): Select Auto-update**

By default, NeverBounce will auto-update the integration every 24 hours. Make sure to toggle this step off if you do not want to auto-update. However if you do so, you might run into stale data problems.

**Step 4 (Optional): Select conditional run criteria**

If you want to only run this enrichment under set circumstances, you are able to input formulas where the column runs only if the formula is true. Learn more about conditional runs in [this Clay University lesson](https://www.clay.com/university/lesson/ai-formulas-conditional-runs-clay-101#:~:text=Conditional%20runs%20\(which%20make%20use,personal%20emails%20for%20all%20rows\).\)).

**Step 5: Choose data to add as columns to table**

Select which data from the enrichment you’d like to add as columns to your table. Even if you choose not to add columns at this point, the enriched data will still be available and accessible for later use.
