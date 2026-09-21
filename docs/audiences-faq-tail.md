### Can I connect multiple Salesforce accounts to Audiences?

No. Audiences supports one Salesforce connection per workspace. Once a Salesforce account is connected, the Salesforce source panel shows that account as a read-only field — there is no dropdown or `+ Add account` option to switch to or add a second Salesforce org.

**Note:** Changing your workspace's default Salesforce connector in **Settings → Connections** does not affect which Salesforce account Audiences uses. Audiences stores a direct reference to the account that was originally connected — the Add Source panel will continue to show that account as read-only regardless of which connector is set as the workspace default.

You can still add multiple imports from the same connected Salesforce account — for example, separate imports for Contacts, Accounts, and SOQL-filtered subsets — but all imports come from the same Salesforce org.

**To switch to a different Salesforce account** (for example, moving from a UAT org to a production org): remove the existing Salesforce source from Audiences, then reconnect with the new account. Before removing, note down your current field mappings — field mapping configurations cannot be recovered after a source is removed. See [I removed and re-added my Salesforce source in Audiences and my field mappings are gone — how do I restore them?](#i-removed-and-re-added-my-salesforce-source-in-audiences-and-my-field-mappings-are-gone--how-do-i-restore-them) for the full implications.

If you need data from a second Salesforce org in Audiences without removing the existing connection, the available workaround is: connect the second org under **Settings → Connections**, bring its records into a Clay table using Salesforce actions, then push those records into Audiences using `Upsert Audiences Record`. Note that Clay table row limits apply in this path.

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

### I removed and re-added my Salesforce source in Audiences and my field mappings are gone — how do I restore them?

Field mappings cannot be recovered once a Salesforce import is removed. The mappings are tied to the specific import configuration — when that import is deleted and a new one is created, the previous mappings are not retained. There is no restore or mapping-history option, so you will need to add the fields back manually.

**To re-add your field mappings:**

1.  Click **Add data** in the top toolbar.
2.  Find your Salesforce integration and click the **⋮** (three-dot) menu next to it.
3.  Select **Settings**, then open the relevant object import (for example, Contacts or Accounts).
4.  In the field-mapping section, add each field you previously had configured.
5.  Click **Save and review** → **Confirm**.

The fields will appear as filter options after the next incremental sync.

**To avoid this in the future:** If your Salesforce connection has a permissions issue, do not remove the Salesforce source from Audiences — removing it deletes the import configuration and field mappings along with it. Instead:

-   Fix the permissions directly in Salesforce — update the connected user's profile or permission sets in Salesforce Setup.
-   If the connection itself needs to be refreshed, use **Reconnect** on your Salesforce connection under **Settings → Connections** in Clay. This reauthorizes the OAuth credential without affecting your Audiences import configurations or field mappings.

### Can I see when the weekly full sync is scheduled, or trigger it manually?

No. The Clay UI shows only that the Salesforce full sync runs weekly — it does not display the exact day or time the next full sync is scheduled for your workspace. The timing is assigned automatically per workspace and is not shown in the interface.

There is no self-serve option to trigger a full sync manually. If you need an expedited full sync — for example, to pick up formula field updates that are not captured by incremental syncs — contact Clay support.

**Workaround for specific records:** The incremental sync (every 15 minutes for Enterprise, once daily for Growth) picks up any Salesforce record whose `SystemModstamp` has been updated. To re-sync specific records sooner, make a small edit to those records in Salesforce — for example, add and remove a space in any field. This updates `SystemModstamp` and Clay will pick up those records on the next incremental sync, without waiting for the weekly full sync.

### Why is my Salesforce Audiences import failing with "Salesforce Bulk API job failed. Records processed: 0"?

This error means Salesforce's Bulk API 2.0 rejected the import job before processing any records. Audiences uses Bulk API 2.0 for all initial full imports and weekly re-syncs. The Bulk API does not support SOQL **semi-joins** — queries where the `WHERE` clause contains a nested `SELECT` statement, for example:

```sql
SELECT Id, FirstName, LastName, AccountId, SystemModstamp, IsDeleted
FROM Contact
WHERE Id IN (SELECT ContactId FROM OpportunityContactRole WHERE ...)
```

A semi-join passes Clay's **Preview** step (which uses Salesforce's standard REST API to estimate matching records) but causes the Bulk API job to fail immediately, surfacing as **"Salesforce Bulk API job [ID] failed. Records processed: 0"** with no records imported.

