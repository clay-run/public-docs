---
title: Waterfalls
source_url: https://university.clay.com/docs/building-a-data-waterfall
description: Maximize your data coverage with waterfalls.
last_synced: 2026-04-27T18:09:26.920Z
---

# Waterfalls

Maximize your data coverage with waterfalls.

Waterfalls allow you to utilize multiple data providers in a predetermined sequence, so you don't duplicate tasks or spend extra credits.

## Using pre-built waterfalls

To run a pre-built waterfall:

1.  Click `Add enrichment` on the top right corner of your table and search for the data point you want to run a waterfall for (ex. Phone number). Under `Waterfalls`, select the waterfall you want to run.
2.  Configure your `Waterfall sequence`. You can reorder, add. or delete your waterfall data providers.
    -   To skip a step in the waterfall, click the toggle switch next to a specific provider.
3.  Enter the required data inputs, such as email addresses or social profile URLs, to set up the enrichment waterfall.
4.  In the **Waterfall output** dropdown, select which sub-field to display in the waterfall's merged column (for example, `people > 0 > title`). You can only pick one field at a time — but all individual provider columns are still added to your table with their full data regardless of which field you select. You can access any field from a provider column by clicking into a row or referencing it in a formula.
5.  Optionally, choose to output the name of the successful provider and hide the provider columns for a cleaner table view.
6.  Configure Run settings, including enabling auto-update or setting conditions for when the waterfall should run.

## Creating a waterfall

1.  While in a table, click `Add column` (which you will find at the far right side).
2.  Select `Waterfall` and click the `🖊️` to next to the title to rename.
3.  Change the `Data Type` that you'll be working with.
4.  Add actions to the waterfall and adjust other settings.
5.  Click `Save`.

## Creating a waterfall template

Waterfall templates allow you to save and reuse your waterfall configuration, making it easier to standardize and replicate successful workflows.

1.  While creating a waterfall, select `Save as template`.
2.  Give your template a name, description, and category.
3.  Select `Save template`.

**Note:** Waterfall templates cannot be edited, only created and deleted.

## Trial plan and provider restrictions

Waterfall enrichments are available on all plans, including the Trial plan. However, some individual providers within a waterfall require a paid plan.

Providers that can return phone numbers — such as PDL (People Data Labs), Bytemine, and others — require the Launch plan or higher. When a waterfall template includes one or more of these providers, Trial users see the error:

> Your subscription does not allow this integration to be added.

This error can appear even when your goal is to find something other than a phone number (for example, a LinkedIn URL), because the provider is phone-number gated regardless of which output you're looking for.

**To work around this on a Trial plan:** open the waterfall's `Waterfall sequence` configuration and remove any providers that return phone numbers. The remaining providers will work normally. To use all providers without restriction, upgrade to a paid plan.
