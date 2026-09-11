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

**SOQL requirements for record subset imports**

SOQL queries for Audiences must be valid SELECT statements and must include `Id`, `SystemModstamp`, and `IsDeleted`. Clay uses these fields to handle incremental syncing and soft-delete detection. For Contact queries, also include `AccountId`; for Lead queries, also include `ConvertedContactId`. The AI query generator includes these fields automatically.

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

### Entity resolution and deduplication

Audiences uses two systems to prevent duplicate records:

**Entity Resolution (automatic)**

Entity Resolution runs continuously in the background. It matches records by identifier strength:

-   **For People:** LinkedIn URL → Email → Probabilistic matching (name + company + location + role)
-   **For Companies:** LinkedIn URL → Domain → Probabilistic matching (name + location + industry)

When a match is found, records merge into a single unified record in Audiences. **Deduplication happens in Clay only** — Audiences does not merge or alter records in your connected Salesforce org.

Records need a high-confidence identifier to match. Auto-enrichment adds `LinkedIn URL` and `CPJ ID` at no cost to improve matching.

**Import record matching (beta)**

When importing from Salesforce or Snowflake, you can configure **Import record matching** to deduplicate records at ingestion time. This feature is currently in beta — contact your Growth Strategist to enable it for your workspace.

**Example:** If you're importing from both Snowflake and Salesforce, setting `domain` as your alias field ensures that a single company row in your Audiences reflects data from both sources — rather than creating two separate records for the same company.

To configure:

1. In your import settings, find `Import record matching` and click `Edit`.
2. Under `When`, choose an **alias field** — typically `Domain` for Companies or `Email` for People (additional options include LinkedIn URL, phone number, and others).
3. Under `In`, map the alias field to the corresponding field in each connected source.
4. When a new record arrives, Audiences checks whether the alias value already exists. If it does, the new data is merged with the existing record instead of creating a duplicate.

You can configure one alias field per entity type (one for People, one for Companies). This setting applies to records imported *after* it is enabled — it does not retroactively merge records already in Audiences.

**Unique Identifier vs. alias field (Snowflake and BigQuery imports)**

When setting up a Snowflake or BigQuery import, you also define a `Unique Identifier` — a field that must be completely unique and non-null across your dataset (for example, `domain` or `work_email_domain` for companies; `email` for people). Clay uses this to determine whether an incoming row should create a new Audiences record or update an existing one. This is distinct from the alias field used in import record matching (beta): the Unique Identifier governs record creation and updates within a single source, while the alias field controls how Clay joins records across multiple sources.

**Other deduplication behaviors**

