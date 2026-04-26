---
title: La Growth Machine integration overview
source_url: https://university.clay.com/docs/la-growth-machine-integration-overview
last_synced: 2026-04-26T01:40:12.936Z
upstream_hash: f71b37ca7559ffff2ae73b1c7cee612506d7deedb161244d15e8d2197bd84c56
---

# La Growth Machine integration overview

Platform for automating multichannel sales outreach.

### Integration Overview

La Growth Machine in Clay allows users to search for leads by email, LinkedIn URL, or lead ID, and create new leads from LinkedIn URLs.

For the Clay and La Growth Machine integration, here’s a breakdown of the actions available:

1.  **Search Lead**: Locate specific leads in La Growth Machine. This can be a LinkedIn URL, Lead ID, or an Email.
2.  **Create or Update Lead**: Add new leads or update existing lead information.

## Requirements for Setting Up La Growth Machine

To get set up with La Growth Machine, you’ll need to obtain an API key and have an existing Cadence if you want to send leads directly to a Cadence.

**Connect La Growth Machine with Clay via an API Key**

To set up La Growth Machine within Clay, you’ll need to first obtain a La Growth Machine API Key. You can request for an API key within your **Settings > Integrations & API.**

Once you’ve obtained your API key, navigate to your enrichment panel.

Paste your API key when creating a new account.

### **Set up audience to send leads to**

To add leads to an Audience directly from Clay you will need to have an existing Audience. This must be done directly within La Growth Machine. To create an audience, head over to the left sidebar and **Leads > Audiences.**

## La Growth Machine use cases

There are a few important callouts

-   If you want to push personalized snippets to La Growth Machine, please make sure to use custom variables within your enrichment
-   Ensure you are mapping out all fields like first name, last name and email correctly

### Action: Create or Update Lead

Create or update a lead in La Growth Machine from a LinkedIn URL. By default, only empty fields will be updated; if you want to update fields that already have data, go to Outreach Settings in your La Growth Machine account, and turn on "Update the existing contact with changed or new fields".

**Step 1: Select the Create or update lead action**

**Step 2: Specify the audience of your lead**

**Step 3 (Optional): Map out contact information**

Map out the contact information of the fields to export to La Growth Machine.

Note: Please make sure you are mapping your fields correctly

**Step 4 (Optional): Specify custom attributes to export**

**Step 5 (Optional): Configure run settings**

Specify Auto-update and Conditional run statements.

![](https://cdn.prod.website-files.com/687e604972375496b891fe58/691e659fa1b8cb9cc1ee32da_672aeddc0616d6a7ef69234a_672aec9c4163926064f940bf_CleanShot%2525202024-10-31%252520at%25252002.14.57%2525402x%252520\(1\).png)

### Action: Create or Update Lead

The Search Lead action allows you to search a lead in La Growth Machine from an email, LinkedIn URL, or lead ID

**Step 1: Select the Search Lead action**

**Step 2: Specify the Lead Identifier**

This can be a LinkedIn URL (NOT a SalesNav URL), an email, or a lead ID

**Step 3 (Optional): Configure run settings**

Specify Auto-update and Conditional run statements.

![](https://cdn.prod.website-files.com/687e604972375496b891fe58/691e659fa1b8cb9cc1ee32da_672aeddc0616d6a7ef69234a_672aec9c4163926064f940bf_CleanShot%2525202024-10-31%252520at%25252002.14.57%2525402x%252520\(1\).png)
