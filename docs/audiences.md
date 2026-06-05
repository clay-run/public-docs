---
title: Audiences (Beta)
source_url: https://university.clay.com/docs/audiences
description: "Note: This feature is currently in beta for Enterprise customers."
last_synced: 2026-04-27T18:09:16.275Z
---

# Audiences (Beta)

**Note:** This feature is currently in beta for Enterprise customers.

Clay Audiences is the unified data layer for your workspace.  It combines your CRM, data warehouse, and third-party enrichments into one persistent profile per contact and account, updated in real time.

Use it to build dynamic segments across millions of records, run automated enrichment and signal workflows at scale, and sync results back to Salesforce without managing dozens of separate tables.

Setting up Audiences is four major steps:

1.  **Import your data** — connect Salesforce or Snowflake and bring your records into Audiences.
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
-   Salesforce

### Importing from Salesforce

**Note:** Setup must be completed separately for People, Companies, Leads, and Opportunities. Complete steps for `People` first, then repeat for `Companies`, then `Leads`, then `Opportunities`.

1.  Click `Add data` → `Add Source` → select your [**Salesforce integration**](https://university.clay.com/docs/salesforce-integration-overview).
    -   If you don't see an SFDC integration listed, contact your Growth Strategist.
2.  Select `People` at the top of the sync panel.
3.  Enable the `Import` toggle.
4.  Leave `Export Sync` and `Create new Salesforce records` off for now.
5.  Add any SFDC fields you frequently use or want to segment by — only fields included here will appear as columns and filter options in your Audience.
    -   You can add more fields later. See [A Salesforce field isn't appearing in my audience filters](#a-salesforce-field-isnt-appearing-in-my-audience-filters--how-do-i-add-it) in the FAQs below.
6.  Name the corresponding Clay fields — these become the column names in Audiences.
7.  Select `Companies` at the top and repeat steps 3–6 for accounts.
8.  Select `Leads` at the top of the sync panel.
9.  Enable the `Import` toggle.
10.  Add any Lead fields you want to filter or segment by — common fields include `Lead Status`, `Lead Source`, `Title`, and `Company`.
     -   Lead records are automatically merged with matching Contact records into a single person record in your People audience. Data from both sources is combined, and duplicates across Salesforce Leads, Contacts, and other sources count as one person.
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
-   **Whitespace detection** — when importing from a Find People or Find Companies search, records that already exist in All People are automatically excluded from the merge. The draft shows a banner with the count of excluded records ("X records from this search are already in the All People list"), and clicking **All people** adds only the net-new contacts.

Deduplication across sources is automatic. Within Salesforce, it uses SFDC IDs — org duplicates carry over as-is.

## Creating an audience

After importing, you will want to create new audiences, so you can appropriately target the right contacts.

To create a new audience:

1.  Click `People` or `Companies` in the left sidebar.
2.  Click the `+` next to `My Audiences`.
3.  Select `Criteria` and then add a `Filter` or `Filter group`.

### Filter operators by field type

The operators available when building a filter depend on the field's data type, shown by the icon next to the field name:

-   **Text fields (T icon)** — support text-matching operators. To match multiple values at once, use **`contains any of`** or **`does not contain any of`** and enter each value — up to 10 values per filter. For example, to include records where Industry is Health, Beauty, or Pets, set the filter to `Industry → contains any of → Health, Beauty, Pets`. This is more efficient than creating a separate filter for each value.
-   **Number fields (# icon)** — support range operators: **`is greater than`**, **`is less than`**, **`is greater than or equal to`**, and **`is less than or equal to`**. For example, `Employees → is greater than → 500`.

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

**Using Audiences from a Clay table:**

Four Clay actions let you move data between a Clay table and your Audience directly.

-   In any Clay table, click `Add enrichment` and search for:
    -   `Upsert Audiences Record` pushes records from a table into your Audience — creating a new record if no match exists, or updating an existing one if a match is found. Use it to commit data from unsupported integrations (e.g., HubSpot), qualify event lists in a table before adding them to your Audience, or migrate enrichment work already done in a table.
    -   `Update Audiences Record` writes data from a table row to one or more fields on an existing Audience record. Unlike `Upsert Audiences Record`, it does not create a new record if no match is found. Both actions write only to fields that already exist in your Audience — to create a new custom field first, see [How do I create a custom Audience field that isn't tied to Salesforce?](#how-do-i-create-a-custom-audience-field-that-isnt-tied-to-salesforce) below.
    -   `Lookup in Audiences` pulls data from your Audience into a table row. Use it to reference enriched or signal data in a table workflow without making Salesforce API calls. By default, signal data is returned for the past **30 days** and the action returns a maximum of **5 signal results** per record — adjust the lookback period in the column settings to retrieve older signals, or use `Get Audiences Activity` when you need more than 5 results.
    -   `Get Audiences Activity` retrieves signal and activity data for an Audiences record — including signal events and, if Gong is connected to your workspace, Gong call records. Use it when you need more than 5 results or want to query a longer time window than `Lookup in Audiences` provides by default.

### Reviewing enrichment results

After a bulk enrichment runs, there are two ways to see which records were successfully enriched:

**View enrichment status and row-level results**

Click `Enrich` in the top-right toolbar to open the enrichments sidebar. The **Bulk enrichments** tab lists all your enrichments grouped as **Active** and **Inactive**. Each card shows a completion count — for example, "1,234 / 5,000 completed." Completed enrichments appear in the **Inactive** section.

If you're viewing a specific segment, use the dropdown at the top of the list to toggle between enrichments on this segment and enrichments across all audiences.

To inspect row-level results, click `⋮` on any enrichment card and select **Open bulk enrichment**. This opens the underlying bulk enrichment table where you can see each row's output and status.

**Filter the audience by the enriched field**

Since enrichment results write permanently back to All People, you can filter any segment to see only records that received data:

1.  Add a filter to your audience.
2.  Select the enriched field (for example, `Phone` or `LinkedIn URL`).
3.  Set the operator to **`is not empty`** to show only records where the enrichment returned a value.

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

### **Sending audiences to workbooks or ad platforms**

When you have a segment ready, you can send it to a workbook or an ad platform to act on it — enrolling contacts in sequences, running account-based ads, or processing records further before taking action.

1.  Click `Send` → `Export action`.
2.  Then click `Add to workbook` or `Sync to ad platforms`.

**How you might use this:**

-   **Outbound sequences** — send high-fit contacts to a workbook, add personalization (LinkedIn activity, news, custom snippets), then enroll in Outreach or Salesloft.
-   **Account-based advertising** — sync company segments to LinkedIn, Meta, or Google Ads. Contacts who no longer qualify are automatically removed.
-   **Rep-owned outbound** — scope workbooks by territory or rep so each AE works only their assigned accounts.
-   **Additional processing** — send to a workbook to enrich, score, or filter before pushing to your destination.

**Syncing to multiple ad platforms**

Each audience can only be synced to one ad platform at a time — there is no option to add a second platform to an existing sync. To push the same segment to two platforms (for example, both Meta and LinkedIn):

1.  Duplicate the audience by re-creating the same filters in a new audience segment.
2.  On the duplicate, click `Send` → `Sync to ad platforms` and select the second platform.
3.  The two audience syncs are independent — deactivating or removing a sync on one audience does not affect the other.

## Writing back to your CRM

Audiences supports **bidirectional sync** with Salesforce. Enriched data and segment changes write back automatically.

Map any Clay data or segment membership to Salesforce fields. Examples:

-   Personal email → SFDC `Personal Email` field.
-   Segment membership → CRM status, campaign enrollment, lead score, or owner assignment.

Export settings control whether Clay **creates new Salesforce records** for net-new contacts or **only updates existing ones**.

The **`Create new Salesforce records`** toggle is in your Salesforce source settings under the export section. It is **off by default** — when off, Clay only updates Salesforce records that already have a matching entry in your Audience. Turn it on to allow Clay to create new Contacts or Leads in Salesforce for Audience records that don't yet exist in SFDC. This toggle is admin-only.

Export sync behavior:

-   **Export frequency:** Once every 24 hours. Clay assigns each workspace a stable export time automatically — the schedule is not user-configurable.
-   **Export batch size:** ~10,000 records per sync.
-   **Subsequent syncs:** Incremental — only changed records are processed.

To estimate API calls for initial export, divide record count by 10,000 and compare against your Salesforce limit.

**Note:** CRM export is admin-only and currently free during beta. Enrichments and signals follow standard Clay table pricing. Export pricing may change at GA.

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

The field will be available for filtering after the next incremental sync (typically within 15 minutes). Read-only Salesforce fields — fields shown with a lock icon in the mapping because Salesforce does not allow Clay to write them — can still be imported and used as filters. They will show a **Never write (Read-only)** export rule.

### Why does "Company LinkedIn URL" appear in my audience filters when I mapped the field as "LinkedIn URL"?

These refer to the same field. In the Salesforce import field mapping, the LinkedIn URL for accounts is labeled **"LinkedIn URL"**. In the audience filter builder, that same field appears as **"Company LinkedIn URL"** — Audiences automatically adds the "Company" prefix to distinguish it from the equivalent person-level field, which appears as **"Person LinkedIn URL"** in People audiences.

The underlying field and data are identical. If you mapped Salesforce's Account LinkedIn URL field and named it "LinkedIn URL" in your import settings, filtering on "Company LinkedIn URL" in your Companies audience targets that same mapped field.

### My CRM is messy. Should I clean it up before setting up Audiences?

You don't need a clean CRM to get started — CRM cleanup is often the first use case Audiences enables. A common approach: sync your existing CRM, run LinkedIn enrichments to refresh contact data, use the enriched identifiers to surface duplicates, then build further enrichments from there.

### Does Audiences update automatically?

Yes. Segments update in real time as records enter or change, typically within 15 minutes. Enrichments and actions trigger automatically for new records when the autoenrich toggle is enabled. No manual runs required after initial setup.

### Can I sync an audience to multiple ad platforms?

Not directly — each audience supports one active ad platform sync at a time. To push the same segment to both Meta and LinkedIn, duplicate the audience and set up a separate sync on the duplicate pointing to the second platform. The two audiences and their syncs are fully independent of each other.

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

### Why does filtering my People audience by deal attributes return fewer contacts than expected?

When you filter a People audience by opportunity or deal attributes (for example, Stage, Amount, or a custom deal field), Clay only includes contacts that are **directly linked to the matching deal via OpportunityContactRole** in Salesforce — not all contacts at the account that owns the deal.

This means the filter answers "find me everyone who is a contact role on these specific deals," not "find me everyone at companies that have these deals." If your Salesforce org doesn't link contacts to opportunities via OpportunityContactRole, or only a subset of contacts are linked, the resulting People audience will be smaller than you might expect.

**To pull all contacts at accounts with matching deals:**

1.  Build a **Companies** audience filtered by your deal criteria (for example, Stage, Amount, or deal name).
2.  From your Companies audience, click **Send → Add to workbook** to export the matched accounts.
3.  In the workbook, write a flag value to a custom Salesforce field on those accounts (for example, a text field set to `"target-campaign-q2"`).
4.  In your **People** audience, add a filter on **Account → [your flag field] equals your flag value**.

This pulls every contact tied to those accounts, regardless of their OpportunityContactRole status.

### Why does Clay MCP show activity data for a contact when the Audiences Activity tab shows no activity?

When a Salesforce lead is converted to a contact, Audiences merges both records into a single People entry using the lead's `ConvertedContactId`. The underlying activity data from the lead record — including activity counts and last-activity dates — is stored in Audiences and is accessible via Clay MCP, including the `ask-question-about-accounts` tool, which queries your Audiences data at the backend level.

However, the current Audiences UI contact view does not yet display a full union of all data from the converted lead. This means activity counts and last-activity dates that originated from the lead record may not appear in the contact's Activity tab even though the data exists in Audiences and is retrievable via MCP.

**Note (beta):** This discrepancy is a known gap during the Audiences beta. When you see activity data returned by Clay MCP for a contact whose Activity tab appears empty, that data is sourced from the corresponding converted lead record. The UI will be updated to show the full union of contact and converted lead data before general availability.

### Why isn't a signal showing up in my Lookup in Audiences result?

Three things to check:

-   **The signal falls outside the default lookback window.** `Lookup in Audiences` returns signal data for the past 30 days by default. If the signal event is older than 30 days, open the column settings and increase the lookback period.
-   **The 5-result cap was reached.** `Lookup in Audiences` returns a maximum of 5 signal results per record. If a company has more active signals than that, some may not appear. Use `Get Audiences Activity` to retrieve a larger set of signal data.
-   **The signal hasn't fired for that record yet.** Signal results are written asynchronously and may not appear immediately after a signal run completes. If a signal should be recent but is still missing, open the signal's column header → `Edit column` and re-run the signal to refresh the data for that record.

### What happens when I archive a record in Audiences?

Archiving a record is a **soft delete** — the record is not permanently removed from your Audiences workspace. When you archive a record:

-   It is **excluded from all audience segments and workflows** — it will not appear in segment filter results or trigger enrichment automations.
-   It can be viewed in the **Archived** section in the left sidebar.
-   It can be **restored at any time** from the Archived section.

**Note on lookup timing:** After archiving a record, there is a brief processing delay before the change is reflected in `Lookup in Audiences` results. Running a lookup immediately after archiving may still return the archived record — lookups typically update within a short time as changes propagate.

To exclude Salesforce-deleted records from your audience lookups, filter on **Sync status → Deleted in source** to identify them, then archive the records you no longer want matched against.
