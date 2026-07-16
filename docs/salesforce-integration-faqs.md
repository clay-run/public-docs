---
title: Salesforce integration FAQs
description: Answering common questions about connecting and troubleshooting the
  Salesforce integration.
last_synced: 2026-04-26T01:40:34.981Z
---

# Salesforce integration FAQs

Answering common questions about connecting and troubleshooting the Salesforce integration.

This doc answers common questions about connecting and troubleshooting the Salesforce integration. For setup instructions and how to use Salesforce actions in Clay, see [this doc](https://www.clay.com/university/guide/salesforce-integration-overview).

## What permissions and scope do I need for the Salesforce enrichment?

**Required Permissions for Your Clay User**

To connect Clay to Salesforce, your Clay user needs:

1.  Access Identity Information (profile, email, address, phone)
2.  Manage User Data via APIs
3.  Perform Requests Anytime (refresh\_token, offline\_access)

An OAuth user must set up the initial connection. After that, any user in your Clay workspace can use the integration.

**Connection Scope and Permissions**

The Salesforce connection is tied to the OAuth user who sets it up:

-   **Data Pull**: Import or look up Salesforce records, limited to the fields and objects the OAuth user can access
-   **Data Push**: Create or update Salesforce records where the OAuth user has write access

For sensitive fields, you can create a permission set to restrict the OAuth user's access.

## What controls are available at the connector level versus inside individual tables?

When you connect Salesforce to Clay, access control works at two levels:

**Connector level (Salesforce controls this)**

The Salesforce user you authenticated with determines everything Clay can read or write. Clay's Salesforce actions — lookup, create, update, upsert — are all restricted to whatever that user is permitted to do in Salesforce. If the user cannot read the Opportunity object in Salesforce, Clay cannot read it either. If the user has write access to `Account.Website`, every Clay table using that connection can update that field.

Permissions are managed entirely on the Salesforce side, through that user's profile, permission sets, field-level security, org-wide defaults, sharing rules, and role hierarchy.

**Table (workbook) level (Clay controls this)**

Inside a Clay table, you configure which actions to run (such as Lookup Record, Create Record, Update Record) and which fields to read or write for each action. Field update behavior is set per table, not at the connection level. These table-level settings determine what the table _attempts_ to do — the connected Salesforce user's permissions are still the final gate on what actually succeeds.

**There is no table-level permission isolation in Clay**

You cannot restrict individual tables to specific Salesforce objects or fields. For example, there is no setting that says "only table A can update the Website field on accounts" or "only tables B and C are allowed to read contacts and opportunities." All Clay tables that use the same connection share the same Salesforce access as the connected user.

If you need different tables to have different levels of access — for example, one table that can only read and another that can write — create separate Salesforce connections authenticated as different Salesforce users, each with the appropriate Salesforce permissions. Then select the correct connection when setting up each table's actions.

For guidance on creating a Salesforce integration user with scoped access, see [Creating a restricted Salesforce user](https://university.clay.com/docs/creating-a-restricted-salesforce-user).

## What Salesforce license type is required to connect Clay?

The license requirement depends on which connection method you use:

-   **User Sign In (OAuth):** Requires a **full Salesforce user license**. Salesforce Integration User licenses and API-only licenses cannot complete the browser-based OAuth approval flow that User Sign In requires. Attempting to connect with one of these license types results in an `OAUTH_APPROVAL_ERROR_GENERIC` error.
-   **Client Credentials:** Works with **Salesforce Integration User licenses and API-only licenses**. Because Client Credentials connects server-to-server without a browser login, it is not subject to the same OAuth flow restriction.

If your org uses a dedicated integration or service account with an API-only or Integration User license, use the **Client Credentials** method. For setup instructions, see [Connecting to Salesforce](https://university.clay.com/docs/salesforce-integration-overview).

## How do I verify which Salesforce user is associated with my connection?

Once you've tested a Salesforce connection, Clay saves the result and displays the connected SFDC user and Salesforce org directly in the connections list — so you can see which account each connection belongs to at a glance without re-testing.

To populate the connections list display (or to re-verify a connection):

1.  In the home sidebar, click `Settings` → `Connections`.
2.  Select `Salesforce`.
3.  Find the connection you want to verify and click the `…` menu next to it.
4.  Select `Test Connection`.

The test confirms the connection is valid and shows the SFDC user's email address and the Salesforce org it is attributed to. Clay saves this information to the connection, and it appears in the connections list going forward. If you see the wrong user, reconnect using the correct Salesforce account.

## How do I change or delete the default Salesforce connection?

**Changing the default:** Setting a connection as default is a **workspace admin–only** action — non-admin workspace members do not see the **Set as default** option in the `…` menu. To update the default, ask a workspace admin to change it in `Settings` → `Connections`, or have an admin update your user role. For details on connection management permissions, see [Connections and integration accounts](./connections-and-integration-accounts.md).

**Deleting the default connection:** You can delete a connection that is currently set as default. When you do, Clay automatically reassigns the default to the next available Salesforce connection. If no other connection exists, the default is cleared. Note that deleting any connection requires you to be either the person who originally added it or a workspace admin — you cannot delete a connection added by someone else unless you are an admin.

**What changing the default affects:** Setting a new default applies only to Salesforce columns you create after making the change. Existing columns and workflows continue to use the connection they were originally configured with — changing the default does not update them. To have all existing columns switch to a different Salesforce account, use **Reconnect** on the connection those columns already reference: this updates the credentials in place, so every column referencing that connection picks up the new account on its next run. See [Connections and integration accounts](./connections-and-integration-accounts.md) for the full reconnect walkthrough.

## Why is a Salesforce object (such as Account) not appearing in Clay?

The objects available in Clay are determined entirely by the permissions of the Salesforce user whose credentials were used to authenticate the integration. Clay queries Salesforce's API for the full list of accessible objects — it does not maintain its own allowlist or blocklist. If an object like Account is missing from the dropdown, it means the connected Salesforce user does not have access to it in Salesforce.

**Things to check on the Salesforce side:**

-   **Object-level permissions:** Does the connected user's profile or permission set include **Read** access to the Account object? In Salesforce, go to `Setup` → `Profiles` (or `Permission Sets`) → find the user's profile → `Object Settings` → `Account` → confirm `Read` is enabled.
-   **Org-wide sharing defaults:** Are there sharing rules that restrict Account visibility for this user? Go to `Setup` → `Sharing Settings` and check the organization-wide default for Accounts.
-   **API access per object:** Some Salesforce orgs restrict which objects are accessible via the API. Confirm the Account object is API-accessible for the connected user.

Once your Salesforce admin grants the necessary permissions, the updated access will be reflected in Clay automatically. You can verify by logging into Salesforce as the connected user and confirming Account records are visible there.

For guidance on setting up an integration user with the right object access, see [Creating a restricted Salesforce user](https://university.clay.com/docs/creating-a-restricted-salesforce-user).

## Why is a Salesforce field not appearing in the Lookup Record field picker?

If a specific field is visible in Salesforce but missing from Clay's Lookup Record dropdown, the most common reason is the field's **data type**. Clay populates the Lookup Record field picker by calling Salesforce's `describeSObject` API and filtering to fields that are both string-typed (text, picklist, email, URL, etc.) and marked as **filterable** by Salesforce — meaning they can be used in a SOQL `WHERE` clause.

Fields that Salesforce marks as non-filterable — most notably **Long Text Area**, **Rich Text Area**, and **Encrypted Text** fields — do not appear in the Lookup Record dropdown. This is a Salesforce restriction: these field types cannot be used as filter criteria in queries, so Clay cannot use them to look up records.

**Permissions are not the issue** if the field is visible to your Salesforce users but still absent from the Clay dropdown. Field-type filtering is applied on top of access checks.

**Workaround**

To use a Long Text Area (or other non-filterable) field as a lookup key in Clay, store a copy of the value in a filterable field type:

1.  In Salesforce, create a new **Text** field on the same object.
2.  Populate the new Text field with the same value using a Salesforce Flow or a formula field.
3.  In Clay, use the new Text field as your Lookup Record match field.

Once the value is in a filterable Text field, it will appear in the Clay Lookup Record dropdown and can be used as a match key.

## Why are some Salesforce fields missing from the Object Field(s) selector in the Lookup Record action?

If a Salesforce field is visible in your Salesforce UI but doesn't appear in the **Object Field(s)** list in Clay's Lookup Record action — the list of fields you can select to *return* from the lookup — the most common cause is **field-level security (FLS)**.

Clay populates the Object Field(s) list by calling Salesforce's object describe API with the connected Salesforce user's credentials. Salesforce's describe API respects FLS: fields that the connected user does not have **Read** access to are not returned, so they never appear as selectable options in Clay. This is distinct from the [search-field picker issue above](#why-is-a-salesforce-field-not-appearing-in-the-lookup-record-field-picker), which is a data-type restriction; the Object Field(s) selector is filtered by what the connected user can actually access.

**How to fix it:**

1. **Update field-level security in Salesforce.** Ask a Salesforce admin to go to `Setup` → `Profiles` (or `Permission Sets`) → find the profile or permission set assigned to the connected Salesforce user → `Object Settings` → select the relevant object (for example, `Contact`) → `Field Permissions`. Enable **Read** access for each field that should appear in Clay.
2. **Refresh the field list in Clay.** After the permission change is saved, open the Lookup Record column in your Clay table and click **Refresh fields**. This re-fetches the object's field definitions from Salesforce and adds the newly accessible fields to the Object Field(s) selector.
3. **Add the fields to your lookup.** Once the fields appear in the **Object Field(s)** dropdown, select each one you want returned. Fields not added here are not returned by the lookup, even if the connected user now has access to them.

**To confirm which Salesforce user your connection is authenticated as**, go to `Settings` → `Connections` → `Salesforce`, click `…` next to your connection, and select `Test Connection`. Clay displays that user's email address — confirm the user has the correct FLS permissions for the fields you need.

## Why are some Salesforce fields missing from the Map fields panel in the Update Record or Create Record action?

If a Salesforce field exists in your org but doesn't appear when you click **+ Add field** in the **Map fields** panel of an Update Record or Create Record action, the most common cause is **field-level security (FLS)**.

Clay populates the Map fields picker by calling Salesforce's object describe API with the connected Salesforce user's credentials. Salesforce's describe API respects FLS: fields that the connected user does not have **Edit** access to (for Update Record) or **Create** access to (for Create Record) are excluded from the response and never appear as options in Clay. Unlike the Object Field(s) selector in the Lookup Record action — which only requires **Read** access — the Map fields panel for write actions requires the appropriate write permission on each field.

**How to fix it:**

1. **Update field-level security in Salesforce.** Ask a Salesforce admin to go to `Setup` → `Profiles` (or `Permission Sets`) → find the profile or permission set assigned to the connected Salesforce user → `Object Settings` → select the relevant object (for example, `Lead`) → `Field Permissions`. Enable **Read** and **Edit** access for each field that should appear in the Map fields panel.
2. **Refresh the field list in Clay.** After the permission change is saved, open the Update Record or Create Record column in your Clay table, scroll to the **Map fields** section, and click **Refresh**. This re-fetches the object's field definitions from Salesforce and adds the newly accessible fields to the picker. The same refresh is also needed when fields were recently created in your Salesforce org — Clay works from a cached copy of field definitions and does not pick up new fields automatically.

**To confirm which Salesforce user your connection is authenticated as**, go to `Settings` → `Connections` → `Salesforce`, click `…` next to your connection, and select `Test Connection`. Clay displays that user's email address — confirm the user has the correct FLS permissions for the fields you need.

## Why does the Lookup Record action return a maximum of 5 results?

The standard **Lookup Record** action returns a maximum of 5 records per run. This is by design — it is optimized for finding a single matching record and returns up to 5 results when multiple matches exist.

If you need to retrieve all contacts (or other records) linked to a specific account — for example, when your CRM has 20 or more contacts per account — use the **Lookup Records via SOQL** action instead. With SOQL you control how many results are returned via your own `LIMIT` clause, or omit it to return all matches:

```sql
SELECT Id, FirstName, LastName, Email, Title
FROM Contact
WHERE AccountId = '/Account ID'
```

Replace `/Account ID` with the relevant column from your Clay table using the `/` picker in the query editor. You can use an AI assistant to help write the query — for example: "write a SOQL query to return all contacts for a given Salesforce account ID." For SOQL syntax reference, see [Salesforce SOQL](salesforce-soql.md).

## Why does the Lookup Record action return "Error: Bad Request"?

The standard **Lookup record** action uses `FIELDS(ALL)` to fetch every field from the matched Salesforce record. If the object's schema contains more than 15 fields that reference related objects — such as owner, parent account, engagement manager, or other relationship fields — Salesforce rejects the query with a 400 error, which appears in Clay as **"Error: Bad Request"**.

This is a Salesforce constraint: a single SOQL query can reference at most 15 cross-object fields. The error occurs regardless of which field you are searching on, and before any matching logic runs.

**Fix:** Switch to the **Lookup records via SOQL** action and explicitly select only the fields you need:

```sql
SELECT Id, Name, Website
FROM Account
WHERE Name LIKE '%/Company Name%'
LIMIT 5
```

By requesting only the fields you actually use, the query stays under the 15-reference limit and the error goes away. For tips on writing SOQL queries in Clay, see the [Lookup records via SOQL](salesforce-integration-overview.md) section of the Salesforce integration overview.

## Why is my Lookup Records via SOQL action returning "Invalid SOQL Query" for some rows?

If only certain rows fail with **"Invalid SOQL Query. Please check your query syntax and try again."** while others succeed, the most likely cause is **special characters in the input value** for those rows. Two characters that commonly appear in company names and break SOQL string literals are:

-   **Apostrophes (`'`)** — a company name like `Peterson's Nuts` contains an apostrophe that Salesforce interprets as the end of the string literal, making the rest of the query invalid.
-   **Pipe characters (`|`)** — these can cause Clay's query substitution to produce a malformed SOQL string.

**Fix:** Add a formula column that cleans the input value before passing it to the SOQL query, then use that cleaned column in your query instead of the raw column. For example:

```javascript
#{{Company Name}}.replace(/'/g, "\\'").replace(/\|/g, "")
```

Only rows with those characters in the matched column will fail — rows with clean values run normally.

## How do I look up activity records (Tasks or Events) for a Salesforce contact?

In Salesforce, activity records — Tasks and Events — are stored as separate objects, not directly on the Contact record. Because of this, the standard **Lookup Record** action (which retrieves the Contact object) won't return a contact's activities. You need to query the Task or Event object directly.

Use the **Lookup records via SOQL** action and filter on the `WhoId` field, which links each Task or Event to its associated contact or lead.

**For Tasks (calls, to-dos, logged emails):**

```sql
SELECT Id, Subject, ActivityDate, Status, Description
FROM Task
WHERE WhoId = '/Salesforce Contact ID'
```

**For Events (meetings, appointments):**

```sql
SELECT Id, Subject, ActivityDate, StartDateTime, EndDateTime, Description
FROM Event
WHERE WhoId = '/Salesforce Contact ID'
```

Replace `/Salesforce Contact ID` with the contact's Salesforce ID column from your Clay table, inserted using the `/` picker in the query editor.

**Tips:**

-   **Select only the fields you need.** Fetching fewer fields keeps queries fast and avoids hitting Salesforce's response-size limits.
-   **Add a `LIMIT` clause** to control how many activity records are returned per contact row (for example, `LIMIT 10`).
-   **Sort by most recent first** using `ORDER BY ActivityDate DESC` so the newest activities appear at the top of the result.
-   **Run two separate SOQL columns** if you need both Tasks and Events — one column querying `Task` and one querying `Event` — then use a formula column to combine or compare the results.

For SOQL syntax reference, see Salesforce's [SOQL documentation](https://developer.salesforce.com/docs/atlas.en-us.soql_sosl.meta/soql_sosl/sforce_api_calls_soql.htm) or the [Lookup records via SOQL](salesforce-integration-overview.md) section of the Salesforce integration overview.

## Why does a Salesforce Lookup return "no records found" when searching by phone number?

If the column holding phone numbers is set to **Number** type, Clay alters the value before passing it to Salesforce. A phone number in plain E.164 format — for example, `+12345678900` — stored in a Number column loses its leading `+`, becoming `12345678900`. If Salesforce stores the number as `+12345678900`, the lookup finds no match. Phone numbers that contain spaces or dashes (for example, `+1 234-567-8900`) produce a coercion error in the cell rather than a silently altered value.

**To fix:** Click the phone number column header, hover over the current data type, and switch it to **Text**. Text columns preserve the exact phone number string — including the leading `+` and any separators — so the value Clay sends to Salesforce matches what Salesforce has stored.

## Why is my Salesforce report data not populating in Clay?

The most likely cause is the report's format. Clay's **Import records from a Salesforce report** source only supports **Tabular** and **Matrix** report formats. Reports in **Summary** or **Joined** format are not supported and will return an error when Clay tries to run them.

Clay's report picker automatically filters to show only Tabular and Matrix reports, so if a report is missing from the picker, it is likely in an unsupported format.

**To fix:** In Salesforce, open the report, click **Edit**, then change the report format to **Tabular** (a flat list without row groupings) or **Matrix** (rows and columns both grouped). Save the report, then re-run your Clay source.

For an overview of Salesforce report formats, see Salesforce's [Report Formats documentation](https://trailhead.salesforce.com/content/learn/modules/lex_implementation_reports_dashboards/lex_implementation_reports_dashboards_report_formats).

## Why did my Salesforce report import only bring in 2,000 rows when my report has more?

This is expected behavior. The Salesforce Analytics API caps the number of records returned when running a report at **2,000 rows**. Clay's **Import records from a Salesforce report** source fetches a single page of results from this API — if your report contains more than 2,000 records, only the first 2,000 are imported into Clay. This is a Salesforce API restriction, not a Clay bug.

**To import more than 2,000 records from Salesforce, use one of these alternatives:**

- **Salesforce List source (recommended):** Create a Salesforce list view that matches your report criteria and use Clay's **Import records from a Salesforce list** source instead. SOQL-compatible list views support up to 50,000 records per import. See the [Salesforce integration overview](salesforce-integration-overview.md) for setup steps.
- **Salesforce SOQL source:** Write a custom SOQL query that pulls the exact records you need. The SOQL source also supports up to 50,000 records per import and gives you full control over filtering and field selection. See [Salesforce SOQL](salesforce-soql.md) for details.

## Why did my scheduled "Import records from a Salesforce list" stop running?

The most common cause is that the source reached the 50,000 total records processed limit. Each "Import records from a Salesforce list" source tracks the cumulative number of records it has ever pulled over its entire lifetime — not the number of rows currently visible in the table. Once that running total reaches 50,000, scheduled refreshes stop importing new records, even if the table appears to have space.

**Why auto-delete does not prevent this.** If auto-delete is enabled and you see the banner "Auto-delete is on with a source that isn't compatible," the source's processed-record counter is still accumulating even as deleted rows are cleared from the table. Deleting rows from the table — whether by auto-delete or manually — does not reset the source's processed count. The table may show far fewer than 50,000 visible rows while the source has already reached the 50,000 lifetime limit.

**Options to continue importing records:**

- **Audiences with bulk enrichment (recommended for ongoing syncs).** Import your Salesforce records into a Clay Audience and run bulk enrichment on a schedule. Audiences are not subject to the 50,000-record source limit. For details, see [Audiences](audiences.md).
- **Webhook source.** If you can configure Salesforce to push record changes to Clay via a webhook — for example, using a Salesforce Flow that triggers a callout when a record is saved — webhook sources do not accumulate toward the 50,000-record limit when auto-delete is enabled. This works well for event-driven workflows where Salesforce fires updates as they happen.
- **Create a new source.** Deleting the existing source and adding a new "Import records from a Salesforce list" source on the same table resets the processed-record counter to zero, giving you a fresh 50,000 records. This is a short-term workaround — the new source will eventually reach the limit again as it processes records.

For a full explanation of which source types are compatible with auto-delete's continuous passthrough mode, see [Auto-delete in tables](auto-delete.md).

## Will Clay create duplicate records in Salesforce?

Clay does not create duplicate records by default. However, you can allow duplicates by enabling the "Duplicate Rule Override" in the Create Record enrichment.

To avoid creating duplicates from your Clay table, first look up an object to check if it exists, then create it only if it doesn't. Here's how to set that up:

1.  Add a **Lookup record** (or **Lookup records via SOQL**) column to find the existing record in Salesforce using a unique identifier such as email address or record ID.
2.  Add a **Create record** column for the object you want to create.
3.  In the **Create record** column settings, open **Run settings** and add a conditional run. Set the condition to check that the ID field returned by your lookup column is empty. Clay will only run Create record on rows where no existing match was found — rows that don't meet the condition are skipped and consume no credits.

For full details on writing run conditions, see [Conditional runs](https://university.clay.com/docs/conditional-runs).

[Learn more about Salesforce's duplicate rules here.](https://help.salesforce.com/s/articleView?id=sales.duplicate_rules_map_of_reference.htm&type=5)

## Why am I seeing a `DUPLICATES_DETECTED` error when creating records in Salesforce?

This error means Salesforce has an active duplicate rule that detected an existing record matching the one Clay tried to create. The rule fired during the Create Record action and returned an error rather than letting the save proceed.

There are three ways to handle this:

**Option 1: Enable Duplicate Rule Override in Clay**

If your Salesforce duplicate rule is configured to "allow save" (it warns about duplicates rather than hard-blocking them), you can tell Clay to proceed with the save anyway. In your **Create Record** column settings, enable the **Duplicate Rule Override** toggle. Clay will then bypass the duplicate warning and create the record even when Salesforce detects a match.

**Option 2: Look up first, then update instead of create**

Rather than creating a record that already exists, look it up and update it instead:

1.  Add a **Lookup record** column before your Create Record column. Search by a unique identifier such as email address.
2.  In your **Create record** column, open **Run settings** and add a conditional run that fires only when the lookup returns no result (the ID field is empty). This means only genuinely new records get created.
3.  Add an **Update record** column with a conditional run that fires only when the lookup returns a result (the ID field is not empty). Set **Record ID** to the ID returned by your lookup column.

This way, new records are created and existing records are updated — without either action running into a duplicate conflict.

**Option 3: Adjust the Salesforce duplicate rule**

On the Salesforce side, modify the duplicate rule to exclude records coming from Clay's integration user. For example, add a condition such as "Current User not equal to \[the Salesforce user Clay authenticates as\]". This prevents the rule from firing when Clay creates records, while still protecting your org from duplicates created by other users.

For details on Clay's Create Record settings, see [Salesforce integration](https://university.clay.com/docs/salesforce-integration-overview). For more on Salesforce duplicate rules, see [Salesforce's documentation](https://help.salesforce.com/s/articleView?id=sales.duplicate_rules_map_of_reference.htm&type=5).

## Why am I seeing a `MALFORMED_ID` error when creating or updating a Salesforce record?

The `MALFORMED_ID` error means Salesforce received a value it cannot interpret as a valid record ID for a reference (lookup) field — such as **OwnerId**, **AccountId**, **ContactId**, or **CampaignId**. Reference fields require the actual Salesforce record ID (an 18-character alphanumeric string, for example `005Pk000008CnYDIA0`), not a display name or label. Passing a person's name — for example, `Matt Bagshaw` — to the **OwnerId** field causes Salesforce to return a `MALFORMED_ID` error, which Clay surfaces as-is.

Clay does not transform field values before sending them to Salesforce — whatever value is in your Clay column is passed directly to the Salesforce API.

**To fix this**, add a **Lookup Record** step before your Create or Update Record action to retrieve the actual Salesforce ID:

1.  **Add a Lookup Record column.** Set the Salesforce object to the type that corresponds to the reference field — for example, **User** for **OwnerId**, **Account** for **AccountId**, or **Contact** for **ContactId**.
2.  **Search by the identifier you have.** Use the person's name, email address, or another field available in your Clay table. Enable **Exact match** to avoid partial-name collisions.
3.  **Map the returned ID into the reference field.** In your **Create Record** or **Update Record** column's **Map fields** section, reference the `Id` field from your Lookup Record result and map it to the reference field (for example, **Owner ID**).

The same fix applies to any reference field that returns a `MALFORMED_ID` error — not just **OwnerId**.

## How do I prevent Salesforce records from being created or updated when there is no valid email?

Use conditional runs on your **Create Record** and **Update Record** action columns to gate them on a passing email validation result. Rows where email validation fails are skipped automatically and do not consume credits.

Here's how to set it up:

1.  Ensure your table has an email validation enrichment column (for example, Clay's built-in **Validate Email** enrichment or a third-party email validator). This column produces a status or result value for each row.
2.  On your **Create Record** column, open **Run settings** and add a conditional run. Set the condition to only run when the email validation column indicates a valid email — for example, `/Email Validation Status is "valid"` or `/Validate Email is not empty`, depending on what your validation enrichment outputs.
3.  Repeat the same conditional run configuration on any **Update Record** columns that should also be skipped when email validation fails.

Rows where the condition is not met show **"Run condition not met"** in the column cell — no Salesforce record is created or updated, and no credits are consumed for those rows.

For full details on writing run conditions, see [Conditional runs](https://university.clay.com/docs/conditional-runs).

## How do I prevent contacts from being pushed to Salesforce when required fields like Account Name or Title are blank?

Gate your Salesforce write so only complete records reach Salesforce. There are two approaches:

**Option 1: Add an "Only run if" condition on the Salesforce action column (all plans)**

Add a run condition to your **Create Record** or **Update Record** action column so it fires only when all required fields are populated.

1.  Open the column settings for your Salesforce **Create Record** or **Update Record** column.
2.  Click **Run settings** → **Only run if**.
3.  In the formula field, enter a condition that checks all required fields. For example, to require both Account Name and Title:

    `/Account Name is not empty AND /Title is not empty`

4.  Click **Generate formula**, verify the preview, then save.

Rows where any required field is blank are skipped and shown as **"Run condition not met"** — no Salesforce record is created or updated, and no credits are consumed for those rows. Repeat this configuration on every Salesforce action column that should respect the same requirement.

For full details on writing run conditions, including combining multiple conditions with AND and OR, see [Conditional runs](https://university.clay.com/docs/conditional-runs).

**Option 2: Filter your Audiences segment before syncing (Growth and Enterprise plans)**

If you're using [Clay Audiences](audiences.md), create a segment filtered to only complete records and sync that segment to Salesforce — records missing required fields are excluded from the sync entirely.

1.  In Audiences, open or create a segment under **People** or **Companies**.
2.  Add a filter for each required field — for example, **Account Name → is not empty** — then add a second filter for **Title → is not empty**. Multiple top-level filters are joined with AND, so only records where all required fields are populated will match.
3.  Sync this filtered segment to Salesforce. Records that don't match the filters stay in Audiences but are never written to Salesforce.

This gives you a single place to manage field-completeness rules across your workspace, rather than maintaining run conditions in each table. Note that syncing an Audiences segment to Salesforce requires a **Growth or Enterprise** plan.

## How do I add leads or contacts to a Salesforce campaign and update the status of existing campaign members?

A Campaign Member in Salesforce represents the relationship between a lead or contact and a campaign. Each Campaign Member record is tied to either a `LeadId` or a `ContactId` — not both at once. Because leads or contacts might already be members of the campaign, you need a conditional workflow that handles both cases — adding new members and updating the status of existing ones.

**Recommended workflow:**

1.  **Lookup records via SOQL** — Check whether the lead or contact is already a campaign member. Using SOQL lets you filter on both the person ID and `CampaignId` at once.

    *For contacts:*
    ```sql
    SELECT Id, Status FROM CampaignMember WHERE ContactId = '/Contact ID' AND CampaignId = '/Campaign ID' LIMIT 1
    ```

    *For leads:*
    ```sql
    SELECT Id, Status FROM CampaignMember WHERE LeadId = '/Lead ID' AND CampaignId = '/Campaign ID' LIMIT 1
    ```

    *If your table contains a mix of leads and contacts, create a formula column (call it something like "Person ID") that returns the Contact ID when populated and falls back to the Lead ID otherwise. Then use an OR query to handle both in a single lookup:*
    ```sql
    SELECT Id, CampaignId, LeadId, ContactId, Status
    FROM CampaignMember
    WHERE CampaignId = '/Campaign ID'
    AND (LeadId = '/Person ID' OR ContactId = '/Person ID')
    LIMIT 1
    ```

    Replace the `/Column Name` placeholders with your Clay columns using the `/` picker in the query editor. This returns the Campaign Member's `Id` and current `Status` if they are already in the campaign, or nothing if they are not.

2.  **Create record (conditional)** — If the lookup returns no result, the person is not yet in the campaign. Add a **Create record** column, set the Salesforce object to `CampaignMember`, and supply `ContactId` (or `LeadId`), `CampaignId`, and the initial `Status`. In **Run settings**, add a conditional run that fires only when the ID field from your SOQL lookup is empty.

3.  **Update record (conditional)** — If the lookup returns a result, the person is already in the campaign and needs their status changed. Add an **Update record** column, set the Salesforce object to `CampaignMember`, set **Record ID** to the `Id` from your SOQL lookup column, and supply the new `Status` value. In **Run settings**, add a conditional run that fires only when the ID field from your SOQL lookup is **not** empty.

For step-by-step instructions and SOQL query examples, see [How do I add leads or contacts to a Salesforce campaign and update the status of existing campaign members?](salesforce-integration-faqs.md) in the Salesforce integration FAQs. That workflow also covers how to update the status of existing campaign members in the same pass.

## What are the default sync settings for CRM integrations?

**How autoupdate works**

By default, Clay does not automatically update rows in a table when a Salesforce source refreshes. When the source re-syncs, new records are added to the table, but existing rows are not automatically re-enriched.

**How do I turn on or off autoupdate?**

1.  While in a Clay table, click the three-dot menu at the top right.
2.  Click on `Table settings`.
3.  Look for `Autoupdate settings` or a similar option in the menu.
4.  Toggle the autoupdate setting on or off as needed.

If autoupdate is enabled, Clay will automatically re-enrich rows when the source updates with new data.

## How can I reduce the Salesforce CPU utilization caused by Clay's queries?

If you see Salesforce CPU time errors or want to prevent Clay's API calls from consuming too much server CPU, there are two approaches:

-   **Use indexes on filter fields.** Make sure the fields you use in `WHERE` clauses in your SOQL queries (for example, email, domain, or LinkedIn URL) are indexed in Salesforce. Salesforce standard fields like `Id`, `Email`, and `CreatedDate` are indexed by default. For custom fields, you may need to enable the **External ID** or **Unique** flag to trigger indexing (these settings can be found in Salesforce Setup → Object Manager → your object → Fields & Relationships → your field → Field Properties).
-   **Add `LIMIT` to your SOQL queries.** Including a `LIMIT` clause prevents the query from scanning too many rows at once. For example, `SELECT Id, Name FROM Contact WHERE Email = '/Email' LIMIT 1` keeps the query focused and reduces CPU time.

Both measures together significantly reduce per-query CPU overhead. If you are still seeing CPU limit errors, contact your Salesforce admin to review query plans or consider moving high-volume lookups to an asynchronous pattern.

## Why does enriching a Salesforce timestamp field cause records to keep re-running?

If you're enriching a Salesforce field that stores a timestamp — for example, `LastActivityDate` or a custom `Last Enriched` date field — and you notice that records keep re-triggering even after they've already been processed, the most likely cause is a circular dependency between the enrichment and the field it's writing to.

Here's what happens:

1.  Clay enriches a Salesforce record and writes to the timestamp field (for example, `LastActivityDate`).
2.  Salesforce updates the record's `SystemModstamp` — the field it uses to track when a record was last modified.
3.  Clay's incremental sync picks up records whose `SystemModstamp` has changed since the last sync.
4.  The record that Clay just enriched is now included in the next sync as a "changed" record.
5.  Clay re-enriches it, updates `SystemModstamp` again, and the cycle repeats.

This loop is a known side effect of enriching any Salesforce field that triggers a `SystemModstamp` update. It is not a bug — it reflects how Salesforce's change-tracking works.

**How to stop the loop:**

The most reliable fix is to use a **run condition** ("Only run if") on your enrichment column to gate the enrichment on a condition that can only be true once — for example, requiring the timestamp field to be empty before running. Set the condition to `/Last Enriched is empty`. This ensures the enrichment fires for a record only when the field hasn't been written yet, and skips records that have already been processed.

**Note:** The loop only occurs when you are writing to a field that affects `SystemModstamp`. Read-only lookups and enrichments that do not write back to Salesforce do not trigger this behavior.

The same risk applies to any custom "last enriched" timestamp field that Clay itself populates. If that field is also used as a trigger or input for the same enrichment, the enrichment will keep re-running after every update.

## Is there a way I can test Salesforce enrichments?

Yes! The easiest option is running enrichments on a single row. Here's how to test a Salesforce enrichment:

1.  Create a new Clay table and add a few test contacts.
2.  Add a Salesforce enrichment column (e.g., Create Record or Update Record).
3.  Click on a single cell in the Salesforce column.
4.  You'll see a "Run" button appear.
5.  Click "Run" to test the enrichment for just that one row.

This lets you verify that your Salesforce enrichment is working correctly before running it on all your data.

## Can I reverse my Salesforce enrichment?

Yes. You can reverse a Salesforce enrichment by following these steps:

1.  Add a new column to the table you want to reverse.
2.  Set it up using the same Salesforce action (Create Record or Update Record) with the same field mappings.
3.  For the values you want to clear, leave the field blank in the Map fields section to write an empty value.
4.  Run this column to overwrite the existing Salesforce data with the blank values.

Note: This won't actually delete the Salesforce records — it will just clear or overwrite the specific fields you mapped.

## Do we need to create a custom Salesforce object to integrate Salesforce data?

No! Salesforce already has standard objects like Contacts, Leads, Accounts, Opportunities, and more. Clay can read from and write to these standard objects directly.

If you have data that doesn't fit into standard Salesforce objects, you may need a custom object. But for most cases, the standard Salesforce objects should be sufficient.

## Can I use a Salesforce API-only or Integration User license with Clay?

Yes, but only via the **Client Credentials** connection method. Salesforce Integration User licenses and API-only licenses cannot complete the browser-based OAuth flow required by the **User Sign In** method — attempting to use one results in an `OAUTH_APPROVAL_ERROR_GENERIC` error.

For setup instructions, see [Connecting to Salesforce](https://university.clay.com/docs/salesforce-integration-overview).

## Why am I seeing an "OAUTH\_APPROVAL\_ERROR\_GENERIC" error when connecting Salesforce?

This error appears during the OAuth sign-in flow. Common causes:

**Integration User or API-Only license**

Integration User and API-Only licenses cannot complete the browser-based OAuth approval screen. Switch to either:

-   A full Salesforce user license for **User Sign In**, or
-   The **Client Credentials** method, which works with integration and API-Only licenses.

**Connected app not pre-approved or not installed**

Since Salesforce's August 2025 security policy update, all Connected Apps — including Clay's — must be pre-installed in your Salesforce org before users can authenticate. If Clay is not installed, Salesforce blocks the OAuth flow with this error.

See [Do I need to install Clay's Connected App in my Salesforce org?](#do-i-need-to-install-clays-connected-app-in-my-salesforce-org) below for installation instructions.

**Other causes**

-   **SSO enforcement:** The user's profile enforces SSO, which blocks the standard OAuth approval screen. Try with a non-SSO user or create a non-SSO service account.
-   **Missing permission:** The user's profile lacks the "Approve uninstalled connected apps" permission. Ask a Salesforce admin to grant it, or connect with a System Administrator account.

## Do I need to install Clay's Connected App in my Salesforce org?

Yes. Since Salesforce's August 2025 security policy update, all Connected Apps — including Clay's — must be pre-installed in your org before users can authenticate. If Clay is not installed, Salesforce blocks the OAuth flow with an `OAUTH_APPROVAL_ERROR_GENERIC` error.

**How to install Clay's Connected App:**

Go to this Salesforce AppExchange listing and install it: [Clay for Salesforce](https://appexchange.salesforce.com/appxListingDetail?listingId=a0N4V00000GZGIiUAP)

Once installed, return to Clay and reconnect your Salesforce account. The OAuth flow should complete successfully.

## Why doesn't the Clay connected app appear under "Connected Apps OAuth Usage"?

If you don't see Clay listed under `Setup` → `Connected Apps OAuth Usage`, the most common cause is that **no user has successfully completed the OAuth flow yet**. Salesforce only adds a connected app to this list after at least one user has authenticated through it.

**Other potential causes:**

-   **The app isn't installed yet.** Clay's connected app must be pre-installed in your org (see above). If it hasn't been installed, it won't appear.
-   **The user's profile lacks the "Approve uninstalled connected apps" permission** (required when the app isn't pre-installed).
-   **Org policies block uninstalled connected apps entirely** (via App Access Control).

**How to fix:**

1.  Install Clay's connected app if it isn't already (see above).
2.  Try authorizing with a System Administrator user first—this lifts the "uninstalled" status and populates Connected Apps OAuth Usage.
3.  In `Setup` → `Connected Apps OAuth Usage`, verify the Clay app is listed and not blocked. If your org uses App Access Control, pre-install or whitelist the app first.

## What callback URL does Clay use for Salesforce?

Clay uses `https://app.clay.com/integrations/salesforce` as its OAuth callback URL. This is the URL Salesforce redirects to after the user approves the OAuth connection.

If your Salesforce org restricts which callback URLs are allowed for connected apps, you may need to add this URL to your allowlist. Check with your Salesforce admin if you're unsure whether callback URL restrictions are in place.

## What OAuth scopes does Clay require for Salesforce?

Clay's Salesforce connected app requests the following OAuth scopes:

1.  **Access the identity URL service** (`id, profile, email, address, phone`) — used to identify the authenticated user and retrieve their profile information.
2.  **Manage user data via APIs** (`api`) — required to read from and write to Salesforce objects using the REST and SOAP APIs.
3.  **Perform requests at any time** (`refresh_token, offline_access`) — allows Clay to refresh access tokens so the connection remains active without requiring re-authentication.

These scopes are the minimum required for Clay to function. Clay does not request scopes beyond these three.

## Do I need to adjust IP or session restrictions in Salesforce to connect Clay?

On **Enterprise plans**, all Salesforce connections in Clay automatically route through Clay's static IP addresses — no toggle or configuration is needed. If your Salesforce org restricts connections by IP address, contact Clay support to request the current IP list, then allowlist them in Salesforce under `Setup` → `Network Access` → `New`.

For full instructions on setting up a restricted Salesforce user with field-level security and IP allowlisting, see [Creating a restricted Salesforce user](https://university.clay.com/docs/creating-a-restricted-salesforce-user).

**Trusted IP Ranges for connected apps**

If your Salesforce org uses Trusted IP Ranges at the connected app level (not the org-wide `Network Access` level), you may need to configure the connected app separately. Go to `Setup` → `App Manager` (or `External Client App Manager`) → find the Clay connected app → click `Edit` → scroll to `IP Relaxation`. Set this to `Relax IP Restrictions`. This ensures users can authorize Clay regardless of their location and the IP filtering is handled at the org-wide Network Access level instead.

**Session security**

Clay's API tokens are long-lived by design (see OAuth scopes above). If your Salesforce org has session timeout settings that revoke tokens aggressively (for example, a 2-hour session timeout), Clay connections may drop unexpectedly. Set the session timeout to a longer value for the connected app, or exempt the Clay integration user from aggressive session policies.

## Why did the owner on my Salesforce record change when Clay updated a field?

Salesforce has a feature called **lead assignment rules** that can reassign a record's owner automatically when certain fields are updated — including updates made by Clay. If you notice that the **Owner** field changed on a lead or contact after Clay updated it, a Salesforce assignment rule is likely the cause.

Assignment rules fire by default whenever a record is created or updated through the API, including Clay's integrations. Clay does not trigger assignment rules intentionally — they are triggered by Salesforce based on the fields Clay writes to and how your org's rules are configured.

**How to prevent assignment rules from firing:**

In Clay's **Update Record** column settings, enable the **Disable auto-assignment rules** toggle. When this is on, Clay passes a flag to the Salesforce API that tells it to skip assignment rules for that update. This is the recommended fix when you want Clay to update fields without changing the record owner.

For the **Create Record** action, Clay does not currently expose a disable-assignment-rules toggle. If Clay is creating new records and you don't want assignment rules to fire, the options are:

1.  Modify the Salesforce assignment rule to exclude records where the owner is the Clay integration user.
2.  After the create, add an **Update Record** column with **Disable auto-assignment rules** enabled to reassign the owner back to the intended value.

## Why is the owner on a new Salesforce lead or contact set to the Clay integration user?

When Clay creates a Salesforce record using the **Create Record** action, Salesforce automatically sets the **Owner** to the user whose credentials are used to authenticate the connection. If you connected Clay using a dedicated integration user or a service account, that user becomes the owner of every record Clay creates.

This is standard Salesforce behavior — the API sets the record owner to the authenticated user unless the request explicitly specifies a different owner.

**To set a specific owner when creating records:**

In your **Create Record** column settings, open **Map fields** and add the **OwnerId** field. Map it to the Salesforce User ID of the person who should own the record. You can look up this ID using a **Lookup Record** column (Salesforce object: **User**, search field: **Name** or **Email**), or retrieve it from your import data if it's already available.

**If the owner keeps reverting to the integration user after creation**, a Salesforce assignment rule may be firing after the record is created — see [Why did the owner on my Salesforce record change when Clay updated a field?](#why-did-the-owner-on-my-salesforce-record-change-when-clay-updated-a-field) for how to disable it.

## Why am I seeing an `INACTIVE_OWNER_OR_USER` error when creating records in Salesforce?

This error means the **OwnerId** value Clay is passing to Salesforce references a user who is inactive or deactivated in your Salesforce org. Salesforce does not allow new records to be created with an inactive owner.

**Common causes:**

-   A column in your Clay table contains an owner ID that was valid when the data was collected but the user has since been deactivated in Salesforce.
-   The Clay connection itself is authenticated as a deactivated user (unlikely but possible if the user was recently deactivated after the connection was set up).

**How to fix:**

1.  **Identify which rows are affected.** Open the cell details for any row showing the error — the error message may include the ID of the inactive user.
2.  **Look up the correct owner.** Add a **Lookup Record** column (Salesforce object: **User**) to find the active user who should own the record. Search by name or email, and make sure the user's status in Salesforce is **Active**.
3.  **Update the OwnerId mapping.** In your **Create Record** column's **Map fields** section, replace the current **OwnerId** value with the active user's ID returned by the lookup column.

If the error is on the connection itself — meaning Clay's authenticated integration user has been deactivated — reconnect using an active Salesforce user. Go to `Settings` → `Connections` → `Salesforce`, click `…` on the affected connection, and select **Reconnect**.

## Why am I seeing a "Retried but failed: Failed to lock row" error when updating Salesforce records?

This error means Salesforce couldn't acquire a write lock on the record during Clay's update — another process (a workflow, trigger, integration, or concurrent update) was already writing to that record at the same time. Salesforce returns a lock error rather than silently dropping one of the writes.

This is a concurrency issue, not a Clay bug. It happens when multiple processes try to update the same record simultaneously. Common triggers:

-   Clay is running updates on the same records as a Salesforce Flow, trigger, or another integration.
-   Multiple Clay columns are writing to the same record at the same time (for example, a Create Record and an Update Record both targeting the same Contact or Lead).
-   High-volume batch updates in Clay coincide with peak activity in your Salesforce org.

**How to reduce lock errors:**

-   **Serialize your Clay updates.** If you have multiple Salesforce write columns in the same table, add **run conditions** that ensure only one runs at a time per row — for example, gate the second column on the first one having completed. See [Conditional runs](https://university.clay.com/docs/conditional-runs).
-   **Reduce concurrency in Salesforce.** Work with your Salesforce admin to identify and optimize Flows or triggers that run on the same objects Clay is updating. Bulkified Flows that process records in batches cause fewer lock conflicts than row-by-row triggers.
-   **Re-run the failed rows.** Lock errors are transient — the record is only locked for the duration of the competing write. Once Clay surfaces the error, open the column, click the **Errored rows** tab, and re-run those specific rows. They usually succeed on the retry when the lock has been released.

If lock errors happen consistently across many rows, it is a sign that Clay's update volume is colliding with ongoing Salesforce automation. In that case, consider batching Clay updates during off-peak hours using the [Scheduled columns](scheduled-columns.md) feature.

## Why do records created or updated by Clay show my name (or another user's name) in Salesforce's Created By or Last Modified By field?

When Clay creates or updates Salesforce records, Salesforce stamps the **Created By** and **Last Modified By** fields with the user whose credentials are used to authenticate the Clay connection. If you connected Clay using your personal Salesforce account, Salesforce attributes all Clay activity to you — even if other team members triggered the Clay run.

This is standard Salesforce behavior. Salesforce records actions as belonging to the authenticated API user, regardless of who initiated the action in the upstream system (Clay).

**To prevent your personal name from appearing in Salesforce audit fields**, use a dedicated integration user or service account to authenticate Clay's Salesforce connection. All records Clay creates or updates will then show the integration user's name, making it easy to identify activity that originated from Clay.

For guidance on creating a scoped integration user, see [Creating a restricted Salesforce user](https://university.clay.com/docs/creating-a-restricted-salesforce-user).

## How do I connect to Salesforce as a specific user (such as an integration user) using User Sign In?

Clay authenticates as whichever Salesforce user is currently signed in to Salesforce in your browser at the time you complete the OAuth flow. To connect as a different user:

1.  Sign in to Salesforce as the user you want Clay to authenticate as (for example, your integration user or service account). If you are already signed in as a different user, sign out first — or use a private/incognito browser window to sign in as the target user without disrupting your existing session.
2.  In Clay, go to `Settings` → `Connections` and click `Add connection`. Search for Salesforce and select it.
3.  Under **User Sign In**, click `Sign in with Salesforce` (or `Sign in with Salesforce sandbox` for a sandbox org). Clay opens a Salesforce OAuth prompt in the browser.
4.  Since you're already signed in as the correct user in that browser session, Salesforce shows the approval screen for that user. Click `Allow`.
5.  Clay creates the connection and labels it with the email of the authenticated user.

After connecting, use **Test Connection** to confirm that Clay is authenticated as the intended user.

**If the user you want to connect as uses an Integration User or API-Only Salesforce license**, the User Sign In method won't work — those license types cannot complete the browser OAuth flow. Use the **Client Credentials** method instead. See [Connecting to Salesforce](https://university.clay.com/docs/salesforce-integration-overview) for setup instructions.

## Why can't I set a Salesforce connection as the default, or change which connection is the default?

Setting or changing the default Salesforce connection is a **workspace admin–only** action. If you don't see the **Set as default** option in the `…` menu for a connection, your account does not have admin permissions in this Clay workspace.

To update the default connection:

-   Ask a workspace admin to change it in `Settings` → `Connections`.
-   Or have a workspace admin update your user role to admin, then make the change yourself.

For details on which connection management actions require admin access, see [Connections and integration accounts](./connections-and-integration-accounts.md).
