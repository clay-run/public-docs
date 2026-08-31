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
| Export a segment to a Clay workbook or campaign | ✓ | ✓ | — |

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
2.  Select your Salesforce account from the dropdown — or click `+ Add account` to authenticate a new one.
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

**Enrichment workflows (beta):** Some workspaces include a **Create enrichment workflow** option in the `Enrich` menu when viewing a People or Companies audience. This option — currently in beta — opens a workflow builder pre-configured with your audience segment as the source. Add an **Enrich** step, configure the enrichment columns you need, and click **Run**; results write permanently back to your Audience records. If you don't see this option, use `Enrich` → `Add bulk enrich` as described above. You can also set up the same enrichment directly from **Workflows**: create a new workflow, select your People or Companies audience as the source/trigger, add an **Enrich** step, configure the columns, and run it.

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

The workflow card shows the current status — **Draft**, **Live**, or **Paused**. To activate it, click the **⋮** (three-dot) menu on the workflow card and select **Open in Workflows**, then click **Publish** in the top toolbar of the workflow editor. Publishing the workflow activates all connected triggers — new segment members will run through the workflow automatically once it is live.

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

-   **Account-based advertising** — sync company segments to LinkedIn, Meta, Google Ads, Bing Ads, Reddit Ads, or Vibe.co. Contacts who no longer qualify are automatically removed.

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

## Writing back to your CRM

