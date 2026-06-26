---
title: Prospeo integration overview
description: Find work emails and enrich person details using name, domain, or LinkedIn.
last_synced: 2026-04-26T01:40:30.619Z
---

# Prospeo integration overview

Find work emails and enrich person details using name, domain, or LinkedIn.

## Getting started with Prospeo

[Prospeo](https://www.clay.com/integrations/data-provider/prospeo) in Clay allows you to find work email addresses and enrich person details using a person's name, company domain, or LinkedIn URL.

Clay's Prospeo integration includes the following actions:

-   Find Work Email
-   Find Email Addresses Associated with a Domain
-   Find Work Email and Enrich Person from LinkedIn URL
-   Find people at company

We'll cover how to connect Clay to Prospeo, then we'll go over each action that is available with Prospeo.

But first let's talk a bit about data enrichment waterfalls.

## Getting better email coverage with waterfall enrichments

Prospeo is great for finding email contacts, but it's not the only way to get this data.

For better coverage on email data, we recommend using [Clay's waterfall enrichments](https://www.clay.com/waterfall-enrichment), which will let you search sequentially across multiple data providers. Learn more on how to use Clay waterfalls with this [Clay University lesson](https://www.clay.com/university/lesson/enrich-people-waterfalls-clay-101).

That said, let's get into it on how to use Prospeo with Clay!

## Connecting with Clay with Prospeo

You have two options to connect Prospeo with Clay.

### Option 1: Use the Clay-managed Prospeo account

By default, Prospeo enrichments will use the Clay-managed Prospeo account. This means that any new enrichment will charge the designated credit amount.

Simply pull up any Datagma enrichment within Clay to use the Clay-managed Prospeo account.

### Option 2: Add your own Prospeo API key

If you are currently on paid plan (Starter, Explorer, Pro) you can use your own Prospeo account within Clay through an API key.

To add your own API key for any Prospeo enrichment, you can do so when you're selecting an account.

Below is an example of where to click within the enrichment panel to add your API key. For more instructions on how to find your Prospeo API key, [follow these instructions](https://datagmaapi.readme.io/reference/getting-started-with-your-api) within Prospeo's documentation.

**Note:** When you use your own Prospeo API key, each lookup is billed directly against your Prospeo account credits — not Clay Data Credits. The results are saved in Clay only. Clay does not write data back to your Prospeo account, so the leads and emails found will not appear in your Prospeo dashboard or contact lists. If you look up the same contact directly in Prospeo later, that will be treated as a new lookup and charged against your Prospeo credits.

## `Action` Find Work Email

The **Find Work Email** action lets you find the work email of a contact using a person's name and company domain.

**Step 1: Choose the Prospeo account you want to use**  
You can use either the Clay-managed Prospeo account or bring your own key.  
If you use the Clay-managed Prospeo account you will be charged at 2 credits per enriched cell.

**Step 2: Select Required and Optional Setup Inputs**  
You will need to enter the Full Name and Company Domain of person you want to find the Work Email for.  
Optionally, you are also able to include catch-all emails.

**Step 3 (Optional): Select Auto-update**  
By default, Prospeo will auto-update the integration every 24 hours. Make sure to toggle this step off if you do not want to auto-update. However if you do so, you might run into stale data problems.

**Step 4 (Optional): Select Conditional Run Criteria**  
If you want to only run this enrichment under set circumstances, you are able to input formulas where the column runs only if the formula is true. Learn more about conditional runs in [this Clay University lesson](https://www.clay.com/university/lesson/ai-formulas-conditional-runs-clay-101#:~:text=Conditional%20runs%20\(which%20make%20use,personal%20emails%20for%20all%20rows\).).

## `Action` Find Email Addresses Associated with a Domain

The **Find Email Addresses Associated with a Domain** action lets you find email addresses associated with a company domain and can also be used to find generic email addresses for a given domain.

**Step 1: Choose the Prospeo account you want to use**  
You can use either the Clay-managed Prospeo account or bring your own key.  
If you use the Clay-managed Prospeo account you will be charged at 2 credits per enriched cell.

**Step 2: Select Required and Optional Setup Inputs**  
To find the email addresses associated with a given domain using Prospeo's email database, you will need to provide the domain and email type which you want to receive (generic, professional). Even though these are marked as optional, it's best advised to enter both fields.

**Step 3 (Optional): Select Auto-update**  
By default, Prospeo will auto-update the integration every 24 hours. Make sure to toggle this step off if you do not want to auto-update. However if you do so, you might run into stale data problems.

**Step 4 (Optional): Select Conditional Run Criteria**  
If you want to only run this enrichment under set circumstances, you are able to input formulas where the column runs only if the formula is true. Learn more about conditional runs in [this Clay University lesson](https://www.clay.com/university/lesson/ai-formulas-conditional-runs-clay-101#:~:text=Conditional%20runs%20\(which%20make%20use,personal%20emails%20for%20all%20rows\).).

## `Action` Find Work Email and Enrich Person from LinkedIn URL

The **Find Work Email and Enrich Person from LinkedIn URL** action lets you find email addresses associated with the given company domain.

**Step 1: Choose the Prospeo account you want to use**  
You can use either the Clay-managed Prospeo account or bring your own key.  
If you use the Clay-managed Prospeo account you will be charged at 2 credits per enriched cell.

**Step 2: Enter LinkedIn URL as setup input**  
Please input the **Linkedin URL** of your contact to find their work email and enriched profile.

**Step 3 (Optional): Select Auto-update**  
By default, Prospeo will auto-update the integration every 24 hours. Make sure to toggle this step off if you do not want to auto-update. However if you do so, you might run into stale data problems.

**Step 4 (Optional): Select Conditional Run Criteria**  
If you want to only run this enrichment under set circumstances, you are able to input formulas where the column runs only if the formula is true. Learn more about conditional runs in [this Clay University lesson](https://www.clay.com/university/lesson/ai-formulas-conditional-runs-clay-101#:~:text=Conditional%20runs%20\(which%20make%20use,personal%20emails%20for%20all%20rows\).)

## `Action` Find people at company

The **Find people at company** action lets you search for contacts at a specific company by domain, with optional filters for job title, seniority, and department.

**Note:** A maximum of 25 contacts are returned per run — this is a cap set by the Prospeo API, not a Clay limitation. There is no configurable limit field on this action, so you cannot restrict results to fewer than 25. If you need to control the number of people returned per company:

- **Fewer than 25**: use Clay's native **Find People** source instead — it includes **Limit per company** (up to 100) and **Limit results** fields. You can run Prospeo enrichments afterward to find emails.
- **More than 25**: use **Find People at These Companies** (under Tools or as a source). It uses Clay's own search index and supports configurable limits up to 100 contacts per company.

**Step 1: Choose the Prospeo account you want to use**  
You can use either the Clay-managed Prospeo account or bring your own key.  
You will be charged **0.3 credits per person found**.

**Step 2: Select Required and Optional Setup Inputs**

Required:

-   **Company domain:** The domain of the company to search (e.g., `clay.com`).

Optional:

-   **Company name:** The name of the company, used to narrow results alongside the domain.
-   **Job titles to include:** Only return people whose job title matches one of these values. Enter all variations you need (e.g., both "VP of Sales" and "Vice President of Sales").
-   **Job titles to exclude:** Exclude people whose job title matches one of these values.
-   **Seniorities:** Filter by seniority level (e.g., Director, VP, C-Level).
-   **Departments:** Filter by department (e.g., Sales, Engineering, Marketing).
