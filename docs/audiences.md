---
title: Audiences
description: "Clay Audiences is available on Growth and Enterprise plans. Launch workspaces can import via CSV, people/company search, and Clay table sends; connecting a CRM or data warehouse requires Growth or above. Trial workspaces do not have access to Audiences."
last_synced: 2026-08-20T01:53:27.941Z
---

# Audiences

**Plan availability:** Clay Audiences is available on **Growth** and **Enterprise** plans (including legacy Enterprise). Launch workspaces have access to core Audiences features — importing via CSV, people/company search, and Clay table sends — but connecting a CRM or data warehouse as a data source requires **Growth or above**. Free, Trial, and legacy non-Enterprise plan workspaces do not have access to Audiences. Growth plans can sync up to 250,000 CRM/DWH records; Enterprise plans support up to 25,000,000 records. Only imported Account, Contact, and Lead records count toward this limit — Activities (Salesforce Tasks and Events) and Opportunities associated with those accounts do not count toward the record limit.

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

**SOQL requirements for record subset imports**

SOQL queries for Audiences must be valid SELECT statements and must include `Id`, `SystemModstamp`, and `IsDeleted`. Clay uses these fields to handle incremental syncing and soft-delete detection. For Contact queries, also include `AccountId`; for Lead queries, also include `ConvertedContactId`. The AI query generator includes these fields automatically.

**No semi-joins (nested sub-selects in `WHERE` clauses).** Salesforce's Bulk API 2.0 — which handles the initial full import and weekly re-sync — does not support SOQL semi-joins: queries that filter using `WHERE Id IN (SELECT ... FROM ...)`. A query containing a semi-join passes Clay's **Preview** step but causes the Bulk API import job to fail immediately with **"Salesforce Bulk API job [ID] failed. Records processed: 0"** and zero records imported. Use direct field filters on the imported object only. To filter contacts by opportunity or contact-role attributes, import all contacts and apply that filter as an audience segment condition after importing.

**Importing a Salesforce record subset with SOQL**

Available on **Growth and Enterprise plans**. When setting up a Salesforce import in Audiences, each object type offers a **Record selection** step with two options:

-   **All records** — imports every record of the selected Salesforce object type.
-   **Record subset** — uses a custom SOQL query to import only the records that match specific criteria.

Record subsets let you bring exactly the Salesforce data you need without importing your entire CRM. This is especially useful when you have privacy, compliance, or data-ownership requirements that make an all-or-nothing import impractical.

**To set up a SOQL-filtered record subset:**

1.  In the Salesforce import setup, select the object type (People, Accounts, Leads, or Opportunities).
2.  Under **Record selection**, choose **Record subset**.
3.  Enter a **Subset name** — this label identifies the import in your Audiences sidebar.
4.  Enter a SOQL `SELECT` query. The query must:
    -   Use explicitly named fields (no `SELECT *`).
    -   Include operational sync fields: `Id`, `SystemModstamp`, and `IsDeleted`. Contacts and Opportunities also require `AccountId`; Leads also require `ConvertedContactId`.
5.  (Optional) Click **Generate with AI** to write a SOQL query from a plain-language description.
6.  Click **Preview** to verify the query returns the expected records, then save.

You can add multiple SOQL subsets per object type to bring in distinct groups of records from the same Salesforce org. Each subset syncs on the standard Audiences schedule — 15-minute incremental syncs on Enterprise plans, plus a weekly full sync.

**Sync timing and behavior**

**API method:** Audiences uses different Salesforce API methods depending on the sync operation. The initial full import and weekly full re-sync use Salesforce's **Bulk API 2.0**, which runs under a separate daily quota from your standard Salesforce REST API — Enterprise Salesforce orgs typically have very high Bulk API limits, so the full sync rarely constrains your available API capacity. Full syncs process records in batches of approximately 50,000 per API call. The **15-minute incremental sync** uses Salesforce's **standard REST API** to query only records changed since the last sync. Export from Audiences back to Salesforce also uses Bulk API 2.0.

