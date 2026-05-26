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
5.  Add any SFDC fields you frequently use or want to segment by.
    -   You can update these later.
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
     -   Opportunity data is associated with your Companies records and becomes available as a filter in your Companies audience.
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

### Sending data from Clay table

You can also send contacts from any existing Clay table directly to your Audience:

1.  Open any table with contacts you want to save to your Audience.
2.  Click `Continue` at the bottom of the table.
3.  Select `Save to People` or `Save to Companies` depending on the record type.

Records saved from tables are automatically deduplicated and merged with your existing audience data.

### Entity resolution and deduplication

Clay matches records using LinkedIn URL and email to:

-   **Cross-source deduplication** — merge the same person from multiple sources.
-   **Whitespace detection** — when importing from a Find People or Find Companies search, records that already exist in All People are automatically excluded from the merge. The draft shows a banner with the count of excluded records ("X records from this search are already in the All People list"), and clicking **All people** adds only the net-new contacts.

Deduplication across sources is automatic. Within Salesforce, it uses SFDC IDs — org duplicates carry over as-is. Native within-source deduplication is coming.

Records need a high-confidence identifier to match. Auto-enrichment adds `LinkedIn URL` and `CPJ ID` at no cost to improve matching.

## Creating an audience

After importing, you will want to create new audiences, so you can appropriately target the right contacts.

To create a new audience:

1.  Click `People` or `Companies` in the left sidebar.
2.  Click the `+` next to `My Audiences`.
3.  Select `Criteria` and then add a `Filter` or `Filter group`.

### Filter operators by field type

The operators available when building a filter depend on the field's data type, shown by the icon next to the field name:

-   **Text fields (T icon)** — support text-matching operators. To match multiple values at once, use **`contains any of`** and enter each value. For example, to include records where Industry is Health, Beauty, or Pets, set the filter to `Industry → contains any of → Health, Beauty, Pets`. This is more efficient than creating a separate filter for each value.
-   **Number fields (# icon)** — support range operators: **`is greater than`**, **`is less than`**, **`is greater than or equal to`**, and **`is less than or equal to`**. For example, `Employees → is greater than → 500`.

**Note:** A field that appears numeric may have been imported as text (shown by a T icon rather than #). Text fields — such as "Annual revenue range" synced from Salesforce as a string — will not show range operators. To use range filtering on a field, it must be configured as a Number type in Clay.

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

Two Clay enrichments let you move data between a Clay table and your Audience directly.

-   In any Clay table, click `Add enrichment` and search for:
    -   `Upsert Audiences Record` pushes records from a table into your Audience — creating a new record if no match exists, or updating an existing one if a match is found. Use it to commit data from unsupported integrations (e.g., HubSpot), qualify event lists in a table before adding them to your Audience, or migrate enrichment work already done in a table.
    -   `Lookup in Audiences` pulls data from your Audience into a table row. Use it to reference enriched or signal data in a table workflow without making Salesforce API calls.

**Accessing company data from People records in a workbook:**

When you send a People audience segment to a workbook, person records include a `related_ids` section alongside their `fields`. Company information is **not** a flat field on person records — companies are a separate entity in Audiences, linked by Audiences ID. The `Company` field in person `fields` will be null even when the person is visually associated with a company in the Audiences UI.

To supply company details (domain, name) as inputs for an enrichment waterfall:

1.  In your workbook, navigate the **Audiences Record** data for the person row to `records > 0 > related_ids > account_ids > 0` — this is the Audiences ID of the person's first linked company.
2.  Add a **Lookup in Audiences** enrichment. Set the entity type to **Companies** and filter by **Audiences ID**. Map the value from step 1 as the ID to filter on.
3.  From the lookup result, access `records > 0 > fields` to find company fields such as domain and name, and map them as inputs to your enrichment waterfall.

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

Export sync behavior:

-   **Export frequency:** Every 24 hours when write-back is enabled.
-   **Export batch size:** ~10,000 records per sync.
-   **Subsequent syncs:** Incremental — only changed records are processed.

To estimate API calls for initial export, divide record count by 10,000 and compare against your Salesforce limit.

**Note:** CRM export is admin-only and currently free during beta. Enrichments and signals follow standard Clay table pricing. Export pricing may change at GA.

## FAQs

### When should I use Audiences vs. a table?

Use Audiences by default for anything you want to reuse, segment on, or build automations on top of. Use tables for one-off workflows, integrations Audiences doesn't yet support natively, or cases where data doesn't need to persist beyond a single run.

### What if my integration isn't supported yet?

Use the `Upstream to Audiences` table enrichment as a bridge. Bring your data into a Clay table from any source, then use Upstream to push those records permanently into your audience. This works for any source Audiences doesn't yet natively support.

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

**If visitors arrived before your Salesforce sync was connected:** Web intent records added to Audiences before you connected Salesforce may not automatically merge with existing SFDC records. To resolve this, use the **deterministic record matching** option in your Salesforce import settings and select domain as the match key. This matching applies to records coming in after the setting is enabled — it does not retroactively deduplicate records already in Audiences.
