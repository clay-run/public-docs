---
title: Audiences
description: "Clay Audiences is available on Growth and Enterprise plans. Launch and Trial workspaces can import via CSV, people/company search, and Clay table sends; connecting a CRM or data warehouse requires Growth or above."
last_synced: 2026-04-27T18:09:16.275Z
---

# Audiences

**Plan availability:** Clay Audiences is available on **Growth** and **Enterprise** plans (including legacy Enterprise). Launch and Trial workspaces have access to core Audiences features — importing via CSV, people/company search, and Clay table sends — but connecting a CRM or data warehouse as a data source requires **Growth or above**. Free workspaces and legacy non-Enterprise plans do not have access to Audiences. Growth plans can sync up to 250,000 CRM/DWH records; Enterprise plans support up to 25,000,000 records.

Clay Audiences is the unified data layer for your workspace.  It combines your CRM, data warehouse, and third-party enrichments into one persistent profile per contact and account, updated in real time.

Use it to build dynamic segments across millions of records, run automated enrichment and signal workflows at scale, and sync results back to Salesforce without managing dozens of separate tables.

Setting up Audiences is four major steps:

1.  **Import your data** — connect Salesforce, HubSpot, Snowflake, or Google BigQuery and bring your records into Audiences.
2.  **Create audiences** — build dynamic segments using filters to target the right contacts and accounts.
3.  **Enrich and monitor** — run bulk enrichments and signals that write data permanently back to each record.
4.  **Write back to your CRM** — sync enriched data and segment membership back to Salesforce.

## Importing your data

To view your full audience, click `People` or `Companies` in the left sidebar.

To add a data source for the first time, click the `Add data` button in the top right, then click `Add Source`.

**Note:** Adding a data source requires Admin access. The `Add data` button and most source options are visible to all workspace members, but only Admins can complete source setup — Editors receive an error when attempting to connect a source. If you're an Editor, ask a workspace Admin to connect the source, or have your role changed.

You can import data from:

-   A new people or companies search
-   Snowflake
-   Google BigQuery
-   Salesforce
-   HubSpot

### Importing from Salesforce

**Note:** Setup must be completed separately for People, Accounts, Leads, and Opportunities. Complete steps for `People` first, then repeat for `Accounts`, then `Leads`, then `Opportunities`.