**Fix:** Remove the nested sub-select and use only direct field filters on the object you are importing. Open the import settings, update the SOQL query to eliminate the semi-join, and re-run the sync. For example, instead of filtering contacts by `WHERE Id IN (SELECT ContactId FROM OpportunityContactRole WHERE ...)`, import all contacts and apply the opportunity contact-role condition as an **audience segment filter** after importing — segment filters evaluate cross-object lookups using a separate query path that supports them.

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

Tables that have an `Upsert Audiences Record` column configured for People also appear in the **Person source** filter by the table's display name — look for the table's name in the same dropdown. (The equivalent filter for Companies audiences shows tables that have an `Upsert Audiences Record` column configured for Companies.) If your table still doesn't appear in the dropdown after checking both display names, contact Clay support.

### How do I find which Clay table a lead in Audiences came from?

Each record in Audiences has a **Source** column that shows the display name of the data source the record originated from. For records sent to Audiences from a Clay table (via **Continue → Save to People** or **Save to Companies**), the Source column displays the table's name.

The Source column is plain text — there is no direct link from the Source column to open the originating table. To open the table, use its name to find it in your workspace's tables list.

**Note:** To filter your audience to show only records that came from a specific table, use the **Person source** filter — see [Why doesn't my Clay table appear in the Person source filter?](#why-doesnt-my-clay-table-appear-in-the-person-source-filter) above.

### My CRM is messy. Should I clean it up before setting up Audiences?

You don't need a clean CRM to get started — CRM cleanup is often the first use case Audiences enables. A common approach: sync your existing CRM, run professional network enrichments to refresh contact data, use the enriched identifiers to surface duplicates, then build further enrichments from there.

### Does Audiences update automatically?

Yes. Segments update in real time as records enter or exit your filter criteria. The refresh frequency depends on your plan:

-   **Enterprise plan:** CRM and data warehouse **imports** (CRM → Clay) run every 15 minutes, and segments update continuously.
-   **Growth plan:** CRM and data warehouse **imports** run daily, and segments update based on that daily refresh.

The 15-minute (or daily) cadence applies to the **import direction only** — it reflects changes from your CRM in Clay. The reverse direction — exporting enriched data from Clay back to Salesforce — runs on a **separate 24-hour schedule**. See [I enriched data in my Audience. Why hasn't it appeared in Salesforce yet?](#i-enriched-data-in-my-audience-why-hasnt-it-appeared-in-salesforce-yet) for details.

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

The Audiences screen does not have a direct CSV download button. To download audience data as a CSV, use the **Enrich** flow to create an enrichment table from the segment, then export that table. **Admin access is required.**

1. Open the audience segment you want to export.
2. Click `Enrich` to open the enrichment panel, then create a new enrichment table for this segment. (The exact button label varies by workspace — you may see **Add bulk enrich** or a `+` button with a **Create Enrichment Table** option.)
3. In the enrichment setup, skip adding enrichment columns and turn off field mapping if you only need the raw segment data.
4. Open the resulting table. If any rows are checked, uncheck them first — the toolbar shows **Tools** only when no rows are selected.
5. Click **Tools** → **Export** → **Download CSV**.

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

### How do I make my Salesforce export conditional on a field match?

The native Audiences export write rules — **Never write**, **Always write**, and **Write if empty** — apply uniformly to all records in the export. There is no per-row condition that prevents a field from being written based on a value comparison, such as "only update this contact if its Salesforce Account ID matches the Account ID on the Audience Company Record."

For that kind of conditional write-back, connect a **Workflow** to your audience segment:

1. Navigate to the segment and click **Send** → **Send to workflow**.
2. In the workflow editor, add a **Lookup** step to retrieve the values you want to compare — for example, the contact's current Salesforce Account ID and the Account ID from the Audience Company Record.
3. Add a **Branch (conditional)** node that checks whether the two values match.
4. On the matching branch, add a **Salesforce Update Record** action to write the data back to Salesforce.
5. Publish the workflow. Contacts that don't pass the check are skipped at the branch node and are not written to Salesforce.

If your goal is to control which contacts are *imported* into Audiences from Salesforce in the first place — for example, importing only contacts whose `AccountId` belongs to a specific set of accounts — use a **SOQL record subset** import rather than importing all records. A SOQL filter on `AccountId` limits which contacts enter Audiences and therefore which contacts are candidates for export. See [Importing a record subset using SOQL](#importing-a-record-subset-using-soql) for setup steps.

### How do I create new Salesforce Accounts or Contacts from an Audience?

New Salesforce records are not created automatically when you run a bulk enrichment. Record creation is not driven by a Create Contact or Create Account action inside the enrichment table — it is controlled by the **`Create new Salesforce records`** toggle in your Audiences Salesforce export settings.

**Before you enable the toggle, create a Clay ID field in Salesforce.** The Clay ID field is a custom External ID field in Salesforce — for example, `Clay_ID__c` — that must be marked as **External ID** in Salesforce so it appears as a selectable option in Clay. Clay uses this field to stamp each new record it creates with a unique identifier, so it can identify and update that record on future syncs without creating duplicates. Have your Salesforce admin create this field on the relevant object (Contact or Account) before proceeding.

To push net-new Accounts or Contacts to Salesforce:

1.  Open your Audiences workspace and go to your Salesforce source settings.
2.  Under the export section, enable the **`Create new Salesforce records`** toggle. (Admin access required — the toggle is off by default.)
3.  In the **Record matching** section, select the Clay ID field you created (for example, `Clay_ID__c`) from the **Select Clay ID field** dropdown. If the field doesn't appear, confirm it is marked as **External ID** in Salesforce, then close and reopen the settings panel.
4.  Confirm your field mappings and save.

Once the toggle is on, Clay will create new Accounts or Contacts in Salesforce for any Audience record that doesn't already have a matching SFDC entry. (Leads and Opportunities do not support record creation through this toggle.)

**What about existing contacts?** Records already imported from Salesforce are tracked by their Salesforce Object IDs — Clay updates them directly without using the Clay ID field. The Clay ID field stays empty on those records and only comes into play for net-new records Clay creates.

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
3.  Click `Add enrichment` and search for **HubSpot** → select **HubSpot: Update object** (to update an existing HubSpot contact or company) or **HubSpot: Create object** (to create a new contact or company in HubSpot).
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

### Do Activities or Opportunities count toward my plan's record limit?

No. The record limit — 250,000 for Growth plans and 25,000,000 for Enterprise plans — counts only your imported **Account**, **Contact**, and **Lead** records. When you enable **Import activities** on a Salesforce Accounts import, the resulting Tasks and Events are stored as activity events linked to each account's detail view and are not counted as separate records. Similarly, Opportunity data imported from Salesforce is associated with your existing Company (Account) records and available as a filter in Companies audiences, but Opportunities are not counted as separate records against your plan limit.

### I changed a field value in Salesforce but it's not updating in Clay

Clay's incremental sync picks up Salesforce changes via `SystemModstamp` — any modification to a Salesforce record triggers a re-sync of all its mapped fields on the next incremental cycle (every 15 minutes on Enterprise, once daily on Growth). However, if the field's current value in Clay was set by a **bulk enrichment** or **Upsert Audiences Record**, Clay's conflict resolution keeps that bulk-enriched value rather than accepting the incoming CRM value. Bulk enrichments and Upsert Audiences Record are Priority 1; Salesforce Account/Contact/Opportunity imports are Priority 2 (see **Conflict resolution when sources provide different field values** under [Entity resolution and deduplication](#entity-resolution-and-deduplication) above).

To accept the Salesforce value, you have two options:

-   **Override the field with a new bulk enrichment.** Use **Update Audiences Record** in a bulk enrichment table to explicitly write the value you want (for example, `0` or null). Because `Update Audiences Record` is also Priority 1, this new value replaces the old bulk-enriched one and stays unless overwritten by another enrichment. See [Adding enrichments](#adding-enrichments).

-   **Archive and re-import the record.** Archive the record in Audiences, then let the next Salesforce sync re-create it with the current Salesforce values. This is a heavier operation best reserved for cases where you need to fully reset a record's field history. See [How do I remove records from an audience?](#how-do-i-remove-records-from-an-audience).

### I enriched data in my Audience. Why hasn't it appeared in Salesforce yet?

Audiences exports to Salesforce run on a **24-hour schedule**. After you enrich data in Audiences, you may need to wait up to 24 hours for the next scheduled export to push the values to Salesforce.

If you need data in Salesforce immediately without waiting for the next scheduled export, add a **Salesforce Update Record** column directly to your bulk enrichment table — see [How do I write enriched fields back to existing Salesforce records from a bulk enrichment?](#how-do-i-write-enriched-fields-back-to-existing-salesforce-records-from-a-bulk-enrichment) above.

### Can the Audiences export sync write data back to Salesforce Lead records?

No. The scheduled Audiences export sync applies to **Contact** and **Account** object types only. Lead records imported into Audiences are import-only — there is no scheduled export rule column in the Lead field mapping, and the Audiences export cycle does not push data back to Salesforce Leads.

To push enriched Audience data back to Salesforce Lead records, use a **Salesforce Update Record** action column in a bulk enrichment table:

1.  Navigate to an audience segment containing the Lead records you want to update and click **Enrich** → **Add bulk enrich**.
2.  Add your data enrichment columns.
3.  Click `Add enrichment` and search for **Salesforce** → select **Update Record**.
4.  Set **Record ID** to the Salesforce Lead ID field stored in your Audience.
5.  Map each enriched field to the corresponding Salesforce Lead field.
6.  Click `Start Run`.

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

**People records from other sources (CSV, people search, Clay table):** If your People audience records were imported via CSV, a people search, or a Clay table send — rather than Salesforce Contacts — company name is not automatically carried over as a field on those records. People audience records do not have a built-in Company Name field, and there is no path in Audiences to copy company-level fields directly onto People records.

If you need company name alongside each person in a table workflow, the recommended approach is to build that association in Clay Tables:

1. Build your company list in a Clay table.
2. In that company table, click **Tools → Import → Find people at these companies**. Apply title, seniority, and location filters, then click **Continue** to generate a people table.
3. Clay automatically adds a **Company Table Data** column to the resulting people table. This column carries all fields from the linked company row — including company name, domain, and any other columns you've added to your company table — into each person's row.

This gives you company context directly alongside each person in the table without requiring company name to be stored as a field in Audiences.

### My Clay segment has far fewer records than my Salesforce report with the same filters — why?

Clay audience segments count only the records that currently match your filters based on data that has been synced into Audiences — not live Salesforce data at query time. A large gap between your segment count and a matching Salesforce report usually traces to one of two causes.

**A filter field is empty for most records.** If you added a field to your Salesforce import mapping after the initial sync, existing records that haven't been re-synced yet have no value for that field in Audiences. A numeric range condition — for example, Annual Revenue between $50M and $5B — excludes every record where the field is empty, even if those same records have a value for the field in Salesforce. This also happens when a segment filter points at a newly added duplicate of an existing field rather than the original mapped field: the duplicate has no data for any record that hasn't been re-synced since it was added.

To resolve this:
1. Check which field your range condition targets. If two similarly named fields appear in the filter picker, use the one that was part of the original import — not a recently added copy.
2. To fill in missing values for specific records right away, make a small edit to those records in Salesforce (for example, add and remove a space in any text field). This updates `SystemModstamp` and Clay re-syncs the record — with all its current field values — on the next incremental sync (within 15 minutes on Enterprise plans, once daily on Growth plans). All records are backfilled automatically on the next weekly full sync.

For more on how newly added fields are populated, see [I added a new Salesforce field to my mapping but some records are missing data for it](#i-added-a-new-salesforce-field-to-my-mapping-but-some-records-are-missing-data-for-it).

**A filter is using a contact-level field instead of the account-level field (or vice versa).** Fields mapped from the Salesforce Contact object and fields mapped from the Salesforce Account object are stored separately in Audiences and answer different questions. For example, a **Type** field mapped from the Salesforce Contact object reflects the type value on each individual contact record. A **Type** field mapped from the Salesforce Account object reflects the type on the contact's parent account — which is what most Salesforce account-level reports filter on. If your Salesforce report uses the account's Type but your segment filters on the contact's Type, the two conditions measure different things and return different counts.

To match your Salesforce report, confirm your segment filter is using the field from the same Salesforce object as the report. Both contact-level and account-level fields appear in the filter picker, and similarly named fields from different objects may look identical if your import mapping did not give them distinct column names. Edit the filter condition and verify the source object to confirm you are filtering on the right field.

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

-   **All fields must have an exact match.** If you filter by both `Email` and a secondary identifier field (such as a profile URL), a record must match both to be returned — a partial match on only one field returns nothing.
-   **Empty fields count as non-matches.** If a field value in your Audience record is empty (null), it will not match any filter condition on that field — including equality checks. For example, filtering by `Profile URL = <value>` will not return records that have an empty Profile URL field, even if the Email matches.

If you need to look up a record that may be missing one of your identifier fields, filter by the field most likely to be populated (typically `Email` or `Profile URL`), and use a single-field filter rather than combining multiple conditions.

### How do I remove records from an audience?

To remove records from your Audience, you archive them. Archiving moves a record to the **Archived** section in the left sidebar — it is no longer visible in any active segment, including All People or All Companies. Archived records can be restored from the **Archived** section at any time.

**Note:** Removing a data source from your import settings (for example, disconnecting HubSpot from your Sources) does not remove the contacts or companies already imported — records persist in Audiences even after their source is removed. To remove those records, archive them manually using one of the methods below.

**To archive a single record:**

1.  Open any record in your Audiences view by clicking on it.
2.  In the record detail panel, click the **⋮** (three-dot) menu in the top right.
3.  Select **Archive record**.
4.  Confirm the action. The record is immediately moved to the Archived section and removed from all active segments.

**To archive multiple records using row selection:**

1.  In your Audiences view, select the rows you want to archive by clicking the checkboxes to the left of each row.
2.  With rows selected, a toolbar appears at the bottom of the screen.
3.  Click **Archive** in the toolbar.
4.  Confirm the action. All selected records are moved to the Archived section.

**To bulk-archive all records from a specific source (recommended for large-scale cleanup):**

The fastest way to archive many records at once — for example, to remove all contacts imported from a HubSpot account you have disconnected — is to create a segment filtered by that source, then archive all records in the segment at once:

1.  In **People** or **Companies**, click **+ Filter** and add a filter on **Origin source**. Select the source you want to clear (for example, `HubSpot Contact - [your account name]`).
2.  Click **Create segment** to save this as a named segment. The **Archive records** option only appears on saved segments — it is not available while the filter is in unsaved (draft) state.
3.  In the left sidebar, click the **⋮** (three-dot) menu next to the segment's name.
4.  Select **Archive records** and confirm. All records currently in the segment are moved to the Archived section and removed from all active segments.

**Note:** **Delete list** in the same segment menu removes the segment from the sidebar but does not archive the records. Use **Archive records** when you want to remove the contact or company records themselves.

**Note:** Archived records can be restored from the **Archived** section in the left sidebar. If a previously archived record enters Audiences again from a source (for example, if the underlying Salesforce record is modified and re-synced), it will appear as a new record without the archived record's enrichment data.

### How do I replace a CSV import with updated data?

CSV imports are one-time — they do not re-sync automatically. If your CSV contained errors and you want to replace it with corrected data, follow these steps to avoid duplicating records:

**1. Archive the old records:**

Before importing the corrected file, remove the incorrect records from your Audience:

1.  Go to **All People** or **All Companies** in your Audiences view.
2.  Filter by the source of the old CSV import (use the **Person source** or **Company source** filter and select the original CSV import name).
3.  Select all rows returned by the filter.
4.  Click **Archive** in the toolbar that appears at the bottom.
5.  Confirm. All records from the old CSV are removed from your Audience.

**2. Import the corrected CSV:**

1.  Click `Add data` → `Add Source` → select **CSV**.
2.  Upload the corrected file and complete the import steps as usual.

The corrected records are imported fresh without duplicating the old ones.

**Note:** If your Audience record count appears higher than expected after importing a corrected CSV — even after archiving — it may mean some records from the original import were merged with records from another source (for example, Salesforce) during entity resolution. Archived records that matched a non-CSV source may still appear in your Audience under that source. In this case, contact Clay support to assist with cleanup.

### How does the Audiences record limit work? What counts toward it?

The Audiences record limit is a **per-workspace cap** on the total number of unique records stored in your Audience, regardless of which source they came from. Growth plans cap at 250,000 records; Enterprise plans cap at 25,000,000.

Records that count toward the limit:

-   All records in **All People** (contacts and leads from any source)
-   All records in **All Companies** (accounts from any source)

Records that do **not** count:

-   Archived records (moved to the Archived section; not counted toward the limit while archived)
-   Segment memberships (a record in 10 different segments still counts as one record)

If your workspace reaches the limit, Clay will stop importing new records from your connected sources until the count drops below the cap. To free up space: archive records you no longer need (see [How do I remove records from an audience?](#how-do-i-remove-records-from-an-audience) above), or upgrade your plan.

Growth plans have a hard cap — there is no add-on to increase the limit without upgrading to Enterprise.

### Can I add a "notes" or "memo" field to an Audience record?

Yes — you can create a custom text field in Audiences and update it from a Clay table using `Update Audiences Record` or `Upsert Audiences Record`. There is no built-in "notes" column, but a custom field works the same way.

**To set this up:**

1.  Create a custom Audience text field — see [How do I create a custom Audience field that isn't tied to Salesforce?](#how-do-i-create-a-custom-audience-field-that-isnt-tied-to-salesforce) above.
2.  In your Clay table, add an `Update Audiences Record` or `Upsert Audiences Record` column.
3.  Map the text column in your table to the custom notes field in Audiences.
4.  Run the column — the value writes permanently to the Audience record.

You can then filter segments on this field, export it to Salesforce, or use it as input for enrichments.

### Why does my Databricks import fail with a schema or permission error?

Databricks imports in Audiences use the Unity Catalog. Two common causes of failure:

**1. The service principal lacks SELECT on the target table.**

In Databricks, grant the service principal read access to the catalog, schema, and table you're importing:

```sql
GRANT USE CATALOG ON CATALOG <catalog_name> TO `<service-principal-id>`;
GRANT USE SCHEMA ON SCHEMA <catalog_name>.<schema_name> TO `<service-principal-id>`;
GRANT SELECT ON TABLE <catalog_name>.<schema_name>.<table_name> TO `<service-principal-id>`;
```

Replace `<service-principal-id>` with the application ID of the service principal connected to Clay.

**2. The table is not registered in Unity Catalog.**

Audiences can only import from tables registered in Unity Catalog — it cannot query tables or views defined in the legacy Hive metastore. To migrate a legacy table, use `CREATE TABLE ... AS SELECT` in Unity Catalog to register a copy, or move the underlying data to a Unity Catalog volume.

If neither of these applies and the import still fails, contact Clay support with the error message shown in the import setup.

### How do I archive records that no longer match my Snowflake import query?

When you update your Snowflake SQL query to exclude records — for example, removing rows below a revenue threshold — those records are marked **Deleted in source** in your Audience on the next full sync (within 7 days). They are not automatically archived; they remain in All People or All Companies with a **Deleted in source** status.

To remove them from your Audience, archive them manually:

1.  Go to **All People** or **All Companies** in your Audiences view.
2.  Add a filter: **Source** → select your Snowflake import → set status to **Deleted in source**.
3.  Select all returned rows.
4.  Click **Archive** in the bottom toolbar and confirm.

Archived records can be restored at any time from the **Archived** section in the left sidebar.