**Note:** Salesforce is currently the only native export destination in Audiences. HubSpot export from Audiences is not yet available — to write data to HubSpot, see [How do I write enriched data back to HubSpot from Audiences?](#how-do-i-write-enriched-data-back-to-hubspot-from-audiences) in the FAQs below.

Audiences supports **bidirectional sync** with Salesforce. To push data from Audiences back to Salesforce, you must first enable the **Export sync** toggle in your Salesforce source settings — this is the master switch for all outbound writes. Even if individual fields are configured with an "Always write" rule, no data flows to Salesforce until Export sync is turned on.

**To enable Export sync (admin-only):**

1.  Go to **Settings** → **Sources / Destinations** and click your Salesforce connection.
2.  Select the object tab you want to export (for example, **Accounts**).
3.  Under **Export [Object] data**, toggle on **Export sync**.
4.  Confirm your field mappings and click **Save and review** → **Confirm**.

Map any Clay data or segment membership to Salesforce fields. Examples:

-   Personal email → SFDC `Personal Email` field.
-   Segment membership → CRM status, campaign enrollment, lead score, or owner assignment.

**Field-level write rules**

Each mapped field has a write rule that controls whether and how Clay pushes its value to Salesforce during an export:

| Rule | Behavior |
|------|----------|
| **Never write** | Clay never exports this field to Salesforce. This is the **default** for all newly added field mappings. |
| **Always write** | Clay writes the current Audiences value to Salesforce on every export cycle, overwriting whatever is in the Salesforce field. |
| **Write if empty** | Clay writes the value only if the corresponding Salesforce field is currently empty. Existing Salesforce values are preserved. |

To change a field's write rule, click the **pencil (edit) icon** next to any mapped field in your Salesforce source settings.

**Important:** Because **Never write** is the default, a newly mapped field will not export data until you explicitly change its write rule. If a specific field isn't showing up in Salesforce after enabling Export sync, confirm its write rule is set to **Always write** or **Write if empty**.

Export settings also control whether Clay **creates new Salesforce records** for Audience records that don't yet have an SFDC match, or **only updates existing ones**.

The **`Create new Salesforce records`** toggle is in your Salesforce source settings under the export section. It is **off by default** — when off, Clay only updates Salesforce records that already have a matching entry in your Audience. Turn it on to allow Clay to create new **Accounts** or **Contacts** in Salesforce for any Audience record that doesn't already have a matching SFDC entry. (This toggle applies to Account and Contact object types only — Leads and Opportunities do not support record creation through this toggle.) This toggle is admin-only.

**What happens when you first enable this toggle:** Clay will attempt to create Salesforce records for *all* Audience records that currently lack a matching SFDC entry — not only records that enter the Audience going forward. For example, if your Companies Audience already contains 60,000 companies with only a subset matched to existing Salesforce Accounts, the first export will attempt to create Account records for all currently-unmatched companies. Test on a small, filtered segment first and verify your matching fields, required Salesforce fields, permissions, and Clay ID field mapping before enabling for a large Audience.

**Note:** Saving records to Audiences does not create anything in Salesforce. Record creation only happens once Export sync is enabled, field mappings are configured, and the `Create new Salesforce records` toggle is on.

Export sync behavior:

-   **Export frequency:** Once every 24 hours. Clay assigns each workspace a stable export time automatically — the schedule is not user-configurable.
-   **First export:** After you enable Export Sync, the first export does not run immediately — it fires at your workspace's next scheduled export time, which may be up to 24 hours away. The Exports panel shows **Not set up** until the first export completes successfully.
-   **Export batch size:** ~10,000 records per batch.
-   **Subsequent syncs:** Incremental — only changed records are processed.

To estimate API calls for initial export, divide record count by 10,000 and compare against your Salesforce limit.

**Note:** CRM export is admin-only. Enrichments and signals follow standard Clay table pricing.

## FAQs

### When should I use Audiences vs. a table?

Use Audiences by default for anything you want to reuse, segment on, or build automations on top of. Use tables for one-off workflows, integrations Audiences doesn't yet support natively, or cases where data doesn't need to persist beyond a single run.

The simplest framing: Tables are how you _work on_ data. Audiences is where your data _lives_. They work together — you still build and run workflows in Tables, they just pull from a cleaner, richer, always-current foundation.

|  | Clay Tables | Audiences |
| --- | --- | --- |
| Best for | One-off, one-time workflows | "Always-on" workflows that keep running |
| Role | How you work on data | Where your data lives |
| Scope | A specific working set you build and run | A slice across your entire dataset |
| Connections | Built per workflow | Continuously synced to your CRM, warehouse, and other sources |
| Scale | Up to 50,000 rows | Millions of records |

**Start with Audiences when:**

-   You want to sync contacts to an ad platform (LinkedIn Ads, Meta Ads) — Audiences is the recommended path for new ad targeting workflows. Table-based ad syncs are deprecated and display a deprecation notice in the product; Clay recommends using Audiences for all new ad sync setups.
-   You want a persistent, deduplicated contact and company database that merges data from your CRM, enrichments, and people searches and stays current over time.
-   You want to continuously enrich contacts and push the results back to your CRM automatically.
-   You're doing ongoing contact management rather than a one-time or exploratory project.

**Start with Tables when:**

-   You need complex multi-step enrichment logic — for example, conditional runs, waterfall enrichments, or AI scoring before deciding which contacts to keep.
-   You're running a one-time or exploratory enrichment project where you don't need to store results permanently.
-   You need fine-grained per-row automation — conditional logic, webhook triggers, or enrichment chains that reference each other.

**People sourcing for ad platform sync — recommended flow:**

1.  In your Companies Audience segment, click **⋮** → **Find people from this list**. Apply job title, seniority, and location filters. At the end of the wizard, click **Send to Audiences** to add the contacts to your People Audience at no credit cost.
    -   Alternatively, use the standalone **Find People** source (also free) with your Companies Audience as the **Target companies** filter (requires Launch, Growth, or Enterprise plan). The same wizard opens — click **Send to Audiences** to send contacts to your People Audience, or **Import to Table** if you prefer to review results first (then click **Continue → Save to People** from the table).
2.  From your People Audience, run **Bulk Enrich** to add the contact fields you need (for example, work email and phone number).
3.  Build a filtered segment from your enriched People Audience.
4.  Click **Send → Sync to ad platforms** to push the segment to LinkedIn Ads or Meta Ads. See [Syncing audiences to ad platforms](#syncing-audiences-to-ad-platforms).

### What if my integration isn't supported yet?

Use the `Upsert Audiences Record` table enrichment as a bridge. Bring your data into a Clay table from any source, then use Upsert to push those records permanently into your Audience. This works for any source Audiences doesn't yet natively support.

### How do I create a custom Audience field that isn't tied to Salesforce?

The `+ Add field` option is available in the `Update Audiences Record` column mapping inside a bulk enrichment table:

1.  Navigate to a segment and click `Enrich` → `Add bulk enrich`.
2.  In the bulk enrich table, click the `Update Audiences Record` column header to open the Configure panel.
3.  In the `Column mapping` dropdown, click `+ Add field`, name the new field, and save.

Once created, the field is immediately available as a filter in any segment and as a target for `Update Audiences Record` or `Upsert Audiences Record` from any Clay table.

**Note:** There is no option to add new fields directly from the Audience screen — you must go through the `Update Audiences Record` column mapping in a bulk enrichment table.

### How do I delete a custom field from Audiences?

Clicking a column header in the Audiences view (People or Companies) only shows **Hide** — there is no "Delete column" option in the column dropdown. To delete a custom field, use the **Data Hub**:

1.  In the left sidebar, click **Data Hub**.
2.  Select the **Fields** tab (it opens by default).
3.  Click the row for the field you want to delete — this opens the field settings sidebar.
4.  Click **Delete field** at the bottom of the sidebar.
5.  Confirm by clicking **Delete** in the dialog that appears.

The field is permanently removed and cannot be recovered.

**Note:** Only custom fields — fields you created yourself — can be deleted. Built-in fields from Salesforce, HubSpot, or other connected sources have the Delete field button disabled. To stop a field from appearing in your column view without deleting it, use **Hide field** instead (available from the same sidebar, or by clicking the column header and selecting **Hide**).

### A Salesforce field isn't appearing in my audience filters — how do I add it?

The answer depends on which type of Salesforce import you are using:

**All records imports:** Only fields explicitly included in the Salesforce import field mapping are brought into Audiences as columns and made available as filter options. If a Salesforce field — including custom fields like `Account_Record_ID__c` — doesn't appear in the filter dropdown, it was not included when the import was configured.

To add a missing field to an "All records" import:

1.  Click **Add data** in the top toolbar.
2.  Find your Salesforce integration and click the **⋮** (three-dot) menu next to it.
3.  Select **Settings**.
4.  In the field mapping section, add the Salesforce field you want and name the corresponding Clay column.
5.  Click **Save and review** → **Confirm**.

**Record subset (SOQL) imports:** Fields are determined by the `SELECT` clause of your SOQL query — only fields listed in the SELECT statement are imported. To add a new field, edit the SOQL query for that import to include the field in the SELECT clause, then reconfirm the import.

The filter option for the field becomes available after the next incremental sync (typically within 15 minutes). However, if you added this field to the mapping after your initial import, records that haven't been modified in Salesforce since the mapping was saved won't have data for the new field yet — see [I added a new Salesforce field to my mapping but some records are missing data for it](#i-added-a-new-salesforce-field-to-my-mapping-but-some-records-are-missing-data-for-it) below. Read-only Salesforce fields — fields shown with a lock icon in the mapping because Salesforce does not allow Clay to write them — can still be imported and used as filters. They will show a **Never write (Read-only)** export rule.

**If a field doesn't appear in the Settings mapping dropdown** (not just in the filter options): Clay fetches the available field list live from Salesforce each time you open the mapping settings — no reconnect or reauth is required for newly created Salesforce fields to appear. If a field you recently created in Salesforce still does not show up in the dropdown, the most likely cause is that the connected Salesforce OAuth user's profile lacks Field-Level Security (FLS) Read access to that field. Salesforce's describe API only returns fields the connected user can read, so any field blocked by FLS will be absent from Clay's dropdown regardless of when it was created. To fix it, ask your Salesforce admin to grant **Read** access to the field via **Setup** → **Profiles** (or **Permission Sets**) → the user's profile → **Object Settings** → **Field Permissions**. After permissions are updated, reopen the mapping settings and the field will appear.

### I added a new Salesforce field to my mapping but some records are missing data for it

When you add a field to your Salesforce import mapping after the initial import, the filter option for that field becomes available after the next incremental sync (typically within 15 minutes). However, existing records are **not** automatically backfilled — only records whose `SystemModstamp` has changed in Salesforce after the mapping was saved will be re-synced with the new field data.

If an existing record had a value for the field in Salesforce before you added the mapping, and that record hasn't been modified since, the value won't appear in your audience until either:

-   **The record is modified in Salesforce** — any change that updates `SystemModstamp` (a user edit, a workflow update, or an integration write-back) triggers the record to be re-synced on the next incremental sync (within 15 minutes). Making a small edit to the record in Salesforce is sufficient.
-   **The weekly full sync runs** — every 7 days, Clay re-reads all Salesforce records regardless of `SystemModstamp`. Missing field values are filled in automatically at that point.

**To fill in missing data immediately for specific records:** In Salesforce, make a small change to any field on the affected accounts or contacts (for example, add and remove a space in a text field). This updates `SystemModstamp` and Clay will pick up those records — with all their current field values including the newly mapped field — on the next incremental sync.

### Can I see when the weekly full sync is scheduled, or trigger it manually?

No. The Clay UI shows only that the Salesforce full sync runs weekly — it does not display the exact day or time the next full sync is scheduled for your workspace. The timing is assigned automatically per workspace and is not shown in the interface.

There is no self-serve option to trigger a full sync manually. If you need an expedited full sync — for example, to pick up formula field updates that are not captured by incremental syncs — contact Clay support.

**Workaround for specific records:** The incremental sync (every 15 minutes for Enterprise, once daily for Growth) picks up any Salesforce record whose `SystemModstamp` has been updated. To re-sync specific records sooner, make a small edit to those records in Salesforce — for example, add and remove a space in any field. This updates `SystemModstamp` and Clay will pick up those records on the next incremental sync, without waiting for the weekly full sync.

### Why do some of my Salesforce Lead records not appear as separate person records in Clay?

When Salesforce data syncs into Audiences, Leads and Contacts are not always separate Clay person records. Clay applies a built-in record-matching rule using the `ConvertedContactId` field on Lead records.

**How it works:**

- **ConvertedContactId check** — If a Lead has a `ConvertedContactId` value, Clay adds that value as an additional external record ID alias on the Lead (alongside the Lead's own `00Q…` Salesforce ID). Clay then checks whether any Contact in your Audiences shares that same external ID (the `003…` value). If a match is found, the Lead and Contact resolve to the same Clay person — not two separate records.
  - If the Contact already exists in Clay, the Lead's data is merged into that existing person record.
  - If the Lead syncs first (before the Contact exists), a single Clay person is created carrying both the `00Q…` Lead ID and the `003…` Contact ID as aliases. When the Contact syncs later, it lands on that same person via the shared alias.

- **Multiple Leads → same Contact** — If two Lead records both have a `ConvertedContactId` pointing to the same Contact, both Leads collapse into that one Clay person record. Only the Lead with the direct conversion pointer is surfaced in Clay; the other Lead is absorbed because both share the same `003…` external ID alias.

- **A Lead without `ConvertedContactId` does not merge this way** — Without a conversion pointer, no shared alias is created. That Lead appears as its own Clay person record unless a separate matching condition applies (for example, a shared profile URL resolved via entity resolution).

- **Email address is not part of this initial import matching** — Different email addresses on two Lead records that point to the same Contact are irrelevant to the `ConvertedContactId` matching step. The `003…` alias is the sole key — not email, phone, or profile URL.

**To investigate a missing Lead record:** Check whether the Lead has a `ConvertedContactId` value in Salesforce. If it does, look for a Contact in your Audiences whose Salesforce external ID matches that `003…` value — the Lead's data will be present on that Contact person record.

**Note:** This record matching is distinct from Audiences' entity resolution (which matches by profile URL, email, or probabilistic signals). `ConvertedContactId` matching happens at import time, before entity resolution runs.

### Why does "Company LinkedIn URL" appear in my audience filters when I mapped the field as "LinkedIn URL"?

These refer to the same field. In the Salesforce import field mapping, the LinkedIn URL for accounts is labeled **"LinkedIn URL"**. In the audience filter builder, that same field appears as **"Company LinkedIn URL"** — Audiences automatically adds the "Company" prefix to distinguish it from the equivalent person-level field, which appears as **"Person LinkedIn URL"** in People audiences.

The underlying field and data are identical. If you mapped Salesforce's Account LinkedIn URL field and named it "LinkedIn URL" in your import settings, filtering on "Company LinkedIn URL" in your Companies audience targets that same mapped field.

### Why doesn't my Clay table appear in the Person source filter?

The **Person source** filter lists each source by its display name. If you sent records from a Clay table to Audiences using **Continue → Save to People**, look for the table's display name in the Person source dropdown — the same name that appears in the **Source** column on each record.

If your table still doesn't appear in the dropdown, the records may have been pushed via the `Upsert Audiences Record` table action, which doesn't create a named source entry. In that case, type a plain-language description into the filter search box (for example, "Filter people by source id: t_0tfg3qav6HC2a54Cdpx") — a **Create filters with AI** option may appear as you type. Click it and Clay will build the Person source filter automatically. If the option doesn't appear, contact Clay support.

### How do I find which Clay table a lead in Audiences came from?

Each record in Audiences has a **Source** column that shows the display name of the data source the record originated from. For records sent to Audiences from a Clay table (via **Continue → Save to People** or **Save to Companies**), the Source column displays the table's name.

The Source column is plain text — there is no direct link from the Source column to open the originating table. To open the table, use its name to find it in your workspace's tables list.

**Note:** To filter your audience to show only records that came from a specific table, use the **Person source** filter — see [Why doesn't my Clay table appear in the Person source filter?](#why-doesnt-my-clay-table-appear-in-the-person-source-filter) above.

### My CRM is messy. Should I clean it up before setting up Audiences?

You don't need a clean CRM to get started — CRM cleanup is often the first use case Audiences enables. A common approach: sync your existing CRM, run professional network enrichments to refresh contact data, use the enriched identifiers to surface duplicates, then build further enrichments from there.

### Does Audiences update automatically?

Yes. Segments update in real time as records enter or exit your filter criteria. The refresh frequency depends on your plan:

-   **Enterprise plan:** CRM and data warehouse syncs run every 15 minutes, and segments update continuously.
-   **Growth plan:** CRM and data warehouse syncs run daily, and segments update based on that daily refresh.

Enrichments configured with `Continuous Enrichment` enabled automatically process new records entering a segment, typically within 15 minutes. No manual runs are required after initial setup.

### Why didn't my audience count change after I tightened my search filters?

By default, audience searches (Find People and Find Companies sources) use **Add new results** mode — the search only adds net-new contacts going forward and never removes contacts from an earlier, broader search. To narrow your results, use the **Replace existing results** option when saving.

When you edit a search's criteria and click **Save**, a dropdown appears with two options:

-   **Add new results**: keeps the current results and adds contacts that match the updated criteria.
-   **Replace existing results**: discards the current results and rebuilds the segment using only contacts that match the updated criteria (contacts previously imported are excluded to avoid re-importing them).

To work with only the narrower set, open the search, tighten your filters, click **Save**, and select **Replace existing results**.

### Can I sync an audience to multiple ad platforms?

Yes — you can add multiple ad platforms to a single audience sync. After your initial sync is active, an **Expand your reach** section appears on the Sync tab. Click **Add** next to any available platform to configure field mappings for that provider. The new platform will sync on the same schedule as your existing provider.

### How do I export my audience data to CSV?

The Audiences screen does not have a direct CSV download button. To download audience data as a CSV, first send the segment to a Clay table using **Add to workbook**, then export that table:

1. Open the audience segment you want to export.
2. Click **Send** → **Export action** → **Add to workbook**. Clay creates a Clay table containing up to 50,000 rows from that segment.
3. Open the table. If any rows are checked, uncheck them first — the toolbar shows **Tools** only when no rows are selected.
4. Click **Tools** → **Export** → **Download CSV**.

For segments with more than 50,000 records, export in batches by applying filters to create smaller sub-segments and repeating steps 2–4 for each batch.

### What happens to a contact's ad targeting when they become a customer?

If your segment has an exclusion condition (e.g., Account Type ≠ "Customer"), the contact is automatically **removed** from the synced ad audience as soon as that condition is met. See [Clay Ads](https://university.clay.com/docs/clay-ads) for platform-specific guidance.

### Will my Salesforce Account ID appear on web visitor records?

Yes — this is expected behavior. When a web intent visitor's company domain matches the domain of a Salesforce Account you have synced into Audiences, Clay merges the two into a single entity using normalized domain matching. Salesforce Account data — including the Account ID — becomes available on that unified company record automatically.

For this to work, you need both:

-   Salesforce Accounts synced into Audiences with website domain fields mapped.
-   Web intent configured as a signal in your Audiences workspace.

**If visitors arrived before your Salesforce sync was connected:** Web intent records added to Audiences before you connected Salesforce may not automatically merge with existing SFDC records. To resolve this, use the **Import record matching** option in your Salesforce import settings and select domain as the match key (this feature is currently in beta — contact your Growth Strategist to enable it). This matching applies to records coming in after the setting is enabled — it does not retroactively merge records already in Audiences.

### I've mapped fields to Salesforce but the data isn't syncing — why?

The most common cause is that the **Export sync toggle is off**. Even if your field mappings are fully configured and individual fields are set to "Always write," no data flows to Salesforce until Export sync is enabled. This toggle is off by default.

To enable it (admin-only):

1.  Go to **Settings** → **Sources / Destinations** and click your Salesforce connection.
2.  Select the object tab you want to export (for example, **Accounts**).
3.  Under **Export [Object] data**, toggle on **Export sync**.
4.  Click **Save and review** → **Confirm**.

Once enabled, the first export does not run immediately — it fires at your workspace's next scheduled export time, which may be up to 24 hours away. See [Writing back to your CRM](#writing-back-to-your-crm) for the full schedule and behavior details.

If Export sync is enabled but **specific fields** are still not updating in Salesforce — and you see no export errors — check each field's **write rule**. A field set to **Write if empty** only sends its value to Salesforce when the corresponding Salesforce field is blank. If that Salesforce field already contains a value, Clay skips the update silently without recording an error. Your data may look correct in Audiences while those fields remain unchanged in Salesforce.

To allow Clay to overwrite existing Salesforce values for a field:

1.  Go to **Settings** → **Sources / Destinations** and click your Salesforce connection.
2.  Select the object tab (for example, **Accounts**).
3.  Find the field that isn't updating and click the **pencil (edit) icon** next to it.
4.  Change the write rule from **Write if empty** to **Always write**.
5.  Click **Save and review** → **Confirm**.

The updated value will be pushed to Salesforce on the next export cycle (within 24 hours).

### How do I create new Salesforce Accounts or Contacts from an Audience?

New Salesforce records are not created automatically when you run a bulk enrichment. Record creation is not driven by a Create Contact or Create Account action inside the enrichment table — it is controlled by the **`Create new Salesforce records`** toggle in your Audiences Salesforce export settings.

To push net-new Accounts or Contacts to Salesforce:

1.  Open your Audiences workspace and go to your Salesforce source settings.
2.  Under the export section, enable the **`Create new Salesforce records`** toggle. (Admin access required — the toggle is off by default.)
3.  Confirm your field mappings and save.

Once the toggle is on, Clay will create new Accounts or Contacts in Salesforce for any Audience record that doesn't already have a matching SFDC entry. (Leads and Opportunities do not support record creation through this toggle.)

To track which contacts in Salesforce came from a specific Audience enrichment, create a custom Audience text field (for example, an "Audience Source" field set to a label like `"Q2-enrichment"`), and map it to a Salesforce field (a custom field, campaign tag, or lead status) in your export settings. You can then filter on that value directly in Salesforce.

### How do I write enriched fields back to existing Salesforce records from a bulk enrichment?

Add a **Salesforce Update Record** action column directly inside your bulk enrichment table. This pushes enriched values to matching Salesforce records in the same run, without waiting for the Audiences export cycle:

1.  In your bulk enrichment, add your data enrichment columns as usual (for example, `Enrich Person` to find LinkedIn URL, email, or industry).
2.  Click `Add enrichment` and search for **Salesforce** → select **Update Record**.
3.  Set **Record ID** to the Salesforce Contact, Lead, or Account ID already stored in your Audience (the field imported from Salesforce or from your original SOQL import).
4.  Map each enriched field to the corresponding Salesforce field you want to populate.
5.  Click `Start Run` — the Update Record column fires alongside your enrichment columns and writes the enriched values directly to Salesforce.

If you have the Audiences Salesforce export enabled, enriched fields also sync back to Salesforce automatically on the next 24-hour export cycle (see [Writing back to your CRM](#writing-back-to-your-crm)). Adding Update Record directly in the enrichment table is useful when you need immediate write-back or when you are not using the native Audiences Salesforce import.

### How do I write enriched data back to HubSpot from Audiences?

Audiences does not have a native HubSpot export destination — Salesforce is currently the only built-in CRM export. To push enriched data to HubSpot, use a Bulk Enrichment with a HubSpot action column directly from within your audience segment:

1.  Navigate to an audience segment and click **Enrich** → **Add bulk enrich**.
2.  In the bulk enrichment table, add your data enrichment columns as usual (for example, `Enrich Person` to find phone numbers or professional profile URLs).
3.  Click `Add enrichment` and search for **HubSpot** → select **HubSpot: Update Contact** (to update existing HubSpot contacts) or **HubSpot: Create records** (to create new contacts or companies in HubSpot).
4.  Map each enriched field to the corresponding HubSpot property you want to populate.
5.  Click **Start Run** — the HubSpot action column fires alongside your enrichment columns and writes the values directly to HubSpot.

This approach supports batching and works for both contacts and companies. To automatically push data for new records entering the segment going forward, enable the **auto-enrich toggle** on the bulk enrichment.

### My HubSpot has more records than my plan limit — how do I limit what gets imported into Audiences?

The Audiences HubSpot connector imports all records for the selected object type (Contacts, Companies, or Deals) — there is no option to select a specific HubSpot list within the Audiences source setup. If your HubSpot object has more than 250,000 records (the Growth plan limit), the import will pull all records for that object. Filtering in Audiences after the import won't reduce your record count against the plan limit — the records have already been imported.

To import only a filtered subset of HubSpot records into Audiences:

1.  In a **Clay table**, add a source and select **Import objects from HubSpot**.
2.  Under **List to pull objects from**, select the specific HubSpot list containing the contacts or companies you want.
3.  Map and format the fields you need in the table.
4.  Add **Upsert Audiences Record** as an action column — this pushes each row from your scoped, mapped table directly into Audiences without going through the full-object Audiences import.

This gives you control over both which records enter Audiences and how their fields are mapped, independent of the native Audiences HubSpot source connector.

**Note:** There is no add-on available to increase the Audiences record limit above 250,000 while staying on the Growth plan. To increase the limit, upgrade to the Enterprise plan, which supports up to 25,000,000 CRM/DWH records.

### I enriched data in my Audience. Why hasn't it appeared in Salesforce yet?

Clay Audiences syncs in two separate directions on different schedules:

-   **Salesforce → Clay Audiences (import):** Changes made in Salesforce appear in your Audience automatically — every **15 minutes** on Enterprise plans, or once **daily** on Growth plans.
-   **Clay Audiences → Salesforce (export):** Enrichments and field updates you make in Clay Audiences are exported back to Salesforce automatically **once every 24 hours**. No manual "Start run" is needed to trigger this.

The 15-minute (or daily) sync applies to the **import direction only** — it reflects Salesforce changes in your Audience. Enriched data written in Clay flows back to Salesforce on the 24-hour export cycle.

After you enable Export sync, the first export does not run immediately — it fires at your workspace's next scheduled export time, which may be up to 24 hours away. Subsequent exports run on the same 24-hour schedule. See [Writing back to your CRM](#writing-back-to-your-crm) for the full export schedule and behavior.

To push enriched data to Salesforce before the next scheduled export, see [How can I export records to Salesforce immediately without waiting for the 24-hour sync?](#how-can-i-export-records-to-salesforce-immediately-without-waiting-for-the-24-hour-sync)

### How can I export records to Salesforce immediately without waiting for the 24-hour sync?

The 24-hour export schedule is fixed and cannot be triggered manually. Two options let you push records to Salesforce sooner:

-   **Export a single record on demand (admin-only):** Open any record in Audiences and click **Export** in the top right of the record panel. This sends that record to Salesforce immediately, without waiting for the next scheduled sync. The button appears only when the record has a Salesforce export configured.
-   **Export many records immediately:** Add a **Salesforce Update Record** action column to a bulk enrichment table — see [How do I write enriched fields back to existing Salesforce records from a bulk enrichment?](#how-do-i-write-enriched-fields-back-to-existing-salesforce-records-from-a-bulk-enrichment) above.

### How do I access Account-level fields (like Company Name or Company Domain) from a People audience?

When you import Salesforce Contacts into a People audience, only fields from the **Contact object** are available as columns — Account-level fields (Company Name, Company Domain, and any custom Account object fields) are not included automatically, even if the Contact has a linked Salesforce Account.

To pull Account-level data into a Clay table:

1. In your table, open the **Audiences Record** cell for a Contact row and navigate to **Records → Related IDs → Account IDs**. This value is the **Clay Company ID** for the linked account — Clay's internal identifier for the Company record in your Audiences. It is **not** the Salesforce Account ID.
2. Add a `Lookup in Audiences` action column.
3. Set **Object type** to **Companies**.
4. Set the filter field to **Company ID** and map it to the Account IDs value from step 1.

The lookup returns the matching Company record from your Audiences, including all Account-level fields configured when you imported Salesforce Accounts into the Companies audience (for example, Company Name, Company Domain, and custom Account fields).

**Salesforce Leads (vs. Contacts):** The steps above apply specifically to records imported from Salesforce **Contacts**. Salesforce **Lead** records in your People audience do not have an automatic Company association. Clay builds the **Account IDs** link by reading the `AccountId` field during Contact import — Lead records have no equivalent Account relationship in Salesforce (they carry a plain-text `Company` field, not an Account lookup), so **Records → Related IDs → Account IDs** is empty for Lead-sourced person records.

Two approaches that do not apply to the Lead → Company case:

- **Mapping a "Linked Account" custom lookup field from the Lead object:** if your Salesforce Leads have a custom lookup field pointing to an Account record, mapping that field in the Leads import brings it in as a text column containing the Salesforce Account ID. However, it does not create a Company association in Audiences — the **Account IDs** path remains empty.
- **Import record matching:** this feature merges records of the same entity type (person records with person records; company records with company records). It cannot link a Lead record in People to an Account record in Companies.

To filter your People audience by company attributes for Lead records, map company-related fields directly from the Lead object in your Salesforce import field mapping — for example, the Lead's built-in **Company**, **Industry**, or **Annual Revenue** text fields. Mapped Lead fields are available as People audience filter options immediately after the next sync.

### Why does filtering my People audience by deal attributes return fewer contacts than expected?

When you filter a People audience by opportunity or deal attributes (for example, Stage, Amount, or a custom deal field), Clay only includes contacts that are **directly linked to the matching deal via OpportunityContactRole** in Salesforce — not all contacts at the account that owns the deal.

This means the filter answers "find me everyone who is a contact role on these specific deals," not "find me everyone at companies that have these deals." If your Salesforce org doesn't link contacts to opportunities via OpportunityContactRole, or only a subset of contacts are linked, the resulting People audience will be smaller than you might expect.

**To pull all contacts at accounts with matching deals:**

1.  Build a **Companies** audience filtered by your deal criteria (for example, Stage, Amount, or deal name).
2.  Connect a workflow to that Companies audience (**Send** → **Send to workflow**) that writes a flag value to a custom Salesforce field on each matching account — for example, a **Salesforce Update Record** action that sets a text field to `"target-campaign-q2"`. Publish the workflow, then use the **Run** dropdown in the workflow editor to run it on all current segment members.
3.  In your **People** audience, add a filter on **Account → [your flag field] equals your flag value**.

This pulls every contact tied to those accounts, regardless of their OpportunityContactRole status.

### Why does my HubSpot deal Stage filter return no results in a Companies audience?

When you filter a Companies audience by **Stage** under the Deals filter group, the value you enter must match HubSpot's **internal stage ID** — not the human-readable display name shown in the HubSpot UI. Clay stores the raw `dealstage` property value as it comes from HubSpot, so entering "Closed Won" returns no results even though that is the stage's display name in HubSpot.

**HubSpot's default pipeline stages** use internal IDs that resemble their display names (for example, `closedlost` for Closed Lost and `closedwon` for Closed Won in the default pipeline). Stages in custom pipelines, or any stage that has been renamed, use a numeric internal ID assigned by HubSpot — which is why trying common text patterns like "closed" or "won" may not match.

**To find the internal stage ID for any deal stage:**

1.  In HubSpot, go to **Settings → Objects → Deals → Pipelines**.
2.  Select the pipeline that contains the stage you want to filter by.
3.  Hover over the stage name — HubSpot displays the internal stage ID.
4.  Copy that value and paste it into the Clay **Stage** filter (for example, use the `contains` operator and enter the internal ID).

**Note:** This limitation applies only to the deal Stage filter in Audiences. In Clay table enrichment columns, deal lookup and retrieval actions return both the internal stage ID and the readable display label as separate fields — so you can see the label there and use it to look up the matching internal ID.

### Why does Clay MCP show activity data for a contact when the Audiences Activity tab shows no activity?

When a Salesforce lead is converted to a contact, Audiences merges both records into a single People entry using the lead's `ConvertedContactId`. The underlying activity data from the lead record — including activity counts and last-activity dates — is stored in Audiences and is accessible via Clay MCP, including the `ask-question-about-accounts` tool, which queries your Audiences data at the backend level.

However, the current Audiences UI contact view does not yet display a full union of all data from the converted lead. This means activity counts and last-activity dates that originated from the lead record may not appear in the contact's Activity tab even though the data exists in Audiences and is retrievable via MCP.

**Note:** This discrepancy is a known limitation in the current Audiences UI. When you see activity data returned by Clay MCP for a contact whose Activity tab appears empty, that data is sourced from the corresponding converted lead record. A future update will show the full union of contact and converted lead data in the UI.

### How does filtering work in Lookup in Audiences when I select multiple fields?

When you select multiple fields in **Fields to filter by**, the lookup uses **AND logic** — a record must match on **all** selected fields to be returned. There is no option to switch to OR logic.

Two behaviors to keep in mind:

-   **All fields must have an exact match.** If you filter by both `Email` and a secondary identifier field (such as a profile URL), a record is only returned when both values match exactly. A record with the right email but a different or missing secondary value won't be returned.
-   **Blank or empty filter values prevent any match.** If any field in **Fields to filter by** has a blank or null value in your table row, the lookup returns "No records found" — even if the Audiences record also has a blank value for that field. Every filter field must have a non-empty value for the lookup to run.

**Tip:** Use a single strong identifier like `Email` when you want reliable matches. Email is unique per person and avoids the no-match issue that occurs when secondary identifier fields are inconsistently populated.

### Why isn't a signal showing up in my Lookup in Audiences result?

Three things to check:

-   **The signal falls outside the default lookback window.** `Lookup in Audiences` returns signal data for the past **90 days** by default via the **Signal data to include (days)** column setting. This lookback is independent of your audience's filter criteria — a contact can be correctly included in a "job change results" audience yet still show empty signal data in a lookup if the job-change event falls outside the configured window. To retrieve older signals, open the column settings and increase **Signal data to include (days)** to cover the relevant time range.
-   **The default 5-result count was reached.** `Lookup in Audiences` returns 5 signal results per record by default. If a company has more active signals than that, some may not appear — increase the result limit in the column settings (up to 50), or use `Get Audiences Activity` to retrieve a larger set of signal data.
-   **The signal hasn't fired for that record yet.** Signal results are written asynchronously and may not appear immediately after a signal run completes. If a signal should be recent but is still missing, open the signal's column header → `Edit column` and re-run the signal to refresh the data for that record.

### Can I remove a source from the 'Add data' list in Audiences?

No. Sources listed under **Add data** — including CSV imports and Clay table (local) sources — cannot be removed from the source list in Audiences. The source listing is retained for filtering and audit purposes.

- **CSV imports:** No removal option is shown in the source list after import.
- **Clay table (local) sources:** The source entry shows only a **View table** option — there is no disconnect or remove action.

To remove the **records** that a source contributed to your Audience, archive them through a segment — see [How do I remove records from an audience?](#how-do-i-remove-records-from-an-audience) below. For CSV sources specifically, see also [How do I replace a CSV import with updated data?](#how-do-i-replace-a-csv-import-with-updated-data).

### How do I remove records from an audience?

The People and Companies views in Audiences do not have per-row checkboxes or a Delete button for individual records. To remove people or companies from your audience, you archive them through a segment filter. **Admin access is required** — the option is not visible to Members or Viewers.

1.  Navigate to **People** or **Companies** in the left sidebar.
2.  Open or create a segment that isolates only the records you want to remove:
    -   **From All People or All Companies:** click **Criteria**, apply a filter (for example, **Origin source** to target a specific import, or **Name → is not empty** to target all records), then click **+ Create Audience** in the toolbar to save the filtered set as a new named segment.
    -   **From an existing audience:** open the segment, apply or update its filters, and click **Save filters** to make sure the segment reflects exactly the records you want to remove.
3.  Once the segment shows the correct records, click the **⋮** (three-dot) menu next to the segment name.
4.  Select **Archive records**.

Archived records are removed from all audience segments and excluded from future enrichments and workflows. The records are not permanently deleted — they can be viewed and restored at any time from the **Archived** section in the left sidebar. See [What happens when I archive a record in Audiences?](#what-happens-when-i-archive-a-record-in-audiences) for full details.

### What happens when I archive a record in Audiences?

Archiving a record is a **soft delete** — the record is not permanently removed from your Audiences workspace. When you archive a record:

-   It is **excluded from all audience segments and workflows** — it will not appear in segment filter results or trigger enrichment automations.
-   It can be viewed in the **Archived** section in the left sidebar.
-   It can be **restored at any time** from the Archived section.

**Important:** Re-importing a record with the same identifiers (email, domain, or external IDs) **will not revive an archived record** — the incoming import is silently skipped and the record stays archived. To bring an archived record back, restore it manually: navigate to **People** or **Companies** in the left sidebar → click **Archived** → find the record → click **Restore**. You can then re-import or re-sync data for that record if needed.

**There is no self-serve option to permanently delete records from Audiences.** Archiving is the only available removal method. If your use case requires permanent removal, contact Clay support.

**Note on lookup timing:** After archiving a record, there is a brief processing delay before the change is reflected in `Lookup in Audiences` results. Running a lookup immediately after archiving may still return the archived record — lookups typically update within a short time as changes propagate.

To exclude Salesforce-deleted records from your audience lookups, filter on **Sync status → Deleted in source** to identify them, then archive the records you no longer want matched against.

### How do I replace a CSV import with updated data?

If you imported a CSV and need to correct the data — for example, because account records changed — archive the old records first, then import the updated file. **Admin access is required** — the Archive records option is not visible to Members or Viewers.

1.  Navigate to **People** or **Companies** in the left sidebar.
2.  Click **New audience** and add a filter: **Origin source** → **=** → select the name of your original CSV file. This targets only records that came from that specific import.
3.  Once the segment shows the correct records, click the **⋮** (three-dot) menu next to the segment name and select **Archive records**.
4.  Import the updated CSV using **Add data** → **Add Source** → **CSV**.

Audiences deduplicates on import using the unique identifier you configure — any incoming record whose identifier matches an existing (non-archived) record will update that record rather than create a duplicate.

**Note:** After archiving, the original CSV source entry remains visible in the Sources tab. There is no self-serve option to remove a CSV source listing — the entry is retained for filtering and audit purposes. To permanently remove the source entry, contact Clay support.

### How do I archive records that no longer match my Snowflake import query?

When you update your Snowflake Import Sync with a more restrictive SQL query (returning fewer records than before), records from the previous import that no longer match the new query are not automatically removed from Audiences. After the next full sync, Clay marks those records as **Deleted in source** for that Snowflake sync — but the audience records remain active and continue to appear in segment filters and enrichments until you manually archive them.

To identify and archive these orphaned records:

1.  Navigate to **People** or **Companies** and click **New audience** to create a segment.
2.  Use one of these filters to isolate the orphaned records:
    -   **Sync status → Deleted in source** — surfaces records whose Snowflake source association was cleared by the most recent full sync.
    -   **Sources → doesn't contain → [your Snowflake sync name]** — surfaces records not currently associated with the active sync.
    -   **[Your custom field] → is empty** — if your updated import adds a new column (for example, an `inferred_updated_at` timestamp used for incremental loading), records where that field is empty were not touched by the new import and are the orphaned ones.
3.  Once the segment shows the correct records, click **⋮** next to the segment name and select **Archive records**.

**Admin access is required** — the Archive records option is not visible to Editors or Viewers.

### Why did Update Audiences Record report 0 fields updated?

This "0 fields updated" result comes from the `Update Audiences Record` action that pushes data into your Audience from a Clay table. The most common cause is that all mapped fields had null values in the source row. This action filters out any field whose value is `null`, `undefined`, or empty before writing to the Audience — when every mapped field is empty, there is nothing to write, so the action completes successfully but reports 0 fields updated. This null-filtering is built into the action and is not user-configurable.

**To confirm this is the cause:** Check whether the columns you mapped into `Update Audiences Record` are populated for the rows that show 0 fields updated.

**To fix it, use an explicit placeholder value instead of null.** Rework your formula so it always returns a meaningful non-null value. For example, if you use a timestamp to mark when a contact becomes eligible, have the formula return the eligible date when it applies and a text value like `"Not Eligible"` when it doesn't. Both are real values, so `Update Audiences Record` writes an update on every run — and you can route off the result (process the row when the field contains a date; skip when it says `"Not Eligible"`).

**Note:** The **Ignore blank values** toggle does exist, but on the `Upsert Audiences Record` action (and on the variant of `Update Audiences Record` that is configured via the Upsert config panel). It is on by default; when disabled, null values are passed through and will clear existing values on the target Audience field. These actions report `✅ Success` (or `✅ Upserting...` / `✅ Updating...`) rather than `0 fields updated`, so the toggle is not what controls the "0 fields updated" message described above.

### How does Clay handle Salesforce Lead-to-Contact conversions?

When a Salesforce Lead is converted into a Contact in Salesforce, Clay automatically merges the Lead record with the Contact record in Audiences. The data from both records is combined into a single person record, and all historical data is preserved. This merging happens automatically and is not user-configurable.

### What's the difference between automatic Lead/Contact merging and deterministic matching?

There are two types of record matching in Clay Audiences:

-   **Automatic Lead/Contact merging** — When Salesforce converts a Lead to a Contact, Clay automatically merges these records. This is Salesforce-specific and not user-configurable.
-   **Deterministic matching** — User-configurable matching across different data sources. You choose which field to match on (email, domain, profile URL, etc.) when importing a new source. This allows you to merge the same person or company from multiple data sources into a single Audiences record.