1.  Click `Add data` → `Add Source` → select your [**Salesforce integration**](https://university.clay.com/docs/salesforce-integration-overview).
    -   If you don't see an SFDC integration listed, contact your Growth Strategist.
2.  Select `People` at the top of the sync panel.
3.  Enable the `Import` toggle.
4.  Leave `Export Sync` and `Create new Salesforce records` off for now.
5.  Add any SFDC fields you frequently use or want to segment by — only fields included here will appear as columns and filter options in your Audience.
    -   You can add more fields later. See [A Salesforce field isn't appearing in my audience filters](#a-salesforce-field-isnt-appearing-in-my-audience-filters--how-do-i-add-it) in the FAQs below.
6.  Name the corresponding Clay fields — these become the column names in Audiences.
7.  Select `Accounts` at the top and repeat steps 3–6 for accounts.
8.  Select `Leads` at the top of the sync panel.
9.  Enable the `Import` toggle.
10.  Add any Lead fields you want to filter or segment by — common fields include `Lead Status`, `Lead Source`, `Title`, and `Company`.
     -   Lead records are automatically merged with matching Contact records into a single person record in your People audience. Data from both sources is combined, and duplicates across Salesforce Leads, Contacts, and other sources count as one person. The primary matching key is the `ConvertedContactId` field — see [Why do some of my Salesforce Lead records not appear as separate person records in Clay?](#why-do-some-of-my-salesforce-lead-records-not-appear-as-separate-person-records-in-clay) for details.
     -   After syncing, you can filter your People audience by **sync status** (whether a Lead record has been imported from Salesforce) and **record conversion status** (whether the Lead has been converted to a Contact in Salesforce).
11.  Name the corresponding Clay fields.
12.  Select `Opportunities` at the top of the sync panel.
13.  Enable the `Import` toggle.
14.  Add any Opportunity fields you want to filter or segment by — common fields include `Stage`, `Amount`, `Close Date`, and `Owner`.
     -   Opportunity data is associated with your Companies records and becomes available as a filter in any Companies audience.
15.  Name the corresponding Clay fields.
16.  Click `Save and Preview`, then `Confirm`.

**Sync timing and behavior**

Clay pulls data from Salesforce on two schedules:

-   **Incremental sync (every 15 minutes):** Retrieves records whose `SystemModstamp` has changed since the last sync. Any modification to a Salesforce record — user edits, workflow updates, or integration changes — updates `SystemModstamp` and triggers the record to be re-synced. There is no field-level filtering; when a record is picked up, all its mapped fields are synced.
-   **Full sync (every 7 days):** Re-reads all records from Salesforce. Catches anything the incremental sync may miss and reconciles hard-deleted records.

**Formula and calculated fields:** Salesforce formula and calculated fields do not update `SystemModstamp` when they recalculate. Changes to these fields are not captured during incremental syncs — they appear in Audiences only after the next weekly full sync.

**Deleted records:** Clay does not remove deleted Salesforce records from Audiences immediately. Instead, the record is marked **Deleted in source**, which you can filter on in your audience. The weekly full sync reconciles hard-deleted records. If a Salesforce record is deleted and recreated (assigning it a new Salesforce ID), it will temporarily appear as a duplicate entry until the next weekly full sync resolves it. There is no self-serve option to trigger an early full sync — contact Clay support if you need an expedited cleanup.

**Salesforce activities (beta):** Importing Salesforce Tasks and Events into Audiences is currently in beta — the toggle is gated by an internal feature flag and may not yet be enabled for your workspace. Contact Clay support to request access. Once enabled, go to your Salesforce source settings, select `Accounts`, and enable the **Also import activities (tasks and events) associated with these accounts** toggle. Accounts are associated automatically in the background. The Activity tab on each record's detail view then shows Salesforce Tasks and Events alongside other connected activity sources (for example, Gong calls or email sequence activity). Each entry displays the activity type (Task or Event), title, and timestamp.

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

### Sending data from Clay table

You can also send contacts from any existing Clay table directly to your Audience:

1.  Open any table with contacts you want to save to your Audience.
2.  Click `Continue` at the bottom of the table.
3.  Select `Save to People` or `Save to Companies` depending on the record type.

Records saved from tables are automatically deduplicated and merged with your existing audience data.

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

To configure:

1. In your import settings, click **Import record matching**.
2. Choose an **alias field** — typically `Domain` for Companies or `Email` for People (additional options include LinkedIn URL, phone number, and others).
3. Map the alias field to the corresponding field in each source.
4. When a new record arrives, Audiences checks whether the alias value already exists. If it does, the new data is merged with the existing record instead of creating a duplicate.

You can configure one alias field per entity type (one for People, one for Companies). This setting applies to records imported *after* it is enabled — it does not retroactively merge records already in Audiences.

**Other deduplication behaviors**

-   **Cross-source deduplication** — merge the same person from multiple sources.
-   **Whitespace detection** — when importing from a Find People or Find Companies search, or saving results from a Clay table to your Audience, records that already exist in All People or All Companies are automatically excluded from the merge. The draft shows a banner with the count of excluded records, and clicking **All people** or **All companies** will only add net-new records. For Companies, exclusion matches on Clay's internal company identifier (CPJ ID). Existing Audience records need entity resolution to have completed — records missing a recognized domain or professional network URL may not yet have been assigned a CPJ ID, which can cause them to slip through as apparent duplicates. Ensuring your Companies audience records have accurate domains and professional network URLs helps entity resolution complete and improves deduplication coverage.

Deduplication across sources is automatic. Within Salesforce, it uses SFDC IDs — org duplicates carry over as-is.

## Creating an audience

After importing, you will want to create new audiences, so you can appropriately target the right contacts.

To create a new audience:

1.  Click `People` or `Companies` in the left sidebar.
2.  Click **New audience** in the top-right corner of the list, or click the `+` next to `My Audiences` in the sidebar.
3.  Select `Criteria` and then add a `Filter` or `Filter group`.
    -   **Filters** evaluate a single condition at a time. All top-level filters are joined with AND — a record must match every one.
    -   **Filter groups** combine multiple conditions using their own AND/OR logic. To build an expression like `A AND B AND (C OR D)`: add A and B as top-level filters, click **`+ Filter group`**, then add C and D inside the group. Once the group contains two or more conditions, a small **`and`** button appears between them — click it to switch to **`or`**.

### Filter operators by field type

The operators available when building a filter depend on the field's data type, shown by the icon next to the field name:

-   **Text fields (T icon)** — support text-matching operators. To match multiple values at once, use **`contains any of`** or **`does not contain any of`** and enter each value — up to 10 values per filter. For example, to include records where Industry is Health, Beauty, or Pets, set the filter to `Industry → contains any of → Health, Beauty, Pets`. This is more efficient than creating a separate filter for each value.
-   **Number fields (# icon)** — support range operators: **`is greater than`**, **`is less than`**, **`is greater than or equal to`**, and **`is less than or equal to`**. For example, `Employees → is greater than → 500`.
-   **Date fields** — support time-based operators: **`within the last`**, **`not within the last`**, **`before`**, and **`after`**. For "within the last" and "not within the last," specify a number of days, weeks, or months as the lookback window. For example, `Created at → within the last → 30 days` targets records created in the past 30 days.
-   **Boolean (true/false) fields** — support **`is true`** and **`is false`** operators. To apply OR logic across two boolean conditions (for example, `field A is true OR field B is true`), add both filters inside a filter group and click the **`and`** connector between them to switch it to **`or`**.

**Note:** A field that appears numeric may have been imported as text (shown by a T icon rather than #). Text fields — such as "Annual revenue range" synced from Salesforce as a string — will not show range operators. To use range filtering on a field, contact Clay support to have the field's type changed to Number (#). Range operators will then appear when you add a filter on that field.

## Enriching and monitoring

### Adding enrichments

Bulk enrichments add contact data, firmographics, technographics, and more to your audience records at scale. They run on an audience and write results permanently back to All People — not just the segment you ran them from. This means any enriched field is immediately available as a filter in any other segment.

**To add an enrichment:**

1.  Navigate to an audience and click `Enrich` → `Add bulk enrich`.
2.  Add enrichment columns as you normally would (e.g., `Enrich Person` for LinkedIn URL, title, phone).
3.  Test on a small batch first — click `Run on 10 rows` to verify output before running at scale.
4.  Open `Field Mapping` and map each column you want to save back to Audiences:
    -   Enable the auto-enrich toggle so that any new record entering this segment is automatically passed through the enrichment — typically within 15 minutes.
5.  Click `Start Run`.

**Note:** Clay does not impose rate limits on Audiences bulk enrichments — the system is built to handle large lists at scale. Third-party data providers (such as Clearbit or Apollo) apply their own rate limits, but Clay queues requests and manages these automatically in the background. If you supply personal API keys for a provider, those keys' own rate limits apply.

**Using Audiences from a Clay table:**

Four Clay actions let you move data between a Clay table and your Audience directly.

-   In any Clay table, click `Add enrichment` and search for:
    -   `Upsert Audiences Record` pushes records from a table into your Audience — creating a new record if no match exists, or updating an existing one if a match is found. Use it to commit data from integrations not yet natively supported in Audiences, qualify event lists in a table before adding them to your Audience, or migrate enrichment work already done in a table.
    -   `Update Audiences Record` writes data from a table row to one or more fields on an existing Audience record. Unlike `Upsert Audiences Record`, it does not create a new record if no match is found. Both actions write only to fields that already exist in your Audience — to create a new custom field first, see [How do I create a custom Audience field that isn't tied to Salesforce?](#how-do-i-create-a-custom-audience-field-that-isnt-tied-to-salesforce) below.
    -   `Lookup in Audiences` pulls data from your Audience into a table row. Use it to reference enriched or signal data in a table workflow without making Salesforce API calls. By default, signal data is returned for the past **90 days** and the action returns **5 signal results** per record by default — adjust the **Signal data to include (days)** setting in the column settings to retrieve older signals, or increase the result limit (up to 50) when you need more results per record. Use `Get Audiences Activity` when you need a larger set of results.
    -   `Get Audiences Activity` retrieves signal and activity data for an Audiences record — including signal events and, if Gong is connected to your workspace, Gong call records. Use it when you need more results or want to query a longer time window than `Lookup in Audiences` provides by default.

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

**To add a signal to a segment:**

1.  Navigate to an audience and click `Enrich`.
2.  Click `Signals` → select a signal type (e.g., `Job Change`).
3.  Set the `look-back period` for the initial run: `3 months`, `6 months`, or `1 year`.
4.  Set the `recurrence frequency` — how often it re-runs going forward.
5.  Review the `cost preview per record` shown before the run begins.
6.  Click `Save and Run`.

After you add a signal:

-   Results write to a `dedicated signal column` on each matching record — stored permanently and globally (not scoped to this segment).
-   Clay **automatically creates a companion segment** combining your original filters plus a filter for the new signal result — this is expected, not an error.
-   Multiple signals each get their own column; the `Signal Summary` column aggregates all results. Click any row to see per-signal detail.
-   Any other segment that filters on this signal type will also surface these results.

### Connecting a workflow to a segment

Connect a Clay workflow to an audience segment to automatically run it on every new member that enters. When a contact or company matches the segment's filters, the connected workflow starts within minutes.

**To connect a workflow:**

1.  Navigate to an audience segment and click `Send` → **Send to workflow**.
2.  In the modal, choose **New workflow** (to create one) or **Existing workflow** (to select from your workspace).
3.  The workflow appears as a card in the **Workflows** section of the sidebar with a **Draft** status.

**Publishing the workflow trigger**

Once connected, click **Publish** to activate the trigger. Publish is a dropdown with three options:

-   **Publish and run [member count]** — publishes the trigger and immediately runs the workflow on all current segment members. New members added later run automatically.
-   **Publish and run 10 [members]** — publishes the trigger and runs the workflow on a sample of 10 members to test behavior before committing to a full run. (Shown only when the segment has more than 10 members.)
-   **Publish and don't run** — publishes the trigger so future members run automatically, but does not run on any existing members.

**Running a published workflow on existing members**

After a workflow is live, open the options menu (⋮) on the workflow card to manually run or re-run it on existing members:

-   **Run all members that haven't run** — runs the workflow on segment members who joined before the trigger was published or who were otherwise skipped.
-   **Force run all members** — re-runs the workflow on every current segment member, including those that already ran. A confirmation prompt appears before this action runs, since it may use credits.

### **Syncing audiences to ad platforms**

When you have a segment ready, you can sync it to an ad platform to run account-based advertising across your highest-fit contacts and companies.

1.  Click `Send` → `Export action`.
2.  Click `Sync to ad platforms`.

**How you might use this:**

-   **Account-based advertising** — sync company segments to LinkedIn, Meta, or Google Ads. Contacts who no longer qualify are automatically removed.

**Syncing to multiple ad platforms**

You can add multiple ad platforms to a single audience sync. After your initial sync is active, an **Expand your reach** section appears on the Sync tab showing available platforms you haven't yet connected. Click **Add** next to any platform to configure field mappings for that provider — it will sync on the same schedule as your existing provider.

**Notes:**
-   You cannot add a platform while a sync is currently in progress — wait for the active sync to complete first.
-   Google Ads is only available for audiences sourced from first-party data (your own CRM or data warehouse). If your audience uses Clay's company/people search (CPJ) data, Google Ads will not be available to add.

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

Audiences supports **bidirectional sync** with Salesforce. Enriched data and segment changes write back automatically.

Map any Clay data or segment membership to Salesforce fields. Examples:

-   Personal email → SFDC `Personal Email` field.
-   Segment membership → CRM status, campaign enrollment, lead score, or owner assignment.

Export settings control whether Clay **creates new Salesforce records** for net-new contacts or **only updates existing ones**.

The **`Create new Salesforce records`** toggle is in your Salesforce source settings under the export section. It is **off by default** — when off, Clay only updates Salesforce records that already have a matching entry in your Audience. Turn it on to allow Clay to create new Contacts or Leads in Salesforce for Audience records that don't yet exist in SFDC. This toggle is admin-only.

Export sync behavior:

-   **Export frequency:** Once every 24 hours. Clay assigns each workspace a stable export time automatically — the schedule is not user-configurable.
-   **First export:** After you enable Export Sync, the first export fires at your workspace's next scheduled export time — this may take up to 24 hours. The Exports panel shows **Not set up** until the first export completes successfully.
-   **Export batch size:** ~10,000 records per sync.
-   **Subsequent syncs:** Incremental — only changed records are processed.

To estimate API calls for initial export, divide record count by 10,000 and compare against your Salesforce limit.

**Note:** CRM export is admin-only. Enrichments and signals follow standard Clay table pricing.

## FAQs

### When should I use Audiences vs. a table?

Use Audiences by default for anything you want to reuse, segment on, or build automations on top of. Use tables for one-off workflows, integrations Audiences doesn't yet support natively, or cases where data doesn't need to persist beyond a single run.

### What if my integration isn't supported yet?

Use the `Upsert Audiences Record` table enrichment as a bridge. Bring your data into a Clay table from any source, then use `Upsert Audiences Record` to push those records permanently into your audience. This works for any source Audiences doesn't yet natively support.

### How do I create a custom Audience field that isn't tied to Salesforce?

The `+ Add field` option is available in the `Update Audiences Record` column mapping inside a bulk enrichment table:

1.  Navigate to a segment and click `Enrich` → `Add bulk enrich`.
2.  In the bulk enrich table, click the `Update Audiences Record` column header to open the Configure panel.
3.  In the `Column mapping` dropdown, click `+ Add field`, name the new field, and save.

Once created, the field is immediately available as a filter in any segment and as a target for `Update Audiences Record` or `Upsert Audiences Record` from any Clay table.

**Note:** There is no option to add new fields directly from the Audience screen — you must go through the `Update Audiences Record` column mapping in a bulk enrichment table.

### A Salesforce field isn't appearing in my audience filters — how do I add it?

Only fields explicitly included in the Salesforce import field mapping are brought into Audiences as columns and made available as filter options. If a Salesforce field — including custom fields like `Account_Record_ID__c` — doesn't appear in the filter dropdown, it was not included when the import was configured.

To add a missing field:

1.  Click **Add data** in the top toolbar.
2.  Find your Salesforce integration and click the **⋮** (three-dot) menu next to it.
3.  Select **Settings**.
4.  In the field mapping section, add the Salesforce field you want and name the corresponding Clay column.
5.  Click **Save and review** → **Confirm**.

The filter option for the field becomes available after the next incremental sync (typically within 15 minutes). However, if you added this field to the mapping after your initial import, records that haven't been modified in Salesforce since the mapping was saved won't have data for the new field yet — see [I added a new Salesforce field to my mapping but some records are missing data for it](#i-added-a-new-salesforce-field-to-my-mapping-but-some-records-are-missing-data-for-it) below. Read-only Salesforce fields — fields shown with a lock icon in the mapping because Salesforce does not allow Clay to write them — can still be imported and used as filters. They will show a **Never write (Read-only)** export rule.

**If a field doesn't appear in the Settings mapping dropdown** (not just in the filter options), the Salesforce account connected to Clay may lack the permissions required to read it. Verify that your Salesforce connection has the required OAuth permissions — see [Salesforce integration FAQs](https://university.clay.com/docs/salesforce-integration-faqs) for the permissions listed under "What permissions and scope do I need for the Salesforce enrichment?" After permissions are updated, return to **Settings** to add the field.

### I added a new Salesforce field to my mapping but some records are missing data for it

When you add a field to your Salesforce import mapping after the initial import, the filter option for that field becomes available after the next incremental sync (typically within 15 minutes). However, existing records are **not** automatically backfilled — only records whose `SystemModstamp` has changed in Salesforce after the mapping was saved will be re-synced with the new field data.

If an existing record had a value for the field in Salesforce before you added the mapping, and that record hasn't been modified since, the value won't appear in your audience until either:

-   **The record is modified in Salesforce** — any change that updates `SystemModstamp` (a user edit, a workflow update, or an integration write-back) triggers the record to be re-synced on the next incremental sync (within 15 minutes). Making a small edit to the record in Salesforce is sufficient.
-   **The weekly full sync runs** — every 7 days, Clay re-reads all Salesforce records regardless of `SystemModstamp`. Missing field values are filled in automatically at that point.

**To fill in missing data immediately for specific records:** In Salesforce, make a small change to any field on the affected accounts or contacts (for example, add and remove a space in a text field). This updates `SystemModstamp` and Clay will pick up those records — with all their current field values including the newly mapped field — on the next incremental sync.

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

The **Person source** filter lists each source by its display name, not by the raw source ID shown in the **Source** column. If you sent records from a Clay table to Audiences using **Continue → Save to People**, look for the table's display name in the Person source dropdown — the raw ID string visible in the Source column (such as `t_0tfg3qav6HC2a54Cdpx`) won't appear there.

If your table still doesn't appear in the dropdown, the records may have been pushed via the `Upsert Audiences Record` table action, which doesn't create a named source entry. In that case, type a plain-language description into the filter search box (for example, "Filter people by source id: t_0tfg3qav6HC2a54Cdpx") — a **Create filters with AI** option may appear as you type. Click it and Clay will build the Person source filter automatically. If the option doesn't appear, contact Clay support.

### My CRM is messy. Should I clean it up before setting up Audiences?

You don't need a clean CRM to get started — CRM cleanup is often the first use case Audiences enables. A common approach: sync your existing CRM, run LinkedIn enrichments to refresh contact data, use the enriched identifiers to surface duplicates, then build further enrichments from there.

### Does Audiences update automatically?

Yes. Segments update in real time as records enter or change, typically within 15 minutes. Enrichments and actions trigger automatically for new records when the autoenrich toggle is enabled. No manual runs required after initial setup.

### Why didn't my audience count change after I tightened my search filters?

Audience searches (Find People and Find Companies sources) are **additive** — the search only adds net-new contacts going forward and never removes contacts already in your audience. If your original search pulled in a large set of contacts, tightening the filters afterward won't reduce that count. Contacts added by the earlier, broader search remain.

To work with a strictly smaller set:

1.  Create a new search with the narrower filters — click `Add data` → `Find people` or `Find companies` and set your tighter criteria.
2.  You don't need to rebuild your enrichment setup from scratch. In your existing enrichment table's **Run setup** panel, update the source to point at the new segment. If the enrichment has already started running, pause and reset it first to return to setup state before editing the source.

### Can I sync an audience to multiple ad platforms?

Yes — you can add multiple ad platforms to a single audience sync. After your initial sync is active, an **Expand your reach** section appears on the Sync tab. Click **Add** next to any available platform to configure field mappings for that provider. The new platform will sync on the same schedule as your existing provider.

### How do I export my audience data to CSV?

The Audiences screen does not have a direct CSV download button, and there is currently no built-in path to download audience data as a CSV file directly from the Audiences screen.

### What happens to a contact's ad targeting when they become a customer?

If your segment has an exclusion condition (e.g., Account Type ≠ "Customer"), the contact is automatically **removed** from the synced ad audience as soon as that condition is met. See [Clay Ads](https://university.clay.com/docs/clay-ads) for platform-specific guidance.

### Will my Salesforce Account ID appear on web visitor records?

Yes — this is expected behavior. When a web intent visitor's company domain matches the domain of a Salesforce Account you have synced into Audiences, Clay merges the two into a single entity using normalized domain matching. Salesforce Account data — including the Account ID — becomes available on that unified company record automatically.

For this to work, you need both:

-   Salesforce Accounts synced into Audiences with website domain fields mapped.
-   Web intent configured as a signal in your Audiences workspace.

**If visitors arrived before your Salesforce sync was connected:** Web intent records added to Audiences before you connected Salesforce may not automatically merge with existing SFDC records. To resolve this, use the **Import record matching** option in your Salesforce import settings and select domain as the match key (this feature is currently in beta — contact your Growth Strategist to enable it). This matching applies to records coming in after the setting is enabled — it does not retroactively merge records already in Audiences.

### How do I create new Salesforce contacts or leads from an Audience enrichment?

New Salesforce records are not created automatically when you run a bulk enrichment. Record creation is not driven by a Create Contact or Create Lead action inside the enrichment table — it is controlled by the **`Create new Salesforce records`** toggle in your Audiences Salesforce export settings.

To push net-new contacts to Salesforce:

1.  Open your Audiences workspace and go to your Salesforce source settings.
2.  Under the export section, enable the **`Create new Salesforce records`** toggle. (Admin access required — the toggle is off by default.)
3.  Confirm your field mappings and save.

Once the toggle is on, Clay will create new Contacts or Leads in Salesforce for any Audience record that doesn't already have a matching SFDC record.

To track which contacts in Salesforce came from a specific Audience enrichment, create a custom Audience text field (for example, an "Audience Source" field set to a label like `"Q2-enrichment"`), and map it to a Salesforce field (a custom field, campaign tag, or lead status) in your export settings. You can then filter on that value directly in Salesforce.

### How do I write enriched fields back to existing Salesforce records from a bulk enrichment?

Add a **Salesforce Update Record** action column directly inside your bulk enrichment table. This pushes enriched values to matching Salesforce records in the same run, without waiting for the Audiences export cycle:

1.  In your bulk enrichment, add your data enrichment columns as usual (for example, `Enrich Person` to find LinkedIn URL, email, or industry).
2.  Click `Add enrichment` and search for **Salesforce** → select **Update Record**.
3.  Set **Record ID** to the Salesforce Contact, Lead, or Account ID already stored in your Audience (the field imported from Salesforce or from your original SOQL import).
4.  Map each enriched field to the corresponding Salesforce field you want to populate.
5.  Click `Start Run` — the Update Record column fires alongside your enrichment columns and writes the enriched values directly to Salesforce.

If you have the Audiences Salesforce export enabled, enriched fields also sync back to Salesforce automatically on the next 24-hour export cycle (see [Writing back to your CRM](#writing-back-to-your-crm)). Adding Update Record directly in the enrichment table is useful when you need immediate write-back or when you are not using the native Audiences Salesforce import.

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

### Why does filtering my People audience by deal attributes return fewer contacts than expected?

When you filter a People audience by opportunity or deal attributes (for example, Stage, Amount, or a custom deal field), Clay only includes contacts that are **directly linked to the matching deal via OpportunityContactRole** in Salesforce — not all contacts at the account that owns the deal.

This means the filter answers "find me everyone who is a contact role on these specific deals," not "find me everyone at companies that have these deals." If your Salesforce org doesn't link contacts to opportunities via OpportunityContactRole, or only a subset of contacts are linked, the resulting People audience will be smaller than you might expect.

**To pull all contacts at accounts with matching deals:**

1.  Build a **Companies** audience filtered by your deal criteria (for example, Stage, Amount, or deal name).
2.  Connect a workflow to that Companies audience (**Send** → **Send to workflow**) that writes a flag value to a custom Salesforce field on each matching account — for example, a **Salesforce Update Record** action that sets a text field to `"target-campaign-q2"`. Publish and run it on all current segment members.
3.  In your **People** audience, add a filter on **Account → [your flag field] equals your flag value**.

This pulls every contact tied to those accounts, regardless of their OpportunityContactRole status.

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

### What happens when I archive a record in Audiences?

Archiving a record is a **soft delete** — the record is not permanently removed from your Audiences workspace. When you archive a record:

-   It is **excluded from all audience segments and workflows** — it will not appear in segment filter results or trigger enrichment automations.
-   It can be viewed in the **Archived** section in the left sidebar.
-   It can be **restored at any time** from the Archived section.

**Note on lookup timing:** After archiving a record, there is a brief processing delay before the change is reflected in `Lookup in Audiences` results. Running a lookup immediately after archiving may still return the archived record — lookups typically update within a short time as changes propagate.

To exclude Salesforce-deleted records from your audience lookups, filter on **Sync status → Deleted in source** to identify them, then archive the records you no longer want matched against.

### Why did Update Audiences Record report 0 fields updated?

This "0 fields updated" result comes from the `Update Audiences Record` action that pushes data into your Audience from a Clay table. The most common cause is that all mapped fields had null values in the source row. This action filters out any field whose value is `null`, `undefined`, or empty before writing to the Audience — when every mapped field is empty, there is nothing to write, so the action completes successfully but reports 0 fields updated. This null-filtering is built into the action and is not user-configurable.

**To confirm this is the cause:** Check whether the columns you mapped into `Update Audiences Record` are populated for the rows that show 0 fields updated.

**To fix it, use an explicit placeholder value instead of null.** Rework your formula so it always returns a meaningful non-null value. For example, if you use a timestamp to mark when a contact becomes eligible, have the formula return the eligible date when it applies and a text value like `"Not Eligible"` when it doesn't. Both are real values, so `Update Audiences Record` writes an update on every run — and you can route off the result (process the row when the field contains a date; skip when it says `"Not Eligible"`).

**Note:** The **Ignore blank values** toggle does exist, but on the `Upsert Audiences Record` action (and on the variant of `Update Audiences Record` that is configured via the Upsert config panel). It is on by default; when disabled, null values are passed through and will clear existing values on the target Audience field. These actions report `✅ Success` (or `✅ Upserting...` / `✅ Updating...`) rather than `0 fields updated`, so the toggle is not what controls the "0 fields updated" message described above.