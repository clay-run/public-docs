---
title: Clearbit integration overview
source_url: https://university.clay.com/docs/clearbit-integration-overview
description: B2B data solutions for lead generation and marketing personalization.
last_synced: 2026-04-27T18:09:36.202Z
upstream_hash: a31a5b247b5c8319e0d2b847867424da5958dd4a18d99f44a7ce985b50f4c140
---

# Clearbit integration overview

B2B data solutions for lead generation and marketing personalization.

# **Getting started with Clearbit**

Clearbit in Clay offers powerful data enrichment actions to retrieve company and person information, including logos, contacts, and domains, based on website domains or email addresses.

There are many actions you can do with Clearbit, including:

-   Find Domain from Company Name
-   Find Logo
-   Enrich Company
-   Enrich Person and Company
-   Find Contacts

We'll cover how to connect Clay to Clearbit, then we'll go over each action that is available with Clearbit.

But first let's talk a bit about data enrichment waterfalls.

## **Getting better email coverage with waterfall enrichments**

Clearbit is great for finding email contacts, but it's not the only way to get this data.

For better coverage on email data, we recommend using [Clay's waterfall enrichments](https://www.clay.com/waterfall-enrichment), which will let you search sequentially across multiple data providers.

Learn more on how to use Clay waterfalls with this [Clay University lesson](https://www.clay.com/university/lesson/enrich-people-waterfalls-clay-101).

That said, let's get into it on how to use Clearbit with Clay!

## **Connecting with Clay with Clearbit**

### **Option 1: Use the Clay-managed Clearbit account**

By default, Clearbit enrichments will use the Clay-managed Clearbit account. This means that any new enrichment will charge the designated credit amount. Simply pull up any Clearbit enrichment within Clay to use the Clay-managed Clearbit account.

### **Option 2: Add your own Clearbit API key**

If you are currently on a paid plan, you can use your own Clearbit account within Clay through an API key.

**Important:** API key usage is only available on paid plans. Please upgrade to access the API key.

For more information on how to find your Clearbit API key, please see reference [Clearbit’s documentation](https://help.clearbit.com/hc/en-us/articles/6045527495191-Access-your-Clearbit-API-key). Please note that API keys are available for Clearbit accounts created in 2023 and earlier. If you signed up in 2024, API keys are not available regardless of plan.

You can add your Clearbit API key through the enrichment panel. Below is an example of where add your API key within the enrichment panel.

### `Action` Find Domain from Company Name

The **Find Domain from Company Name** action helps you find a company’s domain from a given name.

**Step 1: Choose the Clearbit account you want to use**

First, you can use either the Clay-managed Clearbit account or your own API key.

If you use the Clay-managed Clearbit account you won’t be charged any credits.

**Step 2: Enter company name**

Please input the Company Name you want to find the domain for.

**Step 3 (Optional): Select Auto-update**

By default, Clearbit will auto-update the integration every 24 hours. This is optional. Make sure to toggle this step off if you do not want to auto-update, however, you might run into stale data problems.

For more information about how auto-update works, please read [this brief guide](https://docs.clay.com/en/articles/9642165-auto-update-and-auto-dedupe-table).

**Step 4 (Optional): Select conditional run criteria**

If you want to only run this enrichment under set circumstances, you are able to input formulas where the column runs only if the formula is true. Learn more about conditional runs in [this Clay University lesson.](https://www.clay.com/university/lesson/ai-formulas-conditional-runs-clay-101#:~:text=Conditional%20runs%20\(which%20make%20use,personal%20emails%20for%20all%20rows\).\))

**Step 5: Choose data to add as columns to table**

Select which data from the enrichment you’d like to add as columns to your table. Even if you choose not to add columns at this point, the enriched data will still be available and accessible for later use.

### `Action` Find Logo

The **Find Logo** action helps you find a logo of a particular company given a domain.

**Step 1: Enter company domain and specify image size**

Enter the domain of the company you want to find the logo for. Optionally, you are are able to specify the size of the logo, in px, you want Clearbit to provide.

**Step 2 (Optional): Select Auto-update**

By default, Clearbit will auto-update the integration every 24 hours. This is optional. Make sure to toggle this step off if you do not want to auto-update, however, you might run into stale data problems.

For more information about how auto-update works, please read [this brief guide](https://docs.clay.com/en/articles/9642165-auto-update-and-auto-dedupe-table).

**Step 3 (Optional): Select conditional run criteria**

If you want to only run this enrichment under set circumstances, you are able to input formulas where the column runs only if the formula is true. Learn more about conditional runs in [this Clay University lesson.](https://www.clay.com/university/lesson/ai-formulas-conditional-runs-clay-101#:~:text=Conditional%20runs%20\(which%20make%20use,personal%20emails%20for%20all%20rows\).\))

**Step 4: Choose data to add as columns to table**

Select if you want to add the Url of the profile image into your table. Even if you choose not to add the URL column at this point, the enriched data will still be available and accessible for later use.

### `Action` Enrich Company

The **Enrich Company** action helps you get key data about a company given the company website domain.

**Step 1: Choose the Clearbit account you want to use**

First, you can use either the Clay-managed Clearbit account or your own API key.

If you use the Clay-managed Clearbit account you will be charged at 8 credits per enriched cell. For more information on how Clay credits work, please refer to [this guide](https://www.clay.com/university/lesson/clay-credits-overview).

**Step 2: Enter optional and required setup inputs**

Please input the domain of the company which you are trying to enrich.

If you want to ensure you are enriching the right company, you can also add the LinkedIn URL, Twitter URL, Facebook URL, and Company Name.

**Step 3 (Optional): Select Auto-update**

By default, Clearbit will auto-update the integration every 24 hours. This is optional. Make sure to toggle this step off if you do not want to auto-update, however, you might run into stale data problems.

For more information about how auto-update works, please read [this brief guide](https://docs.clay.com/en/articles/9642165-auto-update-and-auto-dedupe-table).

**Step 4 (Optional): Select conditional run criteria**

If you want to only run this enrichment under set circumstances, you are able to input formulas where the column runs only if the formula is true. Learn more about conditional runs in [this Clay University lesson.](https://www.clay.com/university/lesson/ai-formulas-conditional-runs-clay-101#:~:text=Conditional%20runs%20\(which%20make%20use,personal%20emails%20for%20all%20rows\).\))

**Step 5: Choose data to add as columns to table**

Select which data from the enrichment you’d like to add as columns to your table. Even if you choose not to add columns at this point, the enriched data will still be available and accessible for later use.

### `Action` Enrich Person & Company

The **Enrich Person & Company** action helps you find key data about a person and their current company from a given work email.

**Step 1: Choose the Clearbit account you want to use**

First, you can use either the Clay-managed Clearbit account or your own API key.

If you use the Clay-managed Clearbit account you will be charged at 8 credits per enriched cell. For more information on how Clay credits work, please refer to [this guide](https://www.clay.com/university/lesson/clay-credits-overview).

**Step 2: Enter optional and required setup inputs**

Please input the work email of the person and their company you are trying to enrich. Make sure this is a work email address.

**Step 3 (Optional): Select Auto-update**

By default, Clearbit will auto-update the integration every 24 hours. This is optional. Make sure to toggle this step off if you do not want to auto-update, however, you might run into stale data problems.

For more information about how auto-update works, please read [this brief guide](https://docs.clay.com/en/articles/9642165-auto-update-and-auto-dedupe-table).

**Step 4 (Optional): Select conditional run criteria**

If you want to only run this enrichment under set circumstances, you are able to input formulas where the column runs only if the formula is true. Learn more about conditional runs in [this Clay University lesson.](https://www.clay.com/university/lesson/ai-formulas-conditional-runs-clay-101#:~:text=Conditional%20runs%20\(which%20make%20use,personal%20emails%20for%20all%20rows\).\))

**Step 5: Choose data to add as columns to table**

Select which data from the enrichment you’d like to add as columns to your table. Even if you choose not to add columns at this point, the enriched data will still be available and accessible for later use.

### `Action` Find Contacts

The **Find Contacts** action helps you find contacts that work for a company given company domain.

**Step 1: Select Clearbit account**

Please enter your the Clearbit account you want to use. Note that for this action, there is no Clay-managed account.For more information on how to access your Clearbit API Key, please reference [Clearbit’s API documentation](https://help.clearbit.com/hc/en-us/articles/6045527495191-Access-your-Clearbit-API-key).

**Step 2: Enter optional and required setup inputs**

Please input the domain you are trying to find contacts from.

Additionally, adding the name, roles, titles, and other information can help you narrow your search. You can also limit the amount of searches run on your Clearbit account.

**Step 3 (Optional): Select Auto-update**

By default, Clearbit will auto-update the integration every 24 hours. This is optional. Make sure to toggle this step off if you do not want to auto-update, however, you might run into stale data problems.

For more information about how auto-update works, please read [this brief guide](https://docs.clay.com/en/articles/9642165-auto-update-and-auto-dedupe-table).

**Step 4 (Optional): Select conditional run criteria**

If you want to only run this enrichment under set circumstances, you are able to input formulas where the column runs only if the formula is true. Learn more about conditional runs in [this Clay University lesson.](https://www.clay.com/university/lesson/ai-formulas-conditional-runs-clay-101#:~:text=Conditional%20runs%20\(which%20make%20use,personal%20emails%20for%20all%20rows\).\))

**Step 5: Choose data to add as columns to table**

Select which data from the enrichment you’d like to add as columns to your table. Even if you choose not to add columns at this point, the enriched data will still be available and accessible for later use.
