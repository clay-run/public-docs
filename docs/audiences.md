---
title: Audiences
description: "Clay Audiences is available on Growth and Enterprise plans. Launch workspaces can import via CSV, people/company search, and Clay table sends; connecting a CRM or data warehouse requires Growth or above. Trial workspaces do not have access to Audiences."
last_synced: 2026-08-20T01:53:27.941Z
---

# Audiences

**Plan availability:** Clay Audiences is available on **Growth** and **Enterprise** plans (including legacy Enterprise). Launch workspaces have access to core Audiences features — importing via CSV, people/company search, and Clay table sends — but connecting a CRM or data warehouse as a data source requires **Growth or above**. Free, Trial, and legacy non-Enterprise plan workspaces do not have access to Audiences. Growth plans can sync up to 250,000 CRM/DWH records; Enterprise plans support up to 25,000,000 records.

Clay Audiences is the unified data layer for your workspace.  It combines your CRM, data warehouse, and third-party enrichments into one persistent profile per contact and account, updated in real time.

Use it to build dynamic segments across millions of records, run automated enrichment and signal workflows at scale, and sync results back to Salesforce without managing dozens of separate tables.

Setting up Audiences is four major steps:

1.  **Import your data** — connect Salesforce, HubSpot, Snowflake, or Google BigQuery and bring your records into Audiences.
2.  **Create audiences** — build dynamic segments using filters to target the right contacts and accounts.
3.  **Enrich and monitor** — run bulk enrichments and signals that write data permanently back to each record.
4.  **Write back to your CRM** — sync enriched data and segment membership back to Salesforce.

## Roles and permissions

Viewing and filtering audience data is available to all workspace roles. Most write operations require workspace **Admin** access. The table below shows the full breakdown:

| Action | Admin | Editor | Viewer |
|---|---|---|---|
| View, browse, and filter audience data | ✓ | ✓ | ✓ |
| Create and edit audience segments | ✓ | — | — |
| Run bulk enrichments | ✓ | — | — |
| Add or configure data sources | ✓ | — | — |
| Export individual records to Salesforce | ✓ | — | — |
| Upsert or update records from a Clay table into Audiences | ✓ | — | — |

To change someone's role, go to **Settings** → **Team** and use the dropdown next to their name. Changes apply immediately. Editors and Viewers who need to create segments, run bulk enrichments, or manage data sources should have their role upgraded to Admin, or ask a workspace Admin to perform those actions on their behalf.

## Importing your data

To view your full audience, click `People` or `Companies` in the left sidebar.

To add a data source for the first time, click the `Add data` button in the top right, then click `Add Source`. Most sources open a guided wizard that takes the import one step at a time — `CSV file`, `Clay table`, `Snowflake`, `Google BigQuery`, and `Databricks` all work this way. Salesforce and HubSpot open their own source settings panel instead.

**Note:** Non-admin workspace members (Editors and Viewers) can view, browse, and filter audience data, but adding or configuring data sources requires Admin access. Non-admins do not see source setup or configuration controls — those controls are hidden for Editors and Viewers, who instead see a prompt to contact a workspace Admin. If you need to add a data source, ask a workspace Admin to do it, or have your role upgraded to Admin.

You can import data from:

-   A new people or companies search
-   CSV
-   Snowflake
-   Google BigQuery
-   Salesforce
-   HubSpot

### Importing from Salesforce

The Salesforce import flow in Audiences has been redesigned. You can import **all records** of a given Salesforce object type or use a **SOQL query** to bring in only the specific subset of records you need — useful when privacy, compliance, or data-ownership requirements make an all-or-nothing CRM import impractical. Multiple imports can be configured for the same Salesforce account — for example, an "All Accounts" import alongside a "West Coast Leads" SOQL subset.

**Supported object types:** Contacts (appear in People), Accounts (appear in Companies), Leads (appear in People), Opportunities (appear in Companies), and Custom Objects.

**Step 1: Connect your Salesforce account**

1.  Click `Add data` → `Add Source` → select your [**Salesforce integration**](https://university.clay.com/docs/salesforce-integration-overview).
    -   If you don't see a Salesforce integration listed, contact your Growth Strategist.
2.  If no Salesforce account is connected yet, select an account from the dropdown or click `+ Add account` to authenticate one. If your workspace already has a Salesforce account connected in Audiences, the panel shows the connected account as a read-only field — **Audiences supports one Salesforce connection per workspace**. You can add multiple imports (different object types or SOQL subsets) from that one connected org, but you cannot switch to or add a second Salesforce account.
3.  Once connected, you land on the Salesforce source settings page.

**Step 2: Add a Salesforce import**

1.  Click **Add records** to open the import wizard.
2.  Select the **object type** to import: Contact, Account, Lead, Opportunity, or Custom Object.
3.  Choose the **record selection method**:
    -   **All records** — imports every record of the selected object type from Salesforce.
    -   **Record subset** — imports only the records returned by a custom SOQL query. Available for Contacts, Accounts, and Leads. Opportunities support "All records" only.
4.  If you chose **Record subset**:
    -   Enter a **Subset name** to identify this import (for example, "Enterprise Accounts" or "West US Leads").
    -   Write your **SOQL query** in the query editor. To get help, click the wand icon and describe in plain English which records you want — Clay generates a valid SOQL query automatically. Click **Test** to preview matching records before confirming.
5.  Click **Confirm** to start the import. Clay immediately begins syncing records.
6.  To add another import (a different object type or a new SOQL subset), click **Add records** again and repeat.
    -   Lead records are automatically merged with matching Contact records into a single person record in your People audience. The primary matching key is the `ConvertedContactId` field — see [Why do some of my Salesforce Lead records not appear as separate person records in Clay?](#why-do-some-of-my-salesforce-lead-records-not-appear-as-separate-person-records-in-clay) in the FAQs below for details.
    -   Opportunity data is associated with your Companies records and becomes available as a filter in any Companies audience.
