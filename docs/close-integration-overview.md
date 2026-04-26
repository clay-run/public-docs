---
title: Close integration overview
source_url: https://university.clay.com/docs/close-integration-overview
last_synced: 2026-04-26T01:39:46.174Z
upstream_hash: 16e2f6fc129adef59179411b8adc6d4318d98d1bf0b60d46a8f0f5fd68cdae53
---

# Close integration overview

Streamlined CRM software for team productivity.

## Setting up the Close Integration

To set up the Close and Clay integration, follow these steps:

1.  Visit the Settings page and navigate to **Connections.**
2.  Click **\+ Add Connection** and select Close the menu
3.  Enter your Close API key and name your Account. Reference [Close’s API key guide](https://help.close.com/docs/api-keys-oauth) for more help.

## Import Close contacts into Clay as a source

You can use Close as a source for a new or existing table.

To set up Close as a source:

**Step 1:** Select Close source option.

In a workbook, click `+ Add` at the bottom. Search for `Close` and select from the results.

**Step 2:** Select the Close account you want to use.

**Step 3:** Fill out Auth fields to connect to Close’s database.

## Available Close actions

Within your Clay table and workbook, you’re able to run the following Close-supported actions:

-   Lookup Objects
-   Create Leads
-   Update Leads
-   Create Contact
-   Update Contact
-   Subscribe to Sequence

### `Action` Lookup Objects

Lookup an Object (Lead, Contact) in your Close CRM.

To run the Lookup Objects action:

**Step 1:** Select the **Close account** you want to use.

**Step 2:** Specify the object you are looking up

**Step 3:** Build your Query to filter contacts

Use the [**Visual Query Builder**](https://developer.close.com/resources/advanced-filtering/#visual-query-builder) to construct a query. Paste the output into the query field and adjust it to include your Clay variables.

**Step 4:** Configure run settings

By default, new rows within your Clay table will automatically run this action. Learn more about auto-update in [this brief guide](https://docs.clay.com/en/articles/9642165-auto-update-and-auto-dedupe-table).

To run enrichment only under specific conditions, use formulas that trigger the column when the formula is true. Learn more about AI formulas in [this Clay University lesson](https://www.clay.com/university/lesson/ai-formulas-conditional-runs-clay-101).

**Step 5:** Run your enrichment to lookup an object.

### `Action` Create Leads

To run the Create Leads action:

**Step 1:** Select the **Close account** you want to use.

**Step 2:** Map lead fields

Map the relevant fields for the lead you want to create. Click **Refresh Fields** to update, and leave optional fields blank if not needed.

**Step 4:** Configure run settings

By default, new rows within your Clay table will automatically run this action. Learn more about auto-update in [this brief guide](https://docs.clay.com/en/articles/9642165-auto-update-and-auto-dedupe-table).

To run enrichment only under specific conditions, use formulas that trigger the column when the formula is true. Learn more about AI formulas in [this Clay University lesson](https://www.clay.com/university/lesson/ai-formulas-conditional-runs-clay-101).

**Step 5:** Run your enrichment to create a lead.

### `Action` Update Leads

Update a lead in your Close CRM

To run the Update Leads action:

**Step 1:** Select the **Close account** you want to use.

**Step 2:** Specify Lead ID

Enter the Lead ID to update. Use the **Lookup Object** action if you don’t know the Lead ID.

**Step 3:** Map lead fields

Map the relevant fields for the lead you want to update. Click **Refresh Fields** to update, and leave optional fields blank if not needed.

**Step 4:** Configure run settings

By default, new rows within your Clay table will automatically run this action. Learn more about auto-update in [this brief guide](https://docs.clay.com/en/articles/9642165-auto-update-and-auto-dedupe-table).

To run enrichment only under specific conditions, use formulas that trigger the column when the formula is true. Learn more about AI formulas in [this Clay University lesson](https://www.clay.com/university/lesson/ai-formulas-conditional-runs-clay-101).

**Step 5:** Run your enrichment to update a lead.

### `Action` Create Contact

To run the Create Contact action:

**Step 1:** Select the **Close account** you want to use.

**Step 2:** Map contact fields

Map the relevant fields for the contact you want to create. Click **Refresh Fields** to update, and leave optional fields blank if not needed.

**Step 4:** Configure run settings

By default, new rows within your Clay table will automatically run this action. Learn more about auto-update in [this brief guide](https://docs.clay.com/en/articles/9642165-auto-update-and-auto-dedupe-table).

To run enrichment only under specific conditions, use formulas that trigger the column when the formula is true. Learn more about AI formulas in [this Clay University lesson](https://www.clay.com/university/lesson/ai-formulas-conditional-runs-clay-101).

### `Action` Update Contact

Update a contact in your Close CRM.

To run the Update Leads action:

**Step 1:** Select the **Close account** you want to use.

**Step 2:** Specify Contact ID

Enter the Contact ID to update. Use the **Lookup Object** action if you don’t know the Contact ID.

**Step 3:** Map Contact fields

Map the relevant fields for the contact you want to update. Click **Refresh Fields** to update, and leave optional fields blank if not needed.

**Step 4:** Configure run settings

By default, new rows within your Clay table will automatically run this action. Learn more about auto-update in [this brief guide](https://docs.clay.com/en/articles/9642165-auto-update-and-auto-dedupe-table).

To run enrichment only under specific conditions, use formulas that trigger the column when the formula is true. Learn more about AI formulas in [this Clay University lesson](https://www.clay.com/university/lesson/ai-formulas-conditional-runs-clay-101).

**Step 5:** Run your enrichment to update a contact.

### `Action` Subscribe to Sequence

To run the Subscribe to Sequence action:

**Step 1:** Select the **Close account** you want to use.

**Step 2:** Specify Contact and Sequence ID

Enter the Contact and Sequence ID. Use the **Lookup Object** action if you don’t know these IDs.

**(Optional) Step 3:** Enter additional Sequence information

Optionally, you can also specify the following fields for your contact: **Sender Account ID**, **Sender**, **Assign Calls To**, and **From Phone Number.**

**Step 4:** Configure run settings

By default, new rows within your Clay table will automatically run this action. Learn more about auto-update in [this brief guide](https://docs.clay.com/en/articles/9642165-auto-update-and-auto-dedupe-table).

To run enrichment only under specific conditions, use formulas that trigger the column when the formula is true. Learn more about AI formulas in [this Clay University lesson](https://www.clay.com/university/lesson/ai-formulas-conditional-runs-clay-101).

**Step 5:** Run your enrichment to subscribe a contact to a sequence.
