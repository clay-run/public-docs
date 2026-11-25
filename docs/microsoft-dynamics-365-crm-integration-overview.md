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

The **Add Dynamics 365 CRM account** window has two tabs: **User Sign In** (the default, which signs in with a Microsoft user account) and **Service Principal** (which connects with your own Microsoft Entra app registration — see [Connecting with a Service Principal](#connecting-with-a-service-principal-app-registration) below). The steps below are for **User Sign In**.

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

If your organization requires app-only authentication without user account MFA dependencies, connect with a Service Principal instead (see below).

## "Need admin approval" when signing in to Dynamics 365

When you connect Dynamics 365 with the **User Sign In** tab, Microsoft may show a **Need admin approval** screen that says "Clay needs permission to access resources in your organization that only an admin can grant." This happens when your Microsoft organization doesn't let users approve third-party apps on their own.

You have two ways to connect:

-   **Ask a Microsoft admin to approve Clay.** A Microsoft (Entra ID) admin in your organization signs in through the **User Sign In** tab and approves the Clay app.
-   **Use the Service Principal tab instead.** A Service Principal connection uses an app registration that your organization owns, so it doesn't go through the Clay app approval screen. See [Connecting with a Service Principal](#connecting-with-a-service-principal-app-registration).

## Connecting with a Service Principal (app registration)

The **Service Principal** option connects Clay to Dynamics 365 with a Microsoft Entra app registration (client credentials) for server-to-server integration. No individual user signs in, so the connection doesn't depend on a user's password, MFA, or sign-in frequency policies. Service Principal connections work with the Dynamics 365 Create Object, Lookup Object, and Update Object actions.

**Before you start, in Microsoft Entra and Dynamics 365:**

1.  Create an app registration in Microsoft Entra ID (see Microsoft's guide to [creating an app registration and service principal](https://learn.microsoft.com/en-us/entra/identity-platform/howto-create-service-principal-portal)).
2.  Create a client secret for the app registration under **Certificates & secrets**.
3.  In the Power Platform admin center, add the app registration as an **Application User** in your Dynamics 365 environment and assign it a security role. The security role controls which records Clay can read and write.

**To connect Dynamics 365 with a Service Principal in Clay:**

1.  Go to **Settings > Connections**, click + Add Connection, and select **Dynamics 365 CRM**.
2.  Select the **Service Principal** tab.
3.  Fill in the following fields:
    -   **Name your connection** (optional): a name to identify this connection in Clay.
    -   **Environment URL**: your Dynamics 365 environment URL, for example `https://myorg.crm.dynamics.com`. Don't include a trailing slash.
    -   **Directory (tenant) ID**: from your app registration's overview page.
    -   **Application (client) ID**: from your app registration's overview page.
    -   **Client secret**: the client secret you created for the app registration.
4.  Optionally, turn on **Set as default** to auto-select this account where possible.
5.  Click **Authenticate**.

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

**Mapping lookup fields (fields that link to another Dynamics record):** Some Dynamics 365 fields, such as a custom Country, Lead Source, or Parent Account field, don't take text. They link to a record in another Dynamics table, so they need that record's ID (a GUID such as `3f2a1c9e-...`), not its name. If you map plain text like "US" or "Digital Advertising" into one of these fields, Dynamics rejects the record with an error such as "Error in query syntax" or "')' or ',' expected ... in '(Digital Advertising)'". To fill a lookup field from a name:

1.  Add a Dynamics 365 **Look up object** column before your Create Object column. Set **Object Type** to the table the field links to (custom tables are listed too), and filter by the name column using the value from your Clay table.
2.  The lookup result includes the record's ID field (for example `accountid`, or `<table name>id` for a custom table).
3.  In your Create Object column, map that ID into the lookup field instead of the text.
4.  Make sure the Look up object column runs before the Create Object column.

The same applies to lookup fields in the Update Object action.

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

**Note:** The filter field picker lists fields by their **Display Name** in Dynamics 365, not by the internal schema name. For example, the Account object's `accountid` field (schema name) appears in the picker as **Company** (its Display Name). If you can't find a field by its schema name, search for its Display Name instead. You can look up a field's Display Name in Dynamics 365 under **Settings > Customizations > Customize the System**.

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

## Import Dynamics 365 records into Clay Audiences (beta)

**Currently in closed beta.** Using Microsoft Dynamics 365 CRM as a data source in Clay Audiences is available only to select workspaces. If you don't see Dynamics 365 when you add a source in Audiences, contact your Growth Strategist or Clay support to ask about access. For how to add a source in Audiences, see [Importing your data](audiences.md#importing-your-data).

When the Dynamics 365 source is enabled for your workspace, you can import the following Dynamics 365 record types into Clay Audiences:

-   **Accounts** — appear as companies in Audiences.
-   **Contacts** and **Leads** — appear as people in Audiences.
-   **Opportunities**

**Qualified Dynamics 365 Leads merge into their Contacts.** When you qualify a Lead in Dynamics 365 and it creates a Contact, Clay Audiences merges the Lead and the Contact into a single person record instead of keeping two separate records. Clay matches them using the Contact's **Originating lead** lookup (`originatingleadid`).
