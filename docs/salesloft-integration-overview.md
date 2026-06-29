---
title: Salesloft integration overview
description: Sales engagement platform.
last_synced: 2026-04-26T01:40:36.302Z
---

# Salesloft integration overview

Sales engagement platform.

### Integration Overview

Salesloft in Clay allows you to manage accounts and people, including creating, updating, and looking up records, as well as adding people to cadences.

For the Clay and Salesloft integration, here's a breakdown of the actions available:

1.  **Create Account/Person**: Add new accounts or individuals directly to Salesloft.
2.  **Lookup Account/Person**: Find specific accounts or people in Salesloft using existing data fields for reference.
3.  **Add Person to Cadence**: Place individuals on designated cadences for automated outreach or follow-up.
4.  **Upsert Account/Person**: Update existing records or insert new ones to ensure the most current data for accounts and individuals.
5.  **Export Data for Bulk Email Campaigns**: Gather and export data efficiently for large-scale email campaigns, keeping your outreach organized and scalable.

### Requirements for Setting Up SalesLoft

To get set up with Salesloft, you'll need to obtain an API key and have an existing Cadence if you want to send leads directly to a Cadence.

**Connect Salesloft with Clay via an API Key**

To set up Salesloft within Clay, you'll need to first obtain a Salesloft API Key. You can request for an API key within Salesloft's [New API Key](https://developers.salesloft.com/docs/platform/external-calendars/setup-api-key/) Page.

Once you've obtained your API key, navigate to your enrichment panel and paste your API key when creating a new account.

**Set up Cadence within Salesloft**

To add leads to a Cadence directly from Clay you will need to have an existing Cadence. This must be done directly within Salesloft. Refer to [Salesloft's documentation](https://help.salesloft.com/s/article/Create-a-Cadence?language=en_US) if you need more help.

## Salesloft use cases

There are a few important callouts

-   If you want to push personalized snippets to SalesLoft, please make sure to use custom variables within your enrichment
-   Ensure you are mapping out all fields like first name, last name and email correctly

### Action: Create Account

The Salesloft Create Account action lets you create new accounts within Salesloft.

**Step 1: Select the Create Account action**

**Step 2: Select your Salesloft account**

Select the Salesloft account to send emails from. If you have not already integrated Salesloft with Clay, please enter your API key when creating an account ([Salesloft API key documentation](https://developers.salesloft.com/docs/platform/external-calendars/setup-api-key/)).

**Step 3: Configure the required and optional fields**

Make sure fields like first name, last name, and Personal LinkedIn URL are all mapped correctly.

**Step 4: Insert custom variables**

Please note this step if you are inserting custom variables. This can include summaries, AI snippets, and other custom fields within Salesloft.

**Step 5: Configure run settings**

Specify Auto-update and Conditional run statements.

If you are running trigger campaigns please make sure to turn Auto-update on.

![](https://cdn.prod.website-files.com/687e604972375496b891fe58/691e659fa1b8cb9cc1ee32da_672aeddc0616d6a7ef69234a_672aec9c4163926064f940bf_CleanShot%2525202024-10-31%252520at%25252002.14.57%2525402x%252520\(1\).png)

### Action: Upserting an Account

The Salesloft Upsert Account action lets you upsert accounts within Salesloft.

**Step 1: Select the Upsert Account action**

**Step 2: Select your Salesloft account**

Select the Salesloft account to send emails from. If you have not already integrated Salesloft with Clay, please enter your API key when creating an account ([Salesloft API key documentation](https://developers.salesloft.com/docs/platform/external-calendars/setup-api-key/)).

**Step 3: Configure the required and optional fields**

Make sure fields like first name, last name, and Personal LinkedIn URL are all mapped correctly.

**Step 4: Insert custom variables**

Please note this step if you are inserting custom variables. This can include summaries, AI snippets, and other custom fields within Salesloft.

**Step 5: Configure run settings**

Specify Auto-update and Conditional run statements.

If you are running trigger campaigns please make sure to turn Auto-update on.

![](https://cdn.prod.website-files.com/687e604972375496b891fe58/691e659fa1b8cb9cc1ee32da_672aeddc0616d6a7ef69234a_672aec9c4163926064f940bf_CleanShot%2525202024-10-31%252520at%25252002.14.57%2525402x%252520\(1\).png)

### Action: Adding Person to Cadence

The Add Person to Cadence action lets you create new leads within Salesloft.

**Step 1: Select the Add Person to Cadence action**

**Step 2: Select your Salesloft account**

Select the Salesloft account to send emails from. If you have not already integrated Salesloft with Clay, please enter your API key when creating an account ([Salesloft API key documentation](https://developers.salesloft.com/docs/platform/external-calendars/setup-api-key/)).

**Step 3: Specify the Salesloft Person and Cadence ID**

The SalesLoft Person you'd like to add to a cadence. This is normally taken from a Lookup Person or Upsert Person step.

The Cadence you'd like to add this person to.

**Step 4: Configure run settings**

Specify Auto-update and Conditional run statements.

If you are running trigger campaigns please make sure to turn Auto-update on.

![](https://cdn.prod.website-files.com/687e604972375496b891fe58/691e659fa1b8cb9cc1ee32da_672aeddc0616d6a7ef69234a_672aec9c4163926064f940bf_CleanShot%2525202024-10-31%252520at%25252002.14.57%2525402x%252520\(1\).png)

### Action: Upsert Person

The Upsert Person action lets you Upsert leads within Salesloft.

**Step 1: Select the Upsert Person action**

**Step 2: Select your Salesloft account**

Select the Salesloft account to send emails from. If you have not already integrated Salesloft with Clay, please enter your API key when creating an account ([Salesloft API key documentation](https://developers.salesloft.com/docs/platform/external-calendars/setup-api-key/)).

**Step 3: Input mandatory and optional setup inputs**

Enter the contact information of the lead you want to upsert.

If you want to add any additional information to the contacts you are upserting, you can map out the dynamic fields as inputs.

**Step 4: Insert custom variables**

Please note this step if you are inserting custom variables. This can include summaries, AI snippets, and other custom fields within Salesloft.

**Step 5: Configure run settings**

Specify Auto-update and Conditional run statements.

If you are running trigger campaigns please make sure to turn Auto-update on.

![](https://cdn.prod.website-files.com/687e604972375496b891fe58/691e659fa1b8cb9cc1ee32da_672aeddc0616d6a7ef69234a_672aec9c4163926064f940bf_CleanShot%2525202024-10-31%252520at%25252002.14.57%2525402x%252520\(1\).png)

### Action: Create Person

The Salesloft Create Person action lets you create new leads within Salesloft.

**Step 1: Select the Create Person action**

**Step 2: Select your Salesloft account**

Select the Salesloft account to send emails from. If you have not already integrated Salesloft with Clay, please enter your API key when creating an account ([Salesloft API key documentation](https://developers.salesloft.com/docs/platform/external-calendars/setup-api-key/)).

**Step 3: Input mandatory and optional setup inputs**

Enter the contact information of the lead you want to upsert.

If you want to add any additional information to the contacts you are upserting, you can map out the dynamic fields as inputs.

**Step 4: Insert custom variables**

Please note this step if you are inserting custom variables. This can include summaries, AI snippets, and other custom fields within Salesloft.

**Step 5: Configure run settings**

Specify Auto-update and Conditional run statements.

If you are running trigger campaigns please make sure to turn Auto-update on.

![](https://cdn.prod.website-files.com/687e604972375496b891fe58/691e659fa1b8cb9cc1ee32da_672aeddc0616d6a7ef69234a_672aec9c4163926064f940bf_CleanShot%2525202024-10-31%252520at%25252002.14.57%2525402x%252520\(1\).png)

## Avoiding duplicate Salesloft person records

When you use both **Upsert Person** and **Add Person to Cadence** in the same Clay table, both columns may run at the same time. If Add Person to Cadence fires before Upsert Person finishes, Salesloft may create a second person record for the cadence enrollment instead of attaching to the upserted record — leaving you with two duplicate person records for the same contact.

To prevent this, follow two steps:

**1. Pass the Salesloft Person ID from Upsert Person into Add Person to Cadence**

In the Add Person to Cadence column, set the Person input to reference the **Person ID returned by the Upsert Person action** — not the contact's email address directly. Use the `/` field picker inside Add Person to Cadence and select the Person ID output from your Upsert Person column. This helps Add Person to Cadence attach to the existing upserted record rather than creating a new one.

**2. Add a run condition to Add Person to Cadence**

In the Add Person to Cadence column's run settings, add a conditional run so it only executes after Upsert Person has completed successfully. For example, set the condition to run only when the Upsert Person status equals `success`.

Sequencing the two actions this way — Upsert Person first, Add Person to Cadence second — should prevent Add to Cadence from running before the upserted record exists in Salesloft.

## Sending multiple tags to a Salesloft person

The **Tags** field in the **Create Person** and **Upsert Person** actions accepts multiple tags per record. If your tag values live in separate Clay columns (for example, a "Partner Tag" column and a "Hiring Tag" column), you need to combine them into a single column before mapping to Tags — mapping individual text columns directly to the Tags field will concatenate all the values into one tag in Salesloft instead of creating separate tags.

**How to send multiple tags from separate columns:**

1. Add a **formula column** to your Clay table that combines your tag columns into a list:

   ```
   _.compact([{{Partner Tag}}, {{Hiring Tag}}, {{Tier Tag}}])
   ```

   `_.compact()` removes any empty or null values, so rows where a tag column is blank don't create empty tags in Salesloft.

2. In the formula column settings, set the **data type to Multi-select**.

3. In your Salesloft **Create Person** or **Upsert Person** action, map this Multi-select column to the **Tags** field.

Salesloft will receive each value in the list as a separate tag.

**Tip:** If you prefer to keep your formula column as a text type, use `.join(",")` to produce a comma-separated string instead — `_.compact([{{Tag Column 1}}, {{Tag Column 2}}, {{Tag Column 3}}]).join(",")` — and Clay will split the values into separate tags before sending to Salesloft.