Clay pulls data from Salesforce on two schedules:

-   **Incremental sync:** Runs every **15 minutes** on Enterprise plans, or once **daily** on Growth plans. Retrieves records whose `SystemModstamp` has changed since the last sync. Any modification to a Salesforce record — user edits, workflow updates, or integration changes — updates `SystemModstamp` and triggers the record to be re-synced. There is no field-level filtering; when a record is picked up, all its mapped fields are synced.
-   **Full sync (every 7 days):** Re-reads all records from Salesforce. Catches anything the incremental sync may miss and reconciles hard-deleted records.

**Formula and calculated fields:** Salesforce formula and calculated fields do not update `SystemModstamp` when they recalculate. Changes to these fields are not captured during incremental syncs — they appear in Audiences only after the next weekly full sync.

**Deleted records:** How quickly a Salesforce deletion is reflected in Audiences depends on the deletion type:

-   **Soft-deleted records** (records moved to the Salesforce Recycle Bin, still queryable with IsDeleted=true): Picked up by the **15-minute incremental sync** and marked **Deleted in source** in your audience within that cycle.
-   **Hard-deleted records** (records permanently purged from Salesforce, no longer queryable): Not visible to the incremental sync. Clay marks these **Deleted in source** during the next **weekly full sync**.

In both cases, the record is not removed from Audiences — it persists with **Deleted in source** status, which you can filter on in any segment to exclude it from your active audiences. If a Salesforce record is deleted and recreated (assigning it a new Salesforce ID), it will temporarily appear as a duplicate entry until the next weekly full sync resolves it. There is no self-serve option to trigger an early full sync — contact Clay support if you need an expedited cleanup.

**Salesforce activities:** To import Salesforce Tasks and Events associated with your Accounts, go to your Salesforce source settings, select `Accounts`, and enable the **Also import activities (tasks and events) associated with these accounts** toggle. Accounts are associated automatically in the background. The Activity tab on each record's detail view then shows Salesforce Tasks and Events alongside other connected activity sources (for example, Gong calls or email sequence activity). Each entry displays the activity type (Task or Event), title, and timestamp. This toggle is only available for Accounts — there is no equivalent option for Contacts, Leads, or the People object. Even if your Salesforce CRM has Tasks or Events associated with contacts or leads, those activities will not appear in the People Activity tab in Audiences.

#### Importing a record subset using SOQL

**Available on Enterprise plans.** If you don't need to import your entire Salesforce org — or if privacy, compliance, or data-ownership requirements make an all-or-nothing CRM import a non-starter — you can use a SOQL query to bring only a specific subset of records into Audiences.

A record subset import works alongside any standard Salesforce import. You can add multiple named subsets for the same object type, each with its own SOQL query, and they sync independently.

**To add a record subset import:**

1.  Click `Add data` → `Add Source` → select your Salesforce integration.
2.  Select the Salesforce **object type** you want to import (Contact, Account, Lead, or Opportunity).
3.  Under **Record selection**, select **Record subset** instead of **All records**.
4.  Enter a **Subset name** — for example, `US Enterprise Accounts`. This appears as the source label in Settings and in your Sources list.
5.  Write a **SOQL query** that filters to the records you want. Your query must include `Id`, `SystemModstamp`, and `IsDeleted` so Clay can track changes and deletions. Example:
    ```
    SELECT Id, Name, Industry, BillingCountry, AnnualRevenue, SystemModstamp, IsDeleted
    FROM Account
    WHERE BillingCountry = 'US' AND AnnualRevenue > 1000000
    ```
    -   To generate a query from a plain-language description, click **Generate with AI** and describe what you need (for example, "US accounts with annual revenue over $1M"). Clay drafts the SOQL for you — review and adjust the result before continuing.
    -   Click **Preview** to verify a sample of matching records before saving.
6.  Map the SOQL fields to Audience columns.
7.  Click **Save** to activate the import.

