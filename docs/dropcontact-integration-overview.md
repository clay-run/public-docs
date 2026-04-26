---
title: DropContact integration overview
source_url: https://university.clay.com/docs/dropcontact-integration-overview
description: B2B email finder to find emails, enrich contacts, validate data,
  and clean duplicates.
last_synced: 2026-04-26T01:39:54.261Z
upstream_hash: 8c3a7623a6a1fe2bfe5e66a5a8dcce5cb4b60463ea5efd0e593e2a48f9612009
---

# DropContact integration overview

B2B email finder to find emails, enrich contacts, validate data, and clean duplicates.

## Get started with DropContact

[DropContact](#) in Clay allows you to find work email addresses and company names from domain names, streamlining your contact research process.

There are two actions you can perform with [DropContact](https://www.clay.com/integrations/data-provider/dropcontact):

-   Find Work Email
-   Find Company Name from Company Domain

We'll cover how to connect Clay to DropContact, then we'll go over each action that is available with DropContact.

But first let's talk a bit about data enrichment waterfalls.

## Getting better email coverage with waterfall enrichments

[DropContact](https://www.clay.com/integrations/data-provider/dropcontact) is great for finding email contacts, but it's not the only way to get email data.

For better coverage on email data, we recommend using [Clay's waterfall enrichments](https://www.clay.com/waterfall-enrichment), which will let you search sequentially across multiple data providers. Learn more on how to use Clay waterfalls with this [Clay University lesson](https://www.clay.com/university/lesson/enrich-people-waterfalls-clay-101).

That said, let's get into it on how to use DropContact with Clay! 

## Connecting with Clay with DropContact

You have two options to connect DropContact with Clay.

### Option 1: Use the Clay-managed DropContact account

By default, DropContact enrichments will use the Clay-managed DropContact account. This means that any new enrichment will charge the designated credit amount.

Simply pull up any DropContact enrichment within Clay to use the Clay-managed DropContact account.

### Option 2: Add your own DropContact API key

If you are currently on a paid plan, you can use your own DropContact account within Clay through an API key.

You can add your own API key for any DropContact enrichment when selecting an account within the enrichment panel.

Below is an example of where to click within the enrichment panel to add your API key. For more instructions on how to find your DropContact API key, [follow these instructions](https://support.dropcontact.com/article/237-how-to-use-the-dropcontact-api-key) within DropContact's documentation.

## `Action` Find Work Email

The **Find Work Email** action allows for you to find a person's email address with a company domain, phone number, or social URL.

**Step 1: Choose the Dropcontact account you want to use**  
You can use either the Clay-managed Dropcontact account or bring your own key.  
If you use the Clay-managed Dropcontact account you will be charged at 2 credits per enriched cell.

**Step 2: Select Inputs to provide**  
Make the to provide the inputs to Dropcontact. Please note that while all the inputs are optional, the data quality will improve with the amount of data you put in.  
As a rule of thumb, inputting more unique identifiers will help improve data quality.

**Step 3 (Optional): Select Auto-update**  
By default, Dropcontact will auto-update the integration every 24 hours. Make sure to toggle this step off if you do not want to auto-update. However if you do so, you might run into stale data problems.

**Step 4 (Optional): Select Conditional Run Criteria**  
If you want to only run this enrichment under set circumstances, you are able to input formulas where the column runs only if the formula is true. Learn more about conditional runs in [this Clay University lesson](https://www.clay.com/university/lesson/ai-formulas-conditional-runs-clay-101#:~:text=Conditional%20runs%20\(which%20make%20use,personal%20emails%20for%20all%20rows\).).

## `Action` Find Company Name from Company Domain

The **Find Company Name from Company Domain** action helps you search for a company's name from a given domain.

**Step 1: Choose the Dropcontact account you want to use**  
You can use either the Clay-managed Dropcontact account or bring your own key.  
If you use the Clay-managed Dropcontact account you will be charged at 2 credits per enriched cell.

**Step 2: Select Company Domain as input**  
Enter the company domain to receive the company name as the output.

**Step 3 (Optional): Select Auto-update**  
By default, Dropcontact will auto-update the integration every 24 hours. Make sure to toggle this step off if you do not want to auto-update. However if you do so, you might run into stale data problems.

**Step 4 (Optional): Select Conditional Run Criteria**  
If you want to only run this enrichment under set circumstances, you are able to input formulas where the column runs only if the formula is true. Learn more about conditional runs in [this Clay University lesson](https://www.clay.com/university/lesson/ai-formulas-conditional-runs-clay-101#:~:text=Conditional%20runs%20\(which%20make%20use,personal%20emails%20for%20all%20rows\).).
