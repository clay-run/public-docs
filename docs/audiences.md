---
title: Audiences (Beta)
source_url: https://university.clay.com/docs/audiences
description: "Note: This feature is currently in beta for Enterprise customers."
last_synced: 2026-04-27T18:09:16.275Z
upstream_hash: 179d0c9feae111ee5bff85d8a1428b47ca0754c5ef6639700f2c80852a25a96b
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
-   **Whitespace detection** — exclude CRM records when importing from CPJ/People Search.

Deduplication across sources is automatic. Within Salesforce, it uses SFDC IDs — org duplicates carry over as-is. Native within-source deduplication is coming.

Records need a high-confidence identifier to match. Auto-enrichment adds `LinkedIn URL` and `CPJ ID` at no cost to improve matching.

## Creating an audience

After importing, you will want to create new audiences, so you can appropriately target the right contacts.

To create a new audience:

1.  Click `People` or `Companies` in the left sidebar.
2.  Click the `+` next to `My Audiences`.
3.  Select `Criteria` and then add a `Filter` or `Filter group`.

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

## Writing back to your CRM

Audiences supports **bidirectional sync** with Salesforce. Enriched data and segment changes write back automatically.

Map any Clay data or segment membership to Salesforce fields. Examples:

-   Personal email → SFDC `Personal Email` field.
-   Segment membership → CRM status, campaign enrollment, lead score, or owner assignment.

Export settings control whether Clay **creates new Salesforce records** for net-new contacts or **only updates existing ones**.

Export sync behavior:

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

### What happens to a contact's ad targeting when they become a customer?

If your segment has an exclusion condition (e.g., Account Type ≠ "Customer"), the contact is automatically **removed** from the synced ad audience as soon as that condition is met. See [Clay Ads](https://university.clay.com/docs/clay-ads) for platform-specific guidance.
