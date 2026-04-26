---
title: Mixrank integration overview
source_url: https://university.clay.com/docs/mixrank-integration-overview
description: High-frequency data platform for sales, marketing, and investment insights.
last_synced: 2026-04-26T01:40:23.112Z
upstream_hash: f5dfa422ae8f6dde9de5f9f3b972f6263ab784595a0e2481286efb91091de6c4
---

# Mixrank integration overview

High-frequency data platform for sales, marketing, and investment insights.

## **Getting started with Mixrank**

[Mixrank](https://www.clay.com/integrations/data-provider/mixrank) in Clay allows users to enrich a person's profile using their email address or find their personal email address from their LinkedIn or Twitter profiles.

There are two actions you can do with [Mixrank](https://www.clay.com/integrations/data-provider/mixrank), including:

-   Enrich Person from Email
-   Find Personal Email

We'll cover how to connect Clay to Mixrank, then we'll go over each action that is available with Mixrank.

But first let's talk a bit about data enrichment waterfalls.

## **Getting better email coverage with waterfall enrichments**

Mixrank is great for finding email contacts, but it's not the only way to get this data.

For better coverage on email data, we recommend using [Clay's waterfall enrichments](https://www.clay.com/waterfall-enrichment), which will let you search sequentially across multiple data providers.

Learn more on how to use Clay waterfalls with this [Clay University lesson](https://www.clay.com/university/lesson/enrich-people-waterfalls-clay-101).

That said, let's get into it on how to use Mixrank with Clay!

## **Connecting with Clay with Mixrank**

By default, all Mixrank actions within Clay are handled through your Clay account. There’s no need to set up an additional Mixrank account or input an API key.

Each Mixrank action will deduct two credits from your Clay account.

### `Action` Enrich Person from Email

The **Enrich Person from Email** action enriches a person using a personal or work email address.

**Step 1: Enter email address**

Please enter the email address of the person you are trying to enrich

**Step 2 (Optional): Select Auto-update**

By default, Mixrank will auto-update the integration every 24 hours. This is optional. Make sure to toggle this step off if you do not want to auto-update, however, you might run into stale data problems.

For more information about how auto-update works, please read [this brief guide](https://docs.clay.com/en/articles/9642165-auto-update-and-auto-dedupe-table).

**Step 3 (Optional): Select conditional run criteria**

If you want to only run this enrichment under set circumstances, you are able to input formulas where the column runs only if the formula is true. Learn more about conditional runs in [this Clay University lesson](https://www.clay.com/university/lesson/ai-formulas-conditional-runs-clay-101#:~:text=Conditional%20runs%20\(which%20make%20use,personal%20emails%20for%20all%20rows\).\)).

**Step 4: Choose data to add as columns to table**

Select which data from the enrichment you’d like to add as columns to your table. Even if you choose not to add columns at this point, the enriched data will still be available and accessible for later use.

### `Action` Find Personal Email

The **Find Personal Email** action helps you find a person’s personal email address using their LinkedIn URL or Twitter Profile.

**Step 1: Enter either Social URL (LinkedIn) or Twitter URL**

Enter either the LinkedIn or Twitter URL of the person whose personal email address you are trying to find.

**Step 2 (Optional): Select Auto-update**

By default, Mixrank will auto-update the integration every 24 hours. This is optional. Make sure to toggle this step off if you do not want to auto-update, however, you might run into stale data problems.

For more information about how auto-update works, please read [this brief guide](https://docs.clay.com/en/articles/9642165-auto-update-and-auto-dedupe-table).

**Step 3 (Optional): Select conditional run criteria**

If you want to only run this enrichment under set circumstances, you are able to input formulas where the column runs only if the formula is true. Learn more about conditional runs in [this Clay University lesson](https://www.clay.com/university/lesson/ai-formulas-conditional-runs-clay-101#:~:text=Conditional%20runs%20\(which%20make%20use,personal%20emails%20for%20all%20rows\).\)).

**Step 4: Choose data to add as columns to table**

Select which data from the enrichment you’d like to add as columns to your table. Even if you choose not to add columns at this point, the enriched data will still be available and accessible for later use.