-   **Cross-source deduplication** — merge the same person from multiple sources.
-   **Whitespace detection** — when importing from a Find People or Find Companies search, or saving results from a Clay table to your Audience, records that already exist in All People or All Companies are automatically excluded from the merge. The draft shows a banner with the count of excluded records, and clicking **All people** or **All companies** will only add net-new records. For Companies, exclusion matches on Clay's internal company identifier (CPJ ID). Existing Audience records need entity resolution to have completed — records missing a recognized domain or professional network URL may not yet have been assigned a CPJ ID, which can cause them to slip through as apparent duplicates. Ensuring your Companies audience records have accurate domains and professional network URLs helps entity resolution complete and improves deduplication coverage.
-   **Country-code domain variants** — Clay's entity matching normalizes domains by stripping subdomains and `www` prefixes, but does not automatically merge country-code TLD variants. A company at `swarovski.co.uk` and a company at `swarovski.com` are treated as separate entities by default — this reflects how many enterprises maintain distinct regional accounts. If a regional variant appears as net new in your search results and you want to exclude it, use the **Exclude companies** filter in your Find Companies source. See [Find Companies](find-companies.md) for how to set up exclusions.
-   **Secondary domains from your CRM** — Clay entity matching uses only the primary domain field mapped from your CRM source. If your CRM stores additional domains for a company (for example, HubSpot's secondary domain fields), those alternate domains are not imported into the Audiences company record and are not used for entity matching. A Find Companies search result for a secondary domain may appear as net new even if the same company exists in your audience under a different primary domain. To exclude known secondary domains from appearing as net new, add them to the **Exclude companies** filter in your Find Companies source.

Deduplication across sources is automatic. Within Salesforce, it uses SFDC IDs — org duplicates carry over as-is.

**Record persistence when a source is removed**

When a record disappears from a source — for example, a row is deleted from a Clay table, or the table itself is removed — the corresponding Audience record is **not deleted**. Clay marks the record's association with that source as removed, but the record itself persists in Audiences. If the same record exists in multiple sources and disappears from one, it remains in Audiences as long as it is associated with at least one other source. Removing the entire source table does not remove those records from your Audience.

To remove a record from Audiences entirely, archive it manually — see [How do I remove records from an audience?](#how-do-i-remove-records-from-an-audience).

**Conflict resolution when sources provide different field values**

When two data sources write different values to the same field on an Audience record, Clay resolves the conflict using a fixed priority order. Higher-priority source types win; within the same priority tier, the most recently updated value wins.

| Priority | Source types |
|---|---|
| 1 (highest) | Upsert Audiences Record, Bulk Enrichments |
| 2 | Salesforce (Account, Contact, Opportunity), HubSpot |
| 3 | Salesforce (Lead) |
| 4 | Snowflake, BigQuery |
| 5 | CSV |
| 6 (lowest) | Find Companies / Find People search |

There is an optional **CSV-first override** that, when enabled for a workspace, promotes CSV to priority tier 2 — above Salesforce and HubSpot but below Upsert Audiences Record and Bulk Enrichments. Contact your Growth Strategist to enable it.

**When merging happens**

Merging two Audience records into one happens only at the time of a record upsert or import — not when an existing field is later updated with a matching value. For example, if one company record has a null domain and another has `mpsworks.com`, those two records are not automatically merged when a later enrichment fills the first record's domain with `mpsworks.com`. The two records stay separate. To merge them, re-import or re-upsert the record so that the matching identifier is present at ingestion time.

## Creating an audience

After importing, you will want to create new audiences, so you can appropriately target the right contacts.

**Admin access required.** Creating, editing, and deleting audience segments is available to workspace Admins only. Editors and Viewers can view and filter existing segments but cannot create new ones.

To create a new audience:

1.  Click `People` or `Companies` in the left sidebar.
2.  Click **New audience** in the top-right corner of the list, or click the `+` next to `My Audiences` in the sidebar.
3.  Select `Criteria` and then add a `Filter` or `Filter group`.
    -   **Filters** evaluate a single condition at a time. All top-level filters are joined with AND — a record must match every one.
    -   **Filter groups** combine multiple conditions using their own AND/OR logic. Within a single filter group, all conditions share the same operator — all AND or all OR; changing the operator in the group header switches all conditions at once. To mix AND and OR, use a nested filter group. For example, to build `A AND B AND (C OR D)`: add A and B as top-level filters, click **`+ Filter group`**, then add C and D inside the group. Once the group contains two or more conditions, a small **`and`** button appears between them — click it to switch to **`or`**.

**Filtering by CRM and data warehouse properties:** All fields synced from your CRM (Salesforce, HubSpot) or data warehouse are available as filter options alongside Clay's built-in fields — you are not limited to Clay's native properties. When you click **+ Filter**, type the property name in the search box to find it. For example, to build a Companies segment of your existing customers, add a filter on the field in your CRM that tracks account type (such as **Account Type** in Salesforce) and set the value to `Customer`. Any field included in your import field mapping appears in the filter picker after the next sync completes. If a CRM field isn't showing up in the filter list, see [A Salesforce field isn't appearing in my audience filters — how do I add it?](#a-salesforce-field-isnt-appearing-in-my-audience-filters--how-do-i-add-it) in the FAQs below.

### Filter operators by field type

The operators available when building a filter depend on the field's data type, shown by the icon next to the field name:

-   **Text fields (T icon)** — support text-matching operators. To match multiple values at once, use **`contains any of`** and enter each value — up to 10 values per filter. For example, to include records where Industry is Health, Beauty, or Pets, set the filter to `Industry → contains any of → Health, Beauty, Pets`. A **`does not contain any of`** multi-value exclusion operator is not available. To exclude multiple values, add a separate **`doesn't contain`** filter for each value — top-level filters are joined with AND by default, so each additional condition narrows the results.
-   **Number fields (# icon)** — support range operators: **`is greater than`**, **`is less than`**, **`is greater than or equal to`**, and **`is less than or equal to`**. For example, `Employees → is greater than → 500`.
-   **Date fields** — support time-based operators: **`within the last`**, **`not within the last`**, **`before`**, and **`after`**. For "within the last" and "not within the last," specify a number of days, weeks, or months as the lookback window. For example, `Created at → within the last → 30 days` targets records created in the past 30 days.
-   **Boolean (true/false) fields** — support **`is true`** and **`is false`** operators. To apply OR logic across two boolean conditions (for example, `field A is true OR field B is true`), add both filters inside a filter group and click the **`and`** connector between them to switch it to **`or`**.

**Note:** A field that appears numeric may have been imported as text (shown by a T icon rather than #). Text fields — such as "Annual revenue range" synced from Salesforce as a string — will not show range operators. To use range filtering on a field, contact Clay support to have the field's type changed to Number (#). Range operators will then appear when you add a filter on that field.

## Finding people from a Companies Audience

Once you have a Companies Audience segment, you can run a people search scoped strictly to the companies in that segment — without needing a separate company table.

**To find people from a Companies Audience segment:**

1.  Click **Companies** in the left sidebar and open the segment you want to search.
2.  Click the **⋮** (three-dot) menu at the top right of the audience view — or click the **⋮** menu next to the segment name in the sidebar.
3.  Select **Find people from this list**.
4.  In the setup panel, apply filters for job title, seniority, location, and experience.
5.  Click **Continue**. Clay searches for matching contacts at the companies currently in that segment.

The search is scoped to the exact companies in the segment at run time. In the final step of the wizard, click **Send to Audiences** to add the contacts to your People Audience. You can then run bulk enrichments (for example, work email or phone) and export them to an ad platform — see [Syncing audiences to ad platforms](#syncing-audiences-to-ad-platforms).

**Note:** **Find people from this list** is available only on Companies Audience segments — it does not appear on People Audience segments.

**Note:** You can also run a standalone **Find People** search from any workbook and set **Target companies** to a Companies Audience segment — the segment appears alongside Clay tables in the company picker, and the search is free. Both paths open the same Find People wizard; in the final step, click **Send to Audiences** to add contacts to your People Audience, or **Import to Table** to create a new Clay table. The main difference is that **Find people from this list** pre-scopes the search to the companies in the current segment, while standalone Find People requires you to set the Target companies filter yourself. **Note:** The option to use a Companies Audience segment as the Target companies filter in standalone Find People requires Audiences to be enabled on your workspace (available on Launch, Growth, and Enterprise plans).

## Enriching and monitoring

### Adding enrichments

Bulk enrichments add contact data, firmographics, technographics, and more to your audience records at scale. They run on an audience and write results permanently back to All People — not just the segment you ran them from. This means any enriched field is immediately available as a filter in any other segment.

**Admin access required.** Adding and managing bulk enrichments requires workspace Admin access.

**To add an enrichment:**

1.  Navigate to an audience and click `Enrich` → `Add bulk enrich`.
2.  Add enrichment columns as you normally would (e.g., `Enrich Person` for LinkedIn URL, title, phone).
3.  Test on a small batch first — click `Run on 10 rows` to verify output before running at scale.
4.  Open `Field Mapping` and map each column you want to save back to Audiences:
    -   Enable the auto-enrich toggle so that any new record entering this segment is automatically passed through the enrichment — typically within 15 minutes.
5.  Click `Start Run`.

**Note:** To run a bulk enrichment on Audience data, always start from within the Audience — click `Enrich` → `Add bulk enrich` from any segment view. When creating a new Bulk Enrichment from the Clay homepage (`New` → `Bulk enrichment`), the source type options are CSV and Salesforce CRM only — there is no "Audiences" source type in that dialog. The Audience segment serves as the source when you add the enrichment from within Audiences.

**Note:** Clay does not impose rate limits on Audiences bulk enrichments — the system is built to handle large lists at scale. Third-party data providers (such as Clearbit or Apollo) apply their own rate limits, but Clay queues requests and manages these automatically in the background. If you supply personal API keys for a provider, those keys' own rate limits apply.

**To run an existing enrichment on another segment without recreating it:** A single bulk enrichment can be connected to multiple segments — you do not need to recreate it for each one. Open the enrichment from the **Enrich** sidebar and use the **Add segment** option in the Run Setup panel to include additional segments. See [Adding a segment to an existing enrichment](bulk-enrichment.md#adding-a-segment-to-an-existing-enrichment) for full steps.

**Using Audiences from a Clay table:**

Four Clay actions let you move data between a Clay table and your Audience directly.

-   In any Clay table, click `Add enrichment` and search for:
    -   `Upsert Audiences Record` pushes records from a table into your Audience — creating a new record if no match exists, or updating an existing one if a match is found. Use it to commit data from integrations not yet natively supported in Audiences, qualify event lists in a table before adding them to your Audience, or migrate enrichment work already done in a table.
    -   `Update Audiences Record` writes data from a table row to one or more fields on an existing Audience record. Unlike `Upsert Audiences Record`, it does not create a new record if no match is found. Both actions write only to fields that already exist in your Audience — to create a new custom field first, see [How do I create a custom Audience field that isn't tied to Salesforce?](#how-do-i-create-a-custom-audience-field-that-isnt-tied-to-salesforce) below.
    -   `Lookup in Audiences` pulls data from your Audience into a table row. Use it to reference enriched or signal data in a table workflow without making Salesforce API calls. By default, signal data is returned for the past **90 days** and the action returns **5 signal results** per record by default — adjust the **Signal data to include (days)** setting in the column settings to retrieve older signals, or increase the result limit (up to 50) when you need more results per record. Use `Get Audiences Activity` when you need a larger set of results.
    -   `Get Audiences Activity` retrieves signal and activity data for an Audiences record — including signal events and, if Gong is connected to your workspace, Gong call records. Use it when you need more results or want to query a longer time window than `Lookup in Audiences` provides by default. Set **Object type** (People or Companies) and map the Audiences **Record ID**; optionally filter by **Activity types** — for example, select `Job posting` to retrieve only job posting events, or leave it empty to return all types. Configure **Max activities per type** (default 5, max 200) and **Days lookback** (default 90, max 365). For job posting signals, each event includes the job title, URL, location, posted date, seniority, description, company name, and company domain — data you can parse in downstream columns to qualify and route companies based on the specific roles they are hiring for.

### Reviewing enrichment results

After a bulk enrichment runs, there are two ways to see which records were successfully enriched:

**View enrichment status and row-level results**

Click `Enrich` in the top-right toolbar to open the enrichments sidebar. The **Bulk enrichments** tab lists all your enrichments grouped as **Active** and **Inactive**. Each card shows a completion count — for example, "1,234 / 5,000 completed." Completed enrichments appear in the **Inactive** section.

If you're viewing a specific segment, use the dropdown at the top of the list to toggle between enrichments on this segment and enrichments across all audiences.

To inspect row-level results, click `⋮` on any enrichment card and select **Open bulk enrichment**. This opens the underlying bulk enrichment table where you can see each row's output and status.

The bulk enrichment table has two tabs at the top — **Queued rows** and **Errored rows** — that let you switch between rows waiting to process and rows that encountered an error. It is not possible to filter within the bulk enrichment by specific error type; the Errored rows tab shows all rows with errors together. To see the error message for a specific row, open the bulk enrichment, click the **Errored rows** tab, and hover over the relevant cell.

If a bulk enrichment was automatically paused after reaching a credit limit, click **Resume** in the bulk enrichment and select **From where you stopped** to continue processing the remaining rows without restarting from the beginning.

**Filter the audience by the enriched field**

Since enrichment results write permanently back to All People, you can filter any segment to see only records that received data:

1.  Add a filter to your audience.
2.  Select the enriched field (for example, `Phone` or `LinkedIn URL`).
3.  Set the operator to **`is not empty`** to show only records where the enrichment returned a value.

**Errored rows after a run**

In Audiences bulk enrichment, a row appears in the **Errored rows** tab when any of its action columns fail — for example, if a data provider returns no match for a domain. This is true even if the **Update Audiences Record** step succeeded and your data was already written back to Audiences. This is expected behavior, not a bug — Audiences treats a row as complete only when all configured action columns succeed.

To resolve errored rows:
-   **Rerun failed rows** — in the bulk enrichment table, right-click the failing column header → **Run column** → **Run [N] empty or out-of-date rows** to retry only records that didn't get a result.
-   **Remove non-critical provider columns** — if a provider consistently fails to match your records and the data isn't essential, removing that column from the bulk enrichment table means its failures will no longer mark rows as errored.

### Signals

Signals monitor your audience for key changes and write results permanently to each matching record so you can segment on them.

For **Companies** audiences, five built-in signal types are available:

-   **Web Intent** — track which companies are visiting your website.
-   **New Hire** — detect new hires at monitored companies within the last three months.
-   **News & Fundraising** — monitor funding rounds, mergers and acquisitions, strategic partnerships, product launches, and leadership changes.
-   **Job Posting** — alert when a monitored company posts a new job opening; Clay analyzes job descriptions for urgency indicators and geographic expansion signals.
-   **Company Topic Intent** (open beta) — monitor when companies show buying intent for topics you care about, with High, Medium, and Low scoring tiers. Cost: approximately 0.2 credits per account monitored. Contact your Growth Strategist to enable this signal for your workspace.

**Custom signals are not available within Audiences.** To track a more specific or custom signal (for example, website changes, RSS feed mentions, or technology adoption), build that logic in a bulk enrichment on the audience segment using Claygent or scheduled enrichment columns — see [Adding enrichments](#adding-enrichments) above.

**To add a signal to a segment:**

1.  Navigate to an audience and click `Enrich`.
2.  Click `Signals` → select a signal type (e.g., `New Hire`).
3.  Set the `look-back period` for the initial run: `3 months`, `6 months`, or `1 year`.
4.  Set the `recurrence frequency` — how often it re-runs going forward.
5.  Review the `cost preview per record` shown before the run begins.
6.  Click `Save and Run`.

After you add a signal:

-   Results write to a `dedicated signal column` on each matching record — stored permanently and globally (not scoped to this segment).
-   Clay **automatically creates a draft segment** for each signal type — named **New hires** (for New Hire signals), **Companies of job changers** (for Job Change signals), or **Web visitors** (for Web Intent signals). This segment is pinned at the top of the Audiences left sidebar and shows all records in your workspace that matched that signal type. It is a segment within Audiences, not a separate table.
-   Multiple signals each get their own column; the `Signal Summary` column aggregates all results. Click any row to see per-signal detail.
-   Any other segment that filters on this signal type will also surface these results.

**Monitoring signal progress**

While the signal is processing its initial run, its status shows **Running**. Once the initial run completes, the status flips to **Monitoring** and displays a **Last run** timestamp. To see how many records were detected, go to **Audiences** → **Data Hub** → **Signals** — the **Signals fired (30d)** column shows the count of events the signal emitted over the past 30 days.

**Note:** Audience-based signals appear in **Audiences → Data Hub → Signals** (within the Audiences section), not on the main **Signals** page accessible from the workspace left sidebar under Orchestration. The main Signals page shows only table-based signals — audience-based ones are managed here in the Audiences Data Hub.

To see which specific records in your audience were picked up by the signal, add a filter on your audience for the relevant results field (for example, **Job change results**). You can save that filtered view as a separate segment — or open the auto-created draft segment (**New hires**, **Companies of job changers**, or **Web visitors**) pinned at the top of the Audiences left sidebar.

**Enriching people who matched a signal**

To run an enrichment on the people who matched a signal:

1.  In Audiences, open the draft segment for your signal type — **New hires**, **Companies of job changers**, or **Web visitors** — pinned at the top of the Audiences left sidebar.
2.  Inside the segment, click **Enrich** → **Add bulk enrich**.
3.  Add your enrichment columns (for example, `Enrich Person` for LinkedIn URL, phone, or work email).
4.  Click **Start Run**.

Enrichment results write permanently back to All People — they are available as filters in any other segment going forward.

### Claygent-managed columns

In a **Companies** audience, columns written by a Claygent display a four-diamond icon in the column header. Workspace admins and members can click the column header and select **View Claygent** from the dropdown to open the configuration for the Claygent that populates that column. This option does not appear in People audiences or in archived audiences.

### Connecting a workflow to a segment

Connect a Clay workflow to a named audience segment — or to the entire workspace audience (**All People** or **All Companies**) — to automatically run it on every new member that enters. When a contact or company matches the segment's filters, the connected workflow starts within minutes. To run a workflow across your full workspace audience instead of a specific segment, open the trigger segment picker and select **All People** or **All Companies** from the top of the **All** tab — the workflow then triggers for every new person or company entering the workspace-wide audience.

**To connect a workflow:**

1.  Navigate to an audience segment and click `Send` → **Send to workflow**.
2.  In the modal, choose **New workflow** (to create one) or **Existing workflow** (to select from your workspace).
3.  The workflow appears as a card in the **Workflows** section of the sidebar with a **Draft** status.

**Activating the workflow**

The workflow card shows the current status — **Draft**, **Live**, or **Paused**. To activate it, click the **⋮** (three-dot) menu on the workflow card and select **Open in Workflows**, then click **Publish** in the top toolbar of the workflow editor. A dialog appears where you can name this version. If your workflow has an audience segment trigger, the dialog also shows a **Run on all members now** checkbox (with a count of the current segment members). Check this box to immediately run the workflow on every contact or company already in the segment as part of publishing — leave it unchecked to have the workflow trigger only for new members that join the segment going forward. Publishing the workflow activates all connected triggers — new segment members will run through the workflow automatically once it is live.

**Running a workflow on existing segment members**

To manually run the workflow on segment members already in the segment, open the workflow in the editor and use the **Run** dropdown on the trigger card:

-   **Run [X] [members]** — runs the workflow on a sample of up to 10 current segment members. Shown only when the segment has more than 10 members.
-   **Run all [X] [members]** — runs the workflow on all current segment members.

The **Run** button is available in any trigger state — draft, live, or paused — so you can run the workflow on existing members before or after publishing.

**Testing a workflow on specific records**

To test a workflow on hand-picked records — rather than an automatic sample — use the **Add data** button in the test data panel at the bottom of the workflow editor:

1.  Open the workflow in the editor and locate the test panel at the bottom of the screen.
2.  Click **Add data** and select an audience segment from the dropdown.
3.  In the record picker, search for and check the specific records you want to include. You can select up to **50 records** total.
4.  Click **Run [N] rows** to run the workflow on your selected records only.

Selected records are merged with any existing test records for the trigger — duplicates across sources are removed automatically. You can add records from multiple connected audience segments.

### **Syncing audiences to ad platforms**

When you have a segment ready, you can sync it to an ad platform to run account-based advertising across your highest-fit contacts and companies.

1.  Click `Send` → `Export action`.
2.  Click `Sync to ad platforms`.

**How you might use this:**

-   **Account-based advertising** — sync company segments to the professional network, which is the only ad platform that supports account-level (company) targeting. Meta, Google Ads, Bing Ads, Reddit Ads, and Vibe.co support People (contact-level) segments only — to use those platforms, sync a People segment instead. Contacts who no longer qualify are automatically removed.

**Syncing to multiple ad platforms**

You can add multiple ad platforms to a single audience sync. After your initial sync is active, an **Expand your reach** section appears on the Sync tab showing available platforms you haven't yet connected. Click **Add** next to any platform to configure field mappings for that provider — it will sync on the same schedule as your existing provider.

**Notes:**
-   You cannot add a platform while a sync is currently in progress — wait for the active sync to complete first.
-   Google Ads and Bing Ads are only available for audiences sourced from first-party data (your own CRM or data warehouse). If your audience uses Clay's company/people search (CPJ) data, Google Ads and Bing Ads will not be available to add.

**Enhanced Matching (Beta)**

Enhanced Matching improves ad platform match rates by looking up hashed personal email addresses for your contacts via Clay's provider network and sending up to three per record to the connected ad platform. It is currently in beta — contact your Growth Strategist to enable it for your workspace.

When setting up an Audiences → Ads sync, the **Map** step includes an Enhanced Matching panel where you choose a tier:

| Tier | Cost (modern plans) | Cost (legacy plans) | Expected match rates |
|------|---------------------|---------------------|---------------------|
| **Premium** | 2 credits/row | 3 credits/row | Professional network ≤ 95%, Meta ≤ 65% |
| **Standard** | 1 credit/row | 2 credits/row | Professional network ≤ 80%, Meta ≤ 50% |
| **None** | 0 credits | 0 credits | Professional network < 60%, Meta < 30% |

Modern plans include Launch, Growth, and post-2026-pricing-change Enterprise. Legacy Enterprise (EnterpriseApril2023) plans are charged the legacy rates above.

With **Premium** or **Standard**, Clay queries its provider network to find and hash personal emails for each contact automatically. With **None**, you manually map up to three existing hashed email columns from your Audience under **Include emails**.

**Hashed email limit:** All tiers support a maximum of **3 hashed email fields** per contact. If a contact has more than 3 personal email addresses available, only the first three are sent to the ad platform — there is no way to include additional emails beyond this limit.

**Professional network behavior:** The professional network creates a separate audience entry per hashed email address, so your audience size on that platform may exceed your contact count after a sync. This is expected — it means one contact was matched via multiple email addresses.

### Exporting a segment to a workbook table (Beta)

**Currently in beta — available to Enterprise plan workspaces by request.** Contact your Growth Strategist or Clay support to enable this feature for your workspace.

You can export a segment to a Clay workbook table, creating a view of your segment's members that updates automatically as the segment changes. Each record that joins the segment becomes a new row in the linked table.

**To export a segment to a workbook table:**

1.  Navigate to an audience segment.
2.  Click `Send` → **Add to workbook**.
3.  Enter a table name, optionally assign a credit budget, and click **Continue**.

Clay creates the workbook table immediately and queues the initial import.

**Sync behavior:** New contacts or companies that join the segment are automatically added as new rows to the workbook table, usually **within 20 minutes** of joining the segment. No manual trigger or import run is required.

**Import schedule:** The import schedule is not configurable from the workbook table. Clicking the import schedule setting on a table backed by an Audience segment returns you to the Audience segment — the sync timing is managed automatically. There is no way to trigger an on-demand import or adjust the schedule interval from the table itself.

**Table size limit:** Due to Clay table size limits, only the first **50,000 records** from the segment are imported.

**Columns in the table:** The initial table contains three columns — **Name**, **Domain** (for Companies) or **Email** (for People), and **LinkedIn URL**. The underlying source cell for each row stores all current Audience field values. Fields added to your Audience segment after the table was first created do not automatically appear as new columns in that existing table — see [Why aren't new Audience fields appearing as columns in my linked workbook table?](#why-arent-new-audience-fields-appearing-as-columns-in-my-linked-workbook-table) in the FAQs below.

## Writing back to your CRM
