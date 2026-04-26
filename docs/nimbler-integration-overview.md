---
title: Nimbler integration overview
source_url: https://university.clay.com/docs/nimbler-integration-overview
last_synced: 2026-04-26T01:40:24.731Z
upstream_hash: 26c927db1c6eb34fbd66d90da925673d15409c360b5a27f1bfd34463d1b9dfe3
---

# Nimbler integration overview

Enrich data, find contacts, and search by job or industry.

## Getting started with Nimbler

[Nimbler](https://www.clay.com/integrations/data-provider/nimbler) in Clay offers a suite of tools to search for individuals based on job titles or industries.

With in Clay, you can use [Nimbler](https://www.clay.com/integrations/data-provider/nimbler) to:

-   Find Mobile Number
-   Find Personal Email
-   Find Work Email

We'll cover how to connect Clay to Nimbler, then we'll go over each action that is available with Nimbler.

But first let's talk a bit about data enrichment waterfalls.

## Getting better email and phone number coverage with waterfall enrichments

Nimbler is great for finding email and phone number contacts, but it's not the only way to get this data.

For better coverage on email address and phone number data, we recommend using [Clay's waterfall enrichments](https://www.clay.com/waterfall-enrichment), which will let you search sequentially across multiple data providers. Learn more on how to use Clay waterfalls with this [Clay University lesson](https://www.clay.com/university/lesson/enrich-people-waterfalls-clay-101).

That said, let's get into it on how to use Nimbler with Clay!

## Connecting with Clay with Nimbler

You have two options to connect Nimbler with Clay.

### Option 1: Use the Clay-managed Nimbler account

By default, Nimbler enrichments will use the Clay-managed Nimbler account. This means that any new enrichment will charge the designated credit amount.

Simply pull up any Nimbler enrichment within Clay to use the Clay-managed Nimbler account.

### Option 2: Add your own Nimbler API key

If you are currently on a paid plan, you can use your own Nimbler account within Clay through an API key.

To add your own API key for any Nimbler enrichment, you can do so when you're selecting an account.

Below is an example of where to click within the enrichment panel to add your API key. For more instructions on how to find your Nimbler API key, [follow these instructions](https://datagmaapi.readme.io/reference/getting-started-with-your-api) within Nimbler's documentation.

## `Action` Find Mobile Number

The **Find Mobile Number** action lets you use LinkedIn URL, Work Email Address, or Company Name and Full Name to find someone's mobile number and other contact data.

**Step 1: Choose the Nimbler account you want to use**  
You can use either the Clay-managed Nimbler account or bring your own key.  
If you use the Clay-managed Nimbler account you will be charged at 2 credit per enriched cell.

**Step 2: Select and enter Setup Inputs**  
Use LinkedIn URL, Work Email Address, or Company Name and Full Name to find someone's mobile number and other contact data.

**Step 3 (Optional): Select Auto-update**  
By default, Nimbler will auto-update the integration every 24 hours. Make sure to toggle this step off if you do not want to auto-update. However if you do so, you might run into stale data problems.

**Step 4 (Optional): Select Conditional Run Criteria**  
If you want to only run this enrichment under set circumstances, you are able to input formulas where the column runs only if the formula is true. Learn more about conditional runs in [this Clay University lesson](https://www.clay.com/university/lesson/ai-formulas-conditional-runs-clay-101#:~:text=Conditional%20runs%20\(which%20make%20use,personal%20emails%20for%20all%20rows\).).

## `Action` Find Personal Email

The **Find Personal Email** action lets you use LinkedIn URL, Email Address, or Company Name and Full Name to find someone's personal email and other contact data.

**Step 1: Choose the Nimbler account you want to use**  
You can use either the Clay-managed Nimbler account or bring your own key.  
If you use the Clay-managed Nimbler account you will be charged at 2 credit per enriched cell.

**Step 2: Select and enter Setup Inputs**  
Use LinkedIn URL, Email Address, or Company Name and Full Name to find someone's personal email and other contact data.

**Step 3 (Optional): Select Auto-update**  
By default, Nimbler will auto-update the integration every 24 hours. Make sure to toggle this step off if you do not want to auto-update. However if you do so, you might run into stale data problems.

**Step 4 (Optional): Select Conditional Run Criteria**  
If you want to only run this enrichment under set circumstances, you are able to input formulas where the column runs only if the formula is true. Learn more about conditional runs in [this Clay University lesson](https://www.clay.com/university/lesson/ai-formulas-conditional-runs-clay-101#:~:text=Conditional%20runs%20\(which%20make%20use,personal%20emails%20for%20all%20rows\).).

## `Action` Find Work Email

The **Find Work Email** action lets you use a contacts LinkedIn URL or Company Name and Full Name to find someone's work email and other contact data.

**Step 1: Choose the Nimbler account you want to use**  
You can use either the Clay-managed Nimbler account or bring your own key.  
If you use the Clay-managed Nimbler account you will be charged at 2 credit per enriched cell.

**Step 2: Select and enter Setup Inputs**  
Use LinkedIn URL or Company Name and Full Name to find someone's work email and other contact data.

**Step 3 (Optional): Select Auto-update**  
By default, Nimbler will auto-update the integration every 24 hours. Make sure to toggle this step off if you do not want to auto-update. However if you do so, you might run into stale data problems.

**Step 4 (Optional): Select Conditional Run Criteria**  
If you want to only run this enrichment under set circumstances, you are able to input formulas where the column runs only if the formula is true. Learn more about conditional runs in [this Clay University lesson](https://www.clay.com/university/lesson/ai-formulas-conditional-runs-clay-101#:~:text=Conditional%20runs%20\(which%20make%20use,personal%20emails%20for%20all%20rows\).).
