---
title: Microsoft Dynamics 365 CRM integration overview
description: Cloud-based Customer Relationship Management platform
last_synced: 2026-04-26T01:40:21.790Z
---

# Microsoft Dynamics 365 CRM integration overview

Cloud-based Customer Relationship Management platform

## Microsoft Dynamics Integration Overview

Connect Clay to your Dynamics CRM to:

-   Import Objects as a source
-   Lookup Objects
-   Update Objects
-   Create Objects

## Use Cases

There are many powerful use cases with the Microsoft Dynamics Integration. Examples include:

-   **Lead Scoring:** Build accurate lead scores from your enriched contacts.
-   **Customer Segmentation:** Sort customers, companies, and leads into custom industry categories.
-   **Automated Outbound:** Run outbound campaigns based on company size and industry.
-   **TAM Sourcing:** Build targeted lead lists using Clay to import back to your CRM.

## Setting up Dynamics integration

To set up the Dynamics 365 CRM Integration, follow these steps:

**Step 1:** Visit the **Settings** page and navigate to **Connections.**

**Step 2:** Click + Add Connection and select **Dynamics 365 CRM**.

**Step 3:** Enter the **domain** of your Dynamics 365 CRM and sign in to your Dynamics account.

**Step 4:** Name your account key.

Optionally, you can set this account as the default for your workspace.

## Connecting with a service account

For enterprise and team setups, we recommend connecting Dynamics 365 to Clay using a **dedicated service account** — a shared Microsoft account — rather than a personal user account. This prevents connection disruptions if an individual's credentials change or a team member leaves.

**Requirements for the service account:**

-   A valid Microsoft (Azure AD) account
-   A Dynamics 365 license assigned to the account
-   The required Dynamics 365 permissions (for example, a System User role or equivalent)

To connect with a service account, follow the same setup steps above and sign in with the service account credentials at Step 3.

**Note on MFA re-authentication:** The OAuth connection requires re-authentication when your Azure AD Conditional Access policies enforce MFA or sign-in frequency limits (commonly every 7 days). If the service account is not re-authenticated within your organization's required window, the connection will stop working. To avoid disruptions, re-authenticate proactively on schedule or work with your Azure AD administrator to configure a sign-in frequency exemption for the service account used with Clay.

**Entra Service Principal (app-only) authentication is not currently supported.** The Dynamics 365 connection requires signing in with a Microsoft user account (personal or service account). If your organization requires app-only authentication without user account MFA dependencies, please reach out to Clay support to register your interest.

## [‍](https://app.arcade.software/share/IiX3ez8JQvNmSDhn9F7w)Import your Microsoft Dynamics data into Clay

You can import your Dynamics data as a source for a new or existing table.

To get started:

### **Step 1:** Navigate to the **Source panel.**

To access source panel:

**New table:** In a workbook, click `+ Add` at the bottom. Search for `Microsoft` and select from the results.

**Existing Table:** In an existing table, open the table and select **Tools > Import** to configure Dynamics as a data source.

### **Step 2:** Select your Dynamics account

Choose the Dynamics account you wish to use for importing data. Ensure the selected account has the appropriate permissions to access the objects you need.

### Select 3: Import your objects

Specify the **Object Type** to import. Choose from Accounts, Leads, Contacts, or Opportunities

Optionally you can select a **view** to load data from and the fields you want to return. If left blank, all data will be imported for the selected **Object Type** and **Fields**.

### `Actions` Create Object

Select object and map out object type.

**Step 1:** Select your Dynamics 365 account.

**Step 2:** Specify **Object Type** to create.

This can be **Account**, **Contact**, **Lead**, or **Opportunity.**

**Step 3:** Map fields for created object.

Match the relevant fields from your Clay table to the corresponding Dynamics properties, ensuring data types and formats align.

**Step 4:** Configure run settings.

By default auto-update, any new row added to your Clay table will automatically create an object in Dynamics.  Learn more about auto-update in [this brief guide](https://docs.clay.com/en/articles/9642165-auto-update-and-auto-dedupe-table).

To run enrichment only under specific conditions, use formulas that trigger the column when the formula is true. Learn more about AI formulas in [this Clay University lesson](https://www.clay.com/university/lesson/ai-formulas-conditional-runs-clay-101).

**Step 5:** Run enrichment to create an object.

### `Actions` Lookup Object

Check if an object exists in your Dynamics CRM.

**Step 1:** Select your Dynamics 365 account.

**Step 2:** Specify **Object Type** to lookup.

**Step 3:** Filter **Objects**

Define at least one field you want to filter by, then provide the corresponding filter values.

You can either type in these filter values directly or reference data from other columns.

**Step 4 (Optional):** Specify fields to return

Choose the fields you want to return. If no fields are selected, all available fields will return.

**Step 5:** Configure run settings.

By default auto-update, any new row added to your Clay table will automatically lookup for a matching object in Dynamics.  Learn more about auto-update in [this brief guide](https://docs.clay.com/en/articles/9642165-auto-update-and-auto-dedupe-table).

To run enrichment only under specific conditions, use formulas that trigger the column when the formula is true. Learn more about AI formulas in [this Clay University lesson](https://www.clay.com/university/lesson/ai-formulas-conditional-runs-clay-101).

**Step 5:** Run enrichment to lookup an object.

### `Actions` Update Object

Update an object in your Dynamics CRM.

**Step 1:** Select your Dynamics 365 account.

**Step 2:** Specify **Object Type** to update.

**Step 3:** Enter the **Object ID** to update.

**Step 4:** Map fields for created object.

Match the relevant fields from your Clay table to the corresponding Dynamics properties you want to update. Ensure that data types and formats align.

**Step 5:** Configure run settings.

By default auto-update, any new row added to your Clay table will automatically update the object in Dynamics.  Learn more about auto-update in [this brief guide](https://docs.clay.com/en/articles/9642165-auto-update-and-auto-dedupe-table).

To run enrichment only under specific conditions, use formulas that trigger the column when the formula is true. Learn more about AI formulas in [this Clay University lesson](https://www.clay.com/university/lesson/ai-formulas-conditional-runs-clay-101).

**Step 6:** Run enrichment to update an object.