**Multiple subsets:** You can add more than one record subset for the same Salesforce object type. Each appears as a separate named entry under your Salesforce source in Settings and syncs independently.

**Sync timing:** SOQL record subset imports follow the same schedule as standard Salesforce imports — incremental sync every 15 minutes on Enterprise plans, plus a full sync every 7 days. Clay uses the `SystemModstamp` field to detect which records changed since the last sync.

### Importing from HubSpot

**Note:** Setup must be completed separately for Contacts, Companies, and Deals. HubSpot Deal import is currently in early access — contact your Growth Strategist to enable it for your workspace.

1.  Click `Add data` → `Add Source` → select your [**HubSpot integration**](https://university.clay.com/docs/hubspot-integration-overview).
2.  Select `Contacts` at the top of the sync panel.
3.  Enable the `Import` toggle.
4.  Add any HubSpot fields you want to segment by — only fields included here will appear as columns and filter options in your Audience.
5.  Name the corresponding Clay fields — these become the column names in Audiences.
6.  Select `Companies` and repeat steps 3–5 for accounts.
7.  To import Deals (if enabled for your workspace), select `Deals` at the top of the sync panel.
8.  Enable the `Import` toggle.
9.  Add any Deal fields you want to filter or segment by — common fields include `Deal Stage`, `Amount`, `Close Date`, and `Owner`.
    -   Deal data is associated with both your Companies and People records. In a Companies audience, you can filter by deal attributes. In a People audience, only contacts directly linked to a deal via HubSpot contact associations appear when you filter on deal attributes — not all contacts at the company that owns the deal.
10.  Name the corresponding Clay fields.
11.  Click `Save and Preview`, then `Confirm`.

**Troubleshooting — "Export permission required":** If the HubSpot account you select is missing the **Export CRM data** permission, Clay displays a warning and disables the Connect button. Click **Re-authorize HubSpot** in the warning to reconnect your account with the required permission enabled, then continue setup.

**Sync timing and behavior**

HubSpot data sync in Audiences is currently in open beta — contact your Growth Strategist to enable it for your workspace.

Clay syncs data from HubSpot automatically on the following schedules:

-   **Incremental sync:** Runs every **15 minutes** on Enterprise workspaces, or **once daily** on Growth workspaces. Picks up new and changed HubSpot records since the last sync.
-   **Full sync (every 7 days):** Re-reads all records from HubSpot and reconciles deleted records — catching anything the incremental sync may have missed.

**Record scope:** The HubSpot Audiences connector imports all records for the object type you select — there is no option to pre-filter to a specific HubSpot list within the Audiences source setup. If your HubSpot has more records than your plan's limit (250,000 for Growth; 25,000,000 for Enterprise), see [My HubSpot has more records than my plan limit — how do I limit what gets imported?](#my-hubspot-has-more-records-than-my-plan-limit--how-do-i-limit-whats-imported) in the FAQs below.

**Write-back to HubSpot:** Unlike Salesforce, the HubSpot source in Audiences does not include per-field export rules or a scheduled export toggle — there is no write-back configuration in the HubSpot source settings panel. To push enriched data from Audiences to HubSpot, use a Bulk Enrichment Table with a HubSpot action column — see [How do I write enriched data back to HubSpot from Audiences?](#how-do-i-write-enriched-data-back-to-hubspot-from-audiences) in the FAQs below.

### Importing from Snowflake

1.  Click `Add data` → `Import from Snowflake`.
2.  Enter your connection details and SQL query.
    -   Click `Test` to preview your data before continuing.
3.  Confirm the preview looks correct, then click `Continue`.
4.  Define the `Unique Identifier`:
    -   For People: `email` or `user_id`.
    -   For Companies: `company_id` or `domain`.
5.  (Optional) Configure a `Timestamp Field` for incremental syncing:
    -   With a timestamp: syncs run every **15 minutes** and only import new/changed records.
    -   Without a timestamp: the full query reruns every **12 hours**.
6.  Map your Snowflake columns to Audience fields.
7.  Review and click `Confirm` — Clay begins importing immediately.
8.  Monitor the import. If records don't appear immediately, refresh the page to see the latest count.

**Sync timing and behavior**

Clay syncs data from Snowflake on the following schedules:

-   **Incremental sync:** Runs every **15 minutes** when a `Timestamp Field` is configured (for example, `updatedAt`), importing only records that are new or changed since the last sync. Without a timestamp field, the full SQL query reruns every **12 hours**.
-   **Full sync (every 7 days):** Re-reads all records and reconciles deleted records — catching anything the incremental sync may have missed.

**Deleted records:** When a record is no longer returned by your Snowflake import query — either because it was physically removed from the underlying Snowflake table, or because you updated your SQL to exclude it — Clay marks the record's Snowflake source association as **Deleted in source** during the next full sync. The audience record itself is **not removed**. To clean up these records, see [How do I archive records that no longer match my Snowflake import query?](#how-do-i-archive-records-that-no-longer-match-my-snowflake-import-query) below.

### Importing from Google BigQuery

**Note:** Google BigQuery import is currently in early access — contact your Growth Strategist to enable it for your workspace.

1.  Click `Add data` → `Add Source` → select your [**Google BigQuery integration**](https://university.clay.com/docs/google-bigquery-integration).
    -   If you haven't connected BigQuery yet, click `+ Add account` and upload your service account JSON key file. See the [Google BigQuery integration](https://university.clay.com/docs/google-bigquery-integration) for setup instructions.
2.  Enter a SQL `SELECT` query to define which records to import (for example, `SELECT * FROM \`project.dataset.table\` WHERE created_at > "2024-01-01"`).
    -   Click `Test` to preview your data before continuing.
3.  Confirm the preview looks correct, then click `Continue`.
4.  Define the `Unique Identifier`:
    -   For People: `email` or `user_id`.
    -   For Companies: `company_id` or `domain`.
5.  (Optional) Configure a `Timestamp Field` for incremental syncing:
    -   With a timestamp: syncs run every **15 minutes** and only import new/changed records.
    -   Without a timestamp: the full query reruns every **12 hours**.
6.  Map your BigQuery columns to Audience fields.
7.  Review and click `Confirm` — Clay begins importing immediately.

**Sync timing and behavior**

Clay syncs data from Google BigQuery on the following schedules:

-   **Incremental sync:** Runs every **15 minutes** when a `Timestamp Field` is configured, importing only records that are new or changed since the last sync. Without a timestamp field, the full SQL query reruns every **12 hours**.
-   **Full sync (every 7 days):** Re-reads all records and reconciles deleted records — catching anything the incremental sync may have missed.

### Importing from people and companies search

1.  Click `Add data` → `Find people` or `Find companies` to open a search.
2.  Narrow your search using parameters like `Job title` and `Experience`.
3.  Click `Continue` → `Save to People/Companies`.
    -   Note: This sends your search results to a draft version—it won't combine them with your existing Audience data.
    -   If the draft shows a banner that says **"X records from this search are already in the All People list,"** those records are already excluded from the merge. Clicking **All people** in step 5 will only add net-new contacts — the existing records are not duplicated.
4.  In your draft, click `Enrich` to bulk enrich and refine your data, keeping only high-quality leads.
5.  When your search data looks good, click `All people` to merge.

**Note:** When you save a search to your Audience, only basic identity fields are carried over as columns — additional data fields visible in the search preview (such as Company Size or Annual Revenue for companies, or Job Title for people) are not automatically added to your Audience. To add one of these fields, create it as a custom Audience field first: see [How do I create a custom Audience field that isn't tied to Salesforce?](#how-do-i-create-a-custom-audience-field-that-isnt-tied-to-salesforce) below.

**Note:** A search import only populates field values for companies or people that are **new** to your Audience. Records already in your Audience from Salesforce, Snowflake, or another higher-priority source keep their existing field values — Clay's search data has lower precedence and will not overwrite them. To populate or update a field (such as Industry) on records that already exist in your Audience, bring the search results into a Clay table and use the `Upsert Audiences Record` action to push those values to matching records.

**Excluding people (or companies) from your search**

The search setup includes an **Excluded people** panel (or **Excluded companies** for a Find Companies search) where you can specify up to 3 audiences to suppress from the results. Clay filters out any result that matches a record in your exclusion audience before importing.

**Exclusions match by LinkedIn URL or email only** — not by job title, name, or other fields. If a record in your exclusion audience has neither a LinkedIn URL nor an email, Clay cannot resolve it to a Clay person profile and that record will not be excluded from the search results. For example, an exclusion audience of "all Salesforce contacts with a title" will only suppress contacts who have a matching LinkedIn URL or email on their record in the exclusion audience.

**Exclusions operate within Clay only.** The exclusion prevents matching records from being imported into your Audience — it does not affect CRM write-back. When Clay exports enriched records to Salesforce or another CRM, whether a duplicate is created is determined by your CRM's own deduplication and upsert rules, not by the Clay exclusion. To prevent duplicate records in Salesforce, configure matching and deduplication rules in Salesforce directly.

### Importing from CSV

You can import a CSV file of people or companies as a one-time import into Audiences.

1.  Click `Add data` → `Add Source` → select **CSV**.
2.  Name your import, select whether you're importing **People** or **Companies**, and upload your CSV file.
3.  On the mapping screen, set the **Unique identifier** — the CSV column that uniquely identifies each record (such as email for People or domain for Companies). This determines whether an incoming row updates an existing record or creates a new one.
    -   On a people import, a **Company association** field appears as an optional setting. Point it at the column holding each person's company ID to link them to their company records in Audiences.
4.  Map your remaining CSV columns to Audience fields. Click **Auto-map** to automatically suggest mappings based on column names, or **Add mapping** to add a row and configure it manually.
5.  Click **Import** to complete the import.

CSV imports are one-time — they do not re-sync automatically. To update your Audience with new CSV data, repeat the import process with an updated file.

**To replace a CSV import with corrected data:** If the imported CSV contained errors and you want to start fresh, archive the old records before importing the updated file — see [How do I replace a CSV import with updated data?](#how-do-i-replace-a-csv-import-with-updated-data) in the FAQs below.

**Note:** CSV source entries remain listed in the Sources tab after import. There is no self-serve option to remove or disconnect a CSV source listing — it is retained for filtering and audit purposes.

### Sending data from Clay table

You can also send contacts from any existing Clay table directly to your Audience:

1.  Open any table with contacts you want to save to your Audience.
2.  Click `Continue` at the bottom of the table.
3.  Select `Save to People` or `Save to Companies` depending on the record type.
4.  Map your table columns to Audience fields in the field mapping step. Click **Auto-map** to automatically suggest mappings based on column names — Clay matches existing Audience fields and creates new ones where necessary.

Records saved from tables are automatically deduplicated and merged with your existing audience data.

**Starting from Audiences instead:** you can also pull a table in from the `Add data` sidebar.

1.  Click `Add data` → `Add source` → `Clay table`.
2.  On `Select a Clay table`, enter a `Source name` and choose the `Audience type` (People or Companies), then pick the `People table` or `Companies table` and the `View` holding the records you want.
3.  Click `Next`, then map your columns on `Field mapping` — `Clay People` or `Clay Companies` against `Table columns`.
4.  Click `Import`.

**To add enriched data to existing Audience records:** If you enriched companies or people in a Clay table — for example, adding website traffic, technographic data, or any other enrichment — and want those values to appear on records already in your Audience, use `Upsert Audiences Record` (available on Launch, Growth, and Enterprise plans) as an action column in the table instead. In the table, click `Add enrichment` and search for `Upsert Audiences Record` — it creates a new record in Audiences if no match is found, or updates the matching record's fields if one is found. See [Using Audiences from a Clay table](#adding-enrichments) below for the full list of table ↔ Audience actions.