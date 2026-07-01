---
title: Neverbounce integration
description: Email verification and cleaning service ensuring deliverability and
  inbox placement.
last_synced: 2026-04-26T01:40:24.081Z
---

# Neverbounce integration

Email verification and cleaning service ensuring deliverability and inbox placement.

### What is NeverBounce?

NeverBounce in Clay validates work emails to ensure they're safe, reducing bounces, protecting your sender reputation, and improving deliverability.

We'll cover how to connect Clay to NeverBounce, and then we'll go over how to validate an email with NeverBounce.

### Connecting Clay with NeverBounce

NeverBounce is available on all Clay plans using Clay's built-in integration — no API key required to get started. If you want to use your own NeverBounce account, you can optionally connect your own API key through the enrichment panel.

### How do you validate an email with NeverBounce?

Neverbounce's **Validate Email** action helps you determine if the email address you're sending to has a valid inbox. Follow the steps below to validate your emails with NeverBounce.

**Step 1: (Optional) Connect your NeverBounce API key**

If you have your own NeverBounce account, you can add your API key here. Clay's built-in NeverBounce integration is used by default when no key is provided.

**Step 2: Select the email you want to verify**

For this step, input the email address you want to verify

**Step 3 (Optional): Select Auto-update**

By default, NeverBounce will auto-update the integration every 24 hours. Make sure to toggle this step off if you do not want to auto-update. However if you do so, you might run into stale data problems.

**Step 4 (Optional): Select conditional run criteria**

If you want to only run this enrichment under set circumstances, you are able to input formulas where the column runs only if the formula is true. Learn more about conditional runs in [this Clay University lesson](https://www.clay.com/university/lesson/ai-formulas-conditional-runs-clay-101#:~:text=Conditional%20runs%20\(which%20make%20use,personal%20emails%20for%20all%20rows\).\)).

**Step 5: Choose data to add as columns to table**

Select which data from the enrichment you'd like to add as columns to your table. Even if you choose not to add columns at this point, the enriched data will still be available and accessible for later use.
