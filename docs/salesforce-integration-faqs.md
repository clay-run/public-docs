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

## When creating a Salesforce contact, do I need to map Account Name in addition to Account ID?

No. Mapping the **Account ID** field in the **Map fields** panel is sufficient to associate the new contact with an account. The Account Name you see displayed in Salesforce is not a separate field to create — Salesforce derives it from the Account ID relationship and shows it as a label in the record form. Because Account Name is a read-only derived field, it does not appear as an option in Clay's **Map fields** panel and cannot be mapped directly.

To set the correct Account ID, use a **Lookup Record** column (with the **Account** object) to find the account by name, domain, or another identifier, then map the returned `Id` field to the **Account ID** field in your **Create Record** column. For a step-by-step example of retrieving a Salesforce ID for a reference field, see [Why am I seeing a `MALFORMED_ID` error when creating or updating a Salesforce record?](#why-am-i-seeing-a-malformed_id-error-when-creating-or-updating-a-salesforce-record).

## Why does Clay show "✅ Record created" but the record doesn't appear in Salesforce?

When Clay's Create Record action receives a valid record ID back from Salesforce, it marks the action as successful and displays **"✅ Record created"** with a link to the new record. Clay does not perform a follow-up check to verify the record still exists in Salesforce — so if Salesforce discards or removes the record after the initial creation response, the cell still shows success with the original URL.

If you click the URL from a successfully created cell and see **"We couldn't find the record you're trying to access"** in Salesforce, the record was created but then became inaccessible. The most common causes, in rough order of likelihood:

**1. A Salesforce automation removed the record after creation**

Clay creates the record and receives a valid Salesforce ID back — but a workflow rule, Flow, trigger, or Process Builder on the object fires on record creation and deletes or converts the record right after. Check your Salesforce automations on the object for anything that runs on creation.

**2. Required fields weren't mapped**

Salesforce may allow a record to be created in an incomplete state and then discard it if required relationship fields are missing. For Tasks specifically, the `WhoId` (the associated contact or lead) and `WhatId` (the associated account or opportunity) fields are commonly required. Confirm all required fields — including lookup relationship fields — are mapped in your **Create Record** column's **Map fields** section.

If you have a name but not the Salesforce ID for a relationship field, add a **Lookup Record** column before your Create Record step to retrieve the ID first. For a step-by-step example, see [Why am I seeing a `MALFORMED_ID` error when creating or updating a Salesforce record?](#why-am-i-seeing-a-malformed_id-error-when-creating-or-updating-a-salesforce-record).

**3. A field type mismatch**

If a mapped value doesn't match the expected Salesforce field type — for example, text sent where a boolean or lookup ID is expected — the record can fail validation after creation. Review your **Map fields** configuration for type alignment.

**4. Duplicate rules on the object**

If your Salesforce org has duplicate rules configured on the object (or related objects), those rules may be blocking or discarding the record post-creation.

**5. Integration user has write but not read access**

If the Salesforce user connected to Clay has write access but not read access to the object, the record is created successfully but appears "not found" when accessed. Confirm the integration user has full read/write access to the object in Salesforce Setup.

**To narrow it down:**

-   Search your **Salesforce Recycle Bin** — if the record was auto-deleted by an automation, it may still be recoverable there.
-   In Salesforce Setup, review active **Flows** and **triggers** on the object to see if any run on record creation.

## How do I prevent Salesforce records from being created or updated when there is no valid email?

Use conditional runs on your **Create Record** and **Update Record** action columns to gate them on a passing email validation result. Rows where email validation fails are skipped automatically and do not consume credits.

Here's how to set it up:

1.  Ensure your table has an email validation enrichment column (for example, Clay's built-in **Validate Email** enrichment or a third-party email validator). This column produces a status or result value for each row.
2.  On your **Create Record** column, open **Run settings** and add a conditional run. Set the condition to only run when the email validation column indicates a valid email — for example, `/Email Validation Status is "valid"` or `/Validate Email is not empty`, depending on what your validation enrichment outputs.
3.  Repeat the same conditional run configuration on any **Update Record** columns that should also be skipped when email validation fails.

Rows where the condition is not met show **"Run condition not met"** in the column cell — no Salesforce record is created or updated, and no credits are consumed for those rows.

For full details on writing run conditions, see [Conditional runs](https://university.clay.com/docs/conditional-runs).

## Does Salesforce enforce its required fields when Clay creates a record?

Yes. Clay does not validate required fields before sending data to Salesforce — all fields in the **Map fields** panel are optional from Clay's perspective. Salesforce enforces required fields at the API level: if a required field is missing from your mapping, Salesforce rejects the record creation and Clay displays the error from Salesforce (for example, `REQUIRED_FIELD_MISSING: Last Name`).

To avoid this, map all required fields for your Salesforce object in the **Map fields** section of your **Create Record** column. Which fields Salesforce marks as required depends on your org's configuration — check the object's field settings in Salesforce Setup, or look for the asterisk (\*) next to field labels in Salesforce's record creation form. Common required fields for the Contact object include **Last Name** and, depending on your org, **Account ID** (required when contacts must be associated with an account).

To skip rows where a required field is blank — rather than letting Salesforce reject them — add a run condition to your **Create Record** column. See [How do I prevent contacts from being pushed to Salesforce when required fields are blank?](#how-do-i-prevent-contacts-from-being-pushed-to-salesforce-when-required-fields-like-account-name-or-title-are-blank) for instructions.

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

This three-step pattern ensures new leads and contacts are added to the campaign and existing members have their status updated — without creating duplicate Campaign Member records.

**Note:** The valid `Status` values for Campaign Members are configured per campaign in Salesforce. Check your Salesforce org's Campaign Member Status settings to confirm the exact values before writing them from Clay.

For details on writing conditional runs, see [Conditional runs](https://university.clay.com/docs/conditional-runs). For SOQL tips and syntax, see the [Lookup records via SOQL](https://university.clay.com/docs/salesforce-integration-overview) action in the Salesforce integration overview.

## Why does my Campaign Member creation fail with a `DUPLICATE_VALUE` error for some rows?

This error means the contact or lead is already a member of that Salesforce campaign. While a contact can belong to multiple campaigns simultaneously, they cannot be added to the same campaign twice — Salesforce enforces this and rejects the creation with a `DUPLICATE_VALUE` error. This is expected Salesforce behavior, not a Clay issue.

The most common cause is that your **Create Record** column (set to the `CampaignMember` object) runs for every row in your table — including rows for contacts who were already in that campaign before your workflow ran.

**Option 1 — Gate on contact creation (simpler)**

If your table creates new contacts or leads in Salesforce before adding them to a campaign, add a run condition to your Campaign Member Create Record column so it only fires when the contact creation step succeeded. Brand-new contacts cannot already be campaign members, so the error won't occur.

In your Campaign Member **Create Record** column, open **Run settings** and add a conditional run. Set the condition to check that your contact creation column returned a result — for example, `/Create Contact is not empty`, replacing `Create Contact` with the actual name of your contact creation column. For details on writing run conditions, see [Conditional runs](conditional-runs.md).

**Option 2 — Look up campaign membership first (more precise)**

Add a **Lookup Record** or **Lookup records via SOQL** column to check whether the contact is already a member of the target campaign. Set a run condition on your Campaign Member Create Record column to only fire when that lookup returns no result. This approach works regardless of whether the contact was just created or already existed in Salesforce.

For step-by-step instructions and SOQL query examples, see [How do I add leads or contacts to a Salesforce campaign and update the status of existing campaign members?](#how-do-i-add-leads-or-contacts-to-a-salesforce-campaign-and-update-the-status-of-existing-campaign-members). That workflow also covers how to update the status of existing campaign members in the same pass.

## What are the default sync settings for CRM integrations?

By default, Clay syncs Salesforce imports every 24 hours. When new records or updates occur, this triggers action runs that enrich and export the updated fields.

**How do I turn on or off autoupdate?**

Auto-update can be controlled at two levels:

-   **Table level:** Click your table name in the top bar and select `Disable` or `Enable auto-update`. You can also access run settings via the ⚙️ icon in the bottom-right corner of the table.
-   **Column level:** Open an enrichment column, scroll to **Run settings** at the bottom of the column editor, and toggle **Auto-update** on or off. Column-level auto-update only applies when table-level auto-update is enabled.

## How can I reduce the Salesforce CPU utilization caused by Clay's queries?

The queries you see from Clay come from two sources: **Lookup Record columns** reading data from Salesforce on your behalf, and **scheduled imports** (such as a Lead import). Here are five adjustments that reduce the query load on your org:

1.  **Enable Exact match in your Lookup Record columns (biggest win).** By default, the **Lookup Record** action searches Salesforce using a wildcard query (`field LIKE '%value%'`), which performs a full-table scan — the primary driver of high CPU spikes. Enabling **Exact match** switches the query to an indexed equality lookup (`field = 'value'`), which is far lighter. For the biggest reduction, also match on an indexed field such as record ID, email, or an external ID. To enable: open the Lookup Record column, scroll to the search-field settings, and turn on **Exact match**.

2.  **Request only the fields you need.** The standard **Lookup Record** action fetches every field from the matched record using `FIELDS(ALL)`. Replacing it with a **Lookup records via SOQL** column lets you write a `SELECT` statement with only the specific fields you use and add a `LIMIT` clause, making each query much lighter. See the [Lookup records via SOQL](salesforce-integration-overview.md) section of the Salesforce integration overview for setup details.

3.  **Query fewer rows, less often.** Add [run conditions](https://university.clay.com/docs/conditional-runs) to your Lookup columns so they only fire on rows that actually need them. Turn off **auto-update** on columns that don't require continuous refresh (open the column → **Run settings** → toggle **Auto-update** off). Keep your object import on its default daily schedule rather than a more frequent one.

4.  **Stagger when rows run.** In a column's **Run settings**, set **Delay run** to **Run after delay** and enter a delay in seconds. This spreads queries out over time instead of firing them all at once, smoothing out CPU spikes on your org.

5.  **Narrow your import.** If you import records via a Salesforce list view, filter that list view so Clay scans fewer records each sync.

**Note:** The **Run in batches** setting is not available on the standard **Lookup Record** or **Lookup records via SOQL** columns, so it cannot be used to throttle these read queries. The adjustments above are the levers for reducing read-query load.

On the Salesforce side, asking your admin to add custom indexes on the fields Clay filters against will also help those queries run more efficiently.

## Why does enriching a Salesforce timestamp field cause records to keep re-running?

Salesforce system-managed fields such as `LastModifiedDate` and `SystemModstamp` are automatically updated by Salesforce on every record write — including writes triggered by Clay. If you reference one of these fields as an input in an enrichment that also writes back to Salesforce, you can inadvertently create an ongoing loop: Clay updates a record → Salesforce refreshes `LastModifiedDate` → Clay detects the change and re-runs the enrichment → cycle continues.

The same risk applies to any custom "last enriched" timestamp field that Clay itself populates. If that field is also used as a trigger or input for the same enrichment, the enrichment will keep re-running after every update.

**Workaround:** Instead of sending a Salesforce system-managed timestamp back to Salesforce, create a **formula column** in Clay that generates a timestamp based on a stable field — for example, a formula that returns the current date whenever the record's `Id` field is present. Use this formula column as the value you write back to Salesforce, rather than reading `LastModifiedDate` directly.

For general guidance on identifying and stopping automation loops, see [Infinite loops](infinite-loops.md).

## Is there a way I can test Salesforce enrichments?

Yes, you can test Salesforce enrichments by connecting Clay to your Salesforce sandbox org and using that connection when configuring enrichments or sources. This lets you test your Clay workflows with non-production data before running them against your live Salesforce instance.

To connect to a Salesforce sandbox:

1.  Go to `Settings` → `Connections`.
2.  Click `Add connection` and search for `Salesforce`.
3.  Under `User Sign In`, click `Sign in with Salesforce sandbox` and complete the OAuth sign-in flow.

Once connected, select your sandbox connection when adding any Salesforce enrichment or source in your Clay tables.

## Can I reverse my Salesforce enrichment?

No, once you update or create an object in Salesforce from Clay, you cannot undo these actions.

Please check with your Salesforce admin before making any changes to your Salesforce CRM.

## Do we need to create a custom Salesforce object to integrate Salesforce data?

No, one of Clay's benefits is that you can update any object and any field in Salesforce.

## Can I use a Salesforce API-only or Integration User license with Clay?

It depends on which connection method you use.

-   **User Sign In (OAuth):** No. API-only and Integration User licenses cannot complete the browser-based OAuth flow. Attempting to connect with one of these licenses via User Sign In produces an `OAUTH_APPROVAL_ERROR_GENERIC` error.
-   **Client Credentials:** Yes. Client Credentials connects server-to-server without a browser login and is compatible with API-only and Integration User licenses. See the [Salesforce integration](https://university.clay.com/docs/salesforce-integration-overview) doc for setup instructions.

## Why am I seeing an "OAUTH\_APPROVAL\_ERROR\_GENERIC" error when connecting Salesforce?

This error typically occurs when:

-   **Integration User License limitation:** The user attempting the connection has a Salesforce Integration User License or API Only license, which cannot complete UI-based OAuth approval flows.
-   **Connected app not pre-approved:** Your org requires pre-installation of connected apps. If Clay's connected app isn't pre-approved, Salesforce will block the OAuth approval.
-   **SSO enforcement:** When "Is Single Sign-On Enabled" is set on the user or an IdP-redirect flow is forced, Salesforce may not present the OAuth approval screen.

**How to fix:**

1.  **API-only or Integration User license:** Switch to [Client Credentials](https://university.clay.com/docs/salesforce-integration-overview) — it works with these license types and requires no browser login. If you must use User Sign In, switch to a full Salesforce user license (not Integration User) with a profile or permission set that includes API Enabled and Connected App Access.
2.  If your org enforces SSO, temporarily allow direct username/password login for this user, or create a non-SSO service account for authorization.
3.  In `Setup` → `Connected Apps OAuth Usage`, verify the Clay app is listed and not blocked. If your org uses App Access Control, pre-install or whitelist the app first.

## Do I need to install Clay's Connected App in my Salesforce org?

Yes. Since Salesforce's August 2025 security policy update, all Connected Apps — including Clay's — must be pre-installed in your org before users can authenticate. If Clay is not installed, Salesforce blocks the OAuth flow with an `OAUTH_APPROVAL_ERROR_GENERIC` error.

Clay's Connected App does not appear in the Salesforce AppExchange. It becomes available in your org only after a user with the "Approve Uninstalled Connected Apps" permission makes their first connection attempt. Salesforce System Administrators have this permission by default; custom profiles do not receive it automatically.

**To install Clay's Connected App:**

1.  **Register Clay in your org.** Have a Salesforce System Administrator attempt the Clay → Salesforce connection from Clay's `Settings` → `Connections`. Even if the connection fails, this attempt registers Clay in your org's Connected Apps OAuth Usage list. If you are using a custom profile (not a System Administrator), ensure the connecting user has the "Approve Uninstalled Connected Apps" permission — add it via a Permission Set in Salesforce Setup.
2.  **Install the app.** In Salesforce, go to `Setup` → `Apps` → `Connected Apps` → `Connected Apps OAuth Usage`. Find Clay in the list and click `Install`. Confirm when prompted.
3.  **Configure app policies.** After installation, `Manage App Policies` becomes available. Set `Permitted Users` to one of:
    -   `All users may self-authorize` — any Salesforce user can connect to Clay.
    -   `Admin approved users are pre-authorized` — only users explicitly granted access through Permission Sets or Profiles can connect. This is the more restrictive option, common in Enterprise security setups.
4.  **Reconnect Clay.** Return to Clay and complete the Salesforce connection — it should succeed without the OAuth error.

**Note for Salesforce sandboxes:** Each sandbox refresh assigns a new Org ID. Repeat these installation steps after any sandbox refresh.

## Why doesn't the Clay connected app appear under "Connected Apps OAuth Usage"?

A connected app only appears after a successful OAuth authorization. If it's missing, one of these is typically true:

-   The user's profile lacks the "Approve uninstalled connected apps" permission (required when the app isn't pre-installed).
-   Org policies block uninstalled connected apps entirely (via App Access Control).
-   SSO or login flows prevent the OAuth approval prompt.
-   IP restrictions, login-hour restrictions, or Transaction Security Policies block the OAuth request.

**How to fix:**

1.  Add "Approve uninstalled connected apps" to the user's profile or permission set.
2.  Try authorizing with a System Administrator user first—this lifts the "uninstalled" status and populates Connected Apps OAuth Usage.
3.  Once it appears, configure Connected App Policies (e.g., Permitted Users, IP Relaxation, Profile Assignments).

## What callback URL does Clay use for Salesforce?

-   [https://api.clay.com/v3/app-accounts/oauth/salesforce/callback](https://api.clay.com/v3/app-accounts/oauth/salesforce/callback)

## What OAuth scopes does Clay require for Salesforce?

Clay requires these scopes:

-   `api`
-   `refresh_token`
-   `id`
-   `openid`
-   `profile`

## Do I need to adjust IP or session restrictions in Salesforce to connect Clay?

Sometimes. Salesforce session-level or connected-app-level restrictions can interrupt OAuth flows or token exchanges.

**Common blockers:**

-   "Lock sessions to IP address" in Session Settings.
-   Strict HTTPS and network policies that reject redirects from Clay's servers.
-   Very short session timeouts that expire during the OAuth handshake.
-   Permitted IP ranges on the user's profile that exclude the browser or integration IP.
-   Connected App Policies requiring logins from fixed IP ranges.

**Recommendations:**

In `Setup` → `Session Settings`:

-   Disable "Lock sessions to IP address".
-   Use a reasonable session timeout to allow OAuth redirects.

In `Setup` → `Manage Connected Apps` → `Clay`:

-   Set `IP Relaxation` to "Relax IP Restrictions" (Clay's integration calls originate from cloud IPs that may change).
-   Set `Permitted Users` to "All users may self-authorize" unless your org requires admin approval.

## Why did the owner on my Salesforce record change when Clay updated a field?

If a Lead, Contact, or Account owner changes unexpectedly after Clay updates a field (for example, filling in a phone number), Salesforce assignment rules are likely the cause.

Assignment rules in Salesforce fire on every record save — not just when a record is created. When Clay updates a record, Salesforce treats it as a save and re-runs any active assignment rules, which can re-assign the owner.

**To prevent this**, open the settings for your **Update Record** column and enable the **Disable auto-assignment rules** option. This tells Salesforce to skip assignment rules when Clay saves the record.

**Note:** If your Update Record column was created before this option was added, the toggle may be off. Check your column settings if you are seeing unexpected owner changes after Clay updates a record.

## Why is the owner on a new Salesforce lead or contact set to the Clay integration user?

When Clay creates a record using the **Create Record** action, Salesforce sets the new record's owner to the Salesforce user Clay is authenticated as — typically the Clay integration user — because Clay does not set an Owner ID by default.

If your Salesforce org has assignment rules that specifically fire on records owned by integration users (a common pattern for automated lead routing), those rules can trigger at creation time and re-assign the record to a queue or different owner.

**To control the owner at creation time**, add the **Owner ID** field in the **Map fields** section of your **Create Record** column and set it to the Salesforce User ID of the intended owner. If your Clay table has the owner's name rather than their Salesforce User ID, add a **Lookup Record** column (set the Salesforce object to **User** and search by name) to retrieve the ID first — see [Why am I seeing a `MALFORMED_ID` error when creating or updating a Salesforce record?](#why-am-i-seeing-a-malformed_id-error-when-creating-or-updating-a-salesforce-record) for the step-by-step workflow. When the record is created with the correct owner already set, assignment rules that specifically target integration-user-owned records will not match.

**Note:** Unlike the **Update Record** action — which has a **Disable auto-assignment rules** toggle for leads, cases, and accounts — the **Create Record** action does not have a built-in option to suppress assignment rules entirely. If your org has assignment rules that fire on all new records regardless of owner, you will need to adjust those rules on the Salesforce side.

## Why am I seeing an `INACTIVE_OWNER_OR_USER` error when creating records in Salesforce?

This error means Salesforce tried to assign the new record to a deactivated user. Clay's **Create Record** action does not set an Owner ID by default — when no owner is explicitly mapped, Salesforce applies its own ownership logic, which can include inheriting the Account owner as the Contact owner, running assignment rules, or triggering owner-routing flows. If that logic points to a deactivated user, Salesforce rejects the record creation with `INACTIVE_OWNER_OR_USER`.

Because the assignment happens on the Salesforce side, some rows may succeed (for accounts whose owner is active) while others fail (for accounts whose owner has been deactivated).

**Clay-side workaround: explicitly map an Owner ID**

You can bypass Salesforce's automatic owner assignment by mapping the **Owner ID** field in your **Create Record** column to a valid, active Salesforce User ID:

1.  In your **Create Record** column, click **+ Add field** in the **Map fields** section and select **Owner ID**.
2.  Map it to a Clay column containing valid Salesforce User IDs, or type a static User ID directly.
3.  If your Clay table has the owner's name rather than their Salesforce User ID, add a **Lookup Record** column (set the Salesforce object to **User** and search by name or email) to retrieve the ID first. See [Why am I seeing a `MALFORMED_ID` error when creating or updating a Salesforce record?](#why-am-i-seeing-a-malformed_id-error-when-creating-or-updating-a-salesforce-record) for the step-by-step lookup workflow.

When the Owner ID is explicitly set to an active user, Salesforce does not fall back to its default assignment logic for that field.

**Salesforce-side fixes**

If you prefer to resolve the issue on the Salesforce side, ask your Salesforce admin to:

-   **Reactivate the user.** If the deactivated user should still own the records, reactivate their account in Salesforce.
-   **Reassign the Account to an active user.** If new contacts are inheriting their owner from a deactivated Account owner, reassigning the Account to an active user — and bulk-updating the existing contacts on that Account — allows new contacts to be created without the error.
-   **Review assignment rules and owner-routing flows.** Check which assignment rule, Flow, or routing automation is pointing records at the deactivated user and update it to route to active users only.

## Why am I seeing a "Retried but failed: Failed to lock row" error when updating Salesforce records?

This error means Salesforce returned an `UNABLE_TO_LOCK_ROW` response — it could not get exclusive write access to a record because another process was writing to it (or a related record) at the same time.

**Why it happens with Clay**

Clay runs enrichment rows in parallel. When a **Create record**, **Update record**, or **Upsert object** action fires on many rows at once, multiple API calls reach Salesforce simultaneously. If those rows write to records that share a common parent — for example, contacts all mapped to the same placeholder Account — Salesforce locks that parent Account record on each update. When many rows try to lock it simultaneously, some are blocked and the error occurs.

A frequent amplifier is **Declarative Lookup Rollup Summaries (DLRS)** — a Salesforce automation that recalculates a rollup value on a parent record whenever any child record is saved. DLRS holds a write lock on the parent while the rollup runs, which causes concurrent saves on sibling child records to fail with `UNABLE_TO_LOCK_ROW`.

Manual retries succeed because running one cell at a time eliminates the simultaneous lock competition.

**Workarounds**

-   **Enable "Run in batches":** In the action column's **Run settings**, enable **Run in batches**. This sends rows through Salesforce's Composite API in sequential groups rather than all at once, reducing concurrent writes and lowering the chance of lock collisions.
-   **Add a run delay:** In the action column's **Run settings**, set **Delay run** to **Run after delay** and enter a delay in seconds. This staggers when each row fires, giving Salesforce time for in-flight automations (such as DLRS rollups) to finish before the next write arrives.
-   **Map records to real parent objects:** If many rows share the same placeholder Account (or other shared parent), map them to their actual parent records instead. Each write then locks a different record, eliminating the collision.
-   **Ask your Salesforce admin to review automations:** If your org uses DLRS or other triggers on shared parent records, your admin can investigate switching those rollups to scheduled mode — this decouples the rollup write from the original save and eliminates the lock contention entirely.

**Note:** `UNABLE_TO_LOCK_ROW` is a Salesforce-side limitation, not a Clay bug. Clay automatically retries when this error occurs, but surfaces "Retried but failed: Failed to lock row" after exhausting its retry budget.

## Why do records created or updated by Clay show my name (or another user's name) in Salesforce's Created By or Last Modified By field?

Salesforce's `CreatedBy` and `LastModifiedBy` audit fields always reflect the **Salesforce user whose credentials authenticated the API request**. Clay does not have a mechanism to override this — it passes the connection's access token with each API request, and Salesforce sets those fields accordingly.

**For the User Sign In connection method:** Clay authenticates as whichever Salesforce user was active in the browser when you completed the OAuth setup. If you were logged into your personal Salesforce account at that moment, all records Clay writes will show your personal name in those fields — even if you have a dedicated "integration user" configured in Salesforce. The integration user's name will only appear in `CreatedBy` and `LastModifiedBy` if the Clay connection was actually authenticated *as* that integration user.

**To fix this**, reconnect Clay using the integration user's credentials. See [How do I connect to Salesforce as a specific user](#how-do-i-connect-to-salesforce-as-a-specific-user-such-as-an-integration-user-using-user-sign-in) below for steps.

**For the Client Credentials connection method:** `CreatedBy` and `LastModifiedBy` reflect the Salesforce execution user configured in the Connected App's **Run As** field during setup — not whoever configured the Clay connection. This is one reason Client Credentials is often preferred for dedicated integration accounts — the audit fields consistently show the configured execution user regardless of who set up the Clay connection.

**To check which Salesforce user your connection is currently authenticated as**, go to `Settings` → `Connections` → `Salesforce`, click `…` next to your connection, and select `Test Connection`. Clay will display the email address of the authenticated user.

## How do I connect to Salesforce as a specific user (such as an integration user) using User Sign In?

When you connect via **User Sign In**, Clay opens an OAuth popup that authenticates using whatever Salesforce session is active in your browser at that moment. If you are already signed in to Salesforce as your personal account, Clay will connect as you — not as the intended integration user.

To connect as a specific Salesforce user:

1.  Open an incognito or private browser window (this gives you a fresh session with no existing Salesforce login).
2.  Log into Salesforce as the user you want Clay to connect as (for example, a dedicated service account).
3.  From that same window, open Clay and go to `Settings` → `Connections`.
4.  Click `Add connection` (or `Reconnect` on an existing Salesforce connection) and complete the OAuth sign-in flow. Clay will authenticate as whoever is logged into Salesforce in that window.
5.  Optionally, rename the connection (for example, "SFDC Integration User") so it is easy to identify later.

Make sure the connecting user has **API Enabled** and the correct object and field permissions for everything you plan to read or write in Clay. For guidance on setting up a service account with the right access, see [Creating a restricted Salesforce user](https://university.clay.com/docs/creating-a-restricted-salesforce-user).

**Note:** If your Salesforce org uses an Integration User license or API-only license, the User Sign In OAuth flow may not work. If your org enforces SSO (such as Okta, Azure AD, or Google Workspace), incognito may not resolve the issue either — SSO authenticates at the identity provider level, not the browser session level, so your personal account can be picked up automatically even in a fresh private window. In either case, use **Client Credentials** ([setup instructions](https://university.clay.com/docs/salesforce-integration-overview)) instead — it connects server-to-server with no browser login, so SSO cannot intercept it.

## Why can't I set a Salesforce connection as the default, or change which connection is the default?

Setting or changing the default Salesforce connection is restricted to **workspace admins**. Non-admin workspace members do not see the **Set as default** option in the connection menu.

If you need to change the default connection, ask a workspace admin to:

1.  Go to `Settings` → `Connections` and select `Salesforce`.
2.  Find the connection you want to make the default.
3.  Click the `…` menu next to it and select `Set as default`.

To change your own role to admin, ask an existing workspace admin to update it in `Settings` → `Team`.
