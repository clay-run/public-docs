---
title: Hunter
source_url: https://university.clay.com/docs/hunter-integration-overview
description: Email outreach platform.
last_synced: 2026-04-26T01:40:09.700Z
upstream_hash: fe98b3bee8de066ccfce924ff294e7c5258bac003fb2edc4756afb1b47eddb61
---

# Hunter

Email outreach platform.

## Getting started with Hunter.io

[Hunter.io](https://www.clay.com/integrations/data-provider/hunter) helps you easily find and validate email addresses for individuals and companies, including filtering by department, all within Clay.

You can do a few things with [Hunter.io](http://hunter.io/) within Clay, including:

-   Find Emails by Company
-   Find Work Email
-   Validate Email

We'll cover how to connect Clay to Hunter. Then we'll go over each action that is available with Hunter.

But first, let's talk a little bit about data enrichment waterfalls.

## Maximize your data coverage with waterfall enrichment

[Hunter.io](https://www.clay.com/integrations/data-provider/hunter) is an amazing product for finding and verifying someone's email address. However, it's important to know it's not your only option for email enrichment.

We recommend using [Clay's waterfall data enrichment](https://www.clay.com/waterfall-enrichment) to find and verify someone's email address. This allows you to try multiple providers sequentially to maximize your data coverage.

Learn more in this Clay University lesson on [how to use Clay waterfalls.](https://www.clay.com/university/lesson/enrich-people-waterfalls-crm-enrichment)

That said, let's get into it on how to use Hunter.io with Clay!

## Connecting Clay to Hunter.io

You have two options connecting Hunter to Clay.

### Option 1: Use the Clay-managed Hunter account

This means you do not need to have a Hunter account to use the enrichment. You will be charged 2 credits per enriched cell without any need to create a Hunter account.

When you pull up the enrichment you will simply select the option for `Clay-managed Hunter account`. And you can now use the enrichment!

### Option 2: Add your own Hunter API key

Alternatively, if you already have a Hunter account, you can connect that by adding your own API key. However, it's only available for paying customers.

**Heads up!** You'll need [Clay's Starter plan ($149/mo)](https://www.clay.com/university/guide/hunter-integration-overview#) to use your own Hunter API key. It's not accessible on the free plan.

Follow this interactive tutorial with instructions on how to do that:

You can find additional instructions on [how to find your Hunter API key](https://help.hunter.io/en/articles/1970978-what-is-and-where-i-can-find-my-api-secret-key) in their help documentation.

Next, let's learn more about the actions available with the Hunter integration.

## `Action`Find Emails by Company

The **Find Emails by Company** action helps you find public email addresses on the internet from a company domain with the ability to filter by department.

**Step 1: Choose the Hunter account you want to use**

First, you can use either the Clay-managed Hunter.io account or your own API key.

If you use the Clay-managed Hunter account you will be charged at 2 credits per enriched cell. For more information on how Clay credits work, please refer to [this guide](https://docs.clay.com/en/articles/9654103-how-clay-credits-work).

**Step 2: Select what emails you'd like to find within a company**

Next, you'll select the company domain so you can identify people from that organization. Optionally, you can then select what department you'd like to search to find people.

Follow the step-by-step walkthrough in this interactive lesson for an example:

**Step 3 (Optional): Select Auto-update**

By default, Hunter will auto-update the integration every 24 hours. This is optional. Make sure to toggle this step off if you do not want to auto-update, however, you might run into stale data problems.  

For more information about how auto-update works, please read [this brief guide](https://docs.clay.com/en/articles/9642165-auto-update-and-auto-dedupe-table).

**Step 4 (Optional): Select Conditional Run Criteria**

If you want to only run this enrichment under set circumstances, you are able to input formulas where the column runs only if the formula is true. Learn more about conditional runs in [this Clay University lesson](https://www.clay.com/university/lesson/ai-formulas-conditional-runs-clay-101#:~:text=Conditional%20runs%20\(which%20make%20use,personal%20emails%20for%20all%20rows\).).

## `Action` Find Work Email

The **Find Work Email** action helps you find a person's email address from their name and company domain.

**Step 1: Choose the Hunter account you want to use**

First, you can use either the Clay-managed Hunter.io account or your own API key.

If you use the Clay-managed Hunter account you will be charged at 2 credits per enriched cell. For more information on how Clay credits work, please refer to [this guide](https://docs.clay.com/en/articles/9654103-how-clay-credits-work).

**Step 2: Select the individual's full name and domain of the company**

Enter the Company Domain and the full name of the contact you are performing the email search on.

**Step 3 (Optional): Select Auto-update**

By default, Hunter will auto-update the integration every 24 hours. This is optional. Make sure to toggle this step off if you do not want to auto-update, however, you might run into stale data problems.  

For more information about how auto-update works, please read [this brief guide](https://docs.clay.com/en/articles/9642165-auto-update-and-auto-dedupe-table).

**Step 4 (Optional): Select Conditional Run Criteria**

If you want to only run this enrichment under set circumstances, you are able to input formulas where the column runs only if the formula is true. Learn more about conditional runs in [this Clay University lesson](https://www.clay.com/university/lesson/ai-formulas-conditional-runs-clay-101#:~:text=Conditional%20runs%20\(which%20make%20use,personal%20emails%20for%20all%20rows\).).

## `Action` Validate Email

The **Validate Email** action helps you determine if an email address has as valid inbox.

**Step 1: Choose the Hunter account you want to use**

First, you can use either the Clay-managed Hunter.io account or your own API key.

If you use the Clay-managed Hunter account you will be charged at 2 credits per enriched cell. For more information on how Clay credits work, please refer to [this guide](https://docs.clay.com/en/articles/9654103-how-clay-credits-work).

**Step 2: Select the email address you want to verify**

Enter the Email Address you want to verify. Please make sure it follows the format of [name@email.com](mailto:name@email.com)

**Step 3 (Optional): Select Auto-update**

By default, Hunter will auto-update the integration every 24 hours. Make sure to toggle this step off if you do not want to auto-update, however, you might run into stale data problems.

**Step 4 (Optional): Select Conditional Run Criteria**

If you want to only run this enrichment under set circumstances, you are able to input formulas where the column runs only if the formula is true. Learn more about conditional runs in [this Clay University lesson](https://www.clay.com/university/lesson/ai-formulas-conditional-runs-clay-101#:~:text=Conditional%20runs%20\(which%20make%20use,personal%20emails%20for%20all%20rows\).).
