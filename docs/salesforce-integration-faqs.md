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

**Changing the default:** Setting a connection as default is a **workspace admin–only** action — non-admin workspace members do not see the **Set as default** option in the `…` menu. To update the default, ask a workspace admin to change it in `Settings` → `Connections`, or have an admin update your user role. For details on connection management permissions, see [Workspace administration](https://university.clay.com/docs/workspace-administration-documentation).

**Deleting the default connection:** You can delete a connection that is currently set as default. When you do, Clay automatically reassigns the default to the next available Salesforce connection. If no other connection exists, the default is cleared. Note that deleting any connection requires you to be either the person who originally added it or a workspace admin — you cannot delete a connection added by someone else unless you are an admin.

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

## Why does a Salesforce Lookup return "no records found" when searching by phone number?

If the column holding phone numbers is set to **Number** type, Clay alters the value before passing it to Salesforce. A phone number in plain E.164 format — for example, `+12345678900` — stored in a Number column loses its leading `+`, becoming `12345678900`. If Salesforce stores the number as `+12345678900`, the lookup finds no match. Phone numbers that contain spaces or dashes (for example, `+1 234-567-8900`) produce a coercion error in the cell rather than a silently altered value.

**To fix:** Click the phone number column header, hover over the current data type, and switch it to **Text**. Text columns preserve the exact phone number string — including the leading `+` and any separators — so the value Clay sends to Salesforce matches what Salesforce has stored.

## Why is my Salesforce report data not populating in Clay?

The most likely cause is the report's format. Clay's **Import records from a Salesforce report** source only supports **Tabular** and **Matrix** report formats. Reports in **Summary** or **Joined** format are not supported and will return an error when Clay tries to run them.

Clay's report picker automatically filters to show only Tabular and Matrix reports, so if a report is missing from the picker, it is likely in an unsupported format.

**To fix:** In Salesforce, open the report, click **Edit**, then change the report format to **Tabular** (a flat list without row groupings) or **Matrix** (rows and columns both grouped). Save the report, then re-run your Clay source.

For an overview of Salesforce report formats, see Salesforce's [Report Formats documentation](https://trailhead.salesforce.com/content/learn/modules/lex_implementation_reports_dashboards/lex_implementation_reports_dashboards_report_formats).

## Will Clay create duplicate records in Salesforce?

No. By default, Clay prevents duplicate records. However, you can allow duplicates by enabling the "Duplicate Rule Override" in the Create Record enrichment.

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

## How do I prevent Salesforce records from being created or updated when there is no valid email?

Use conditional runs on your **Create Record** and **Update Record** action columns to gate them on a passing email validation result. Rows where email validation fails are skipped automatically and do not consume credits.

Here's how to set it up:

1.  Ensure your table has an email validation enrichment column (for example, Clay's built-in **Validate Email** enrichment or a third-party email validator). This column produces a status or result value for each row.
2.  On your **Create Record** column, open **Run settings** and add a conditional run. Set the condition to only run when the email validation column indicates a valid email — for example, `/Email Validation Status is "valid"` or `/Validate Email is not empty`, depending on what your validation enrichment outputs.
3.  Repeat the same conditional run configuration on any **Update Record** columns that should also be skipped when email validation fails.

Rows where the condition is not met show **"Run condition not met"** in the column cell — no Salesforce record is created or updated, and no credits are consumed for those rows.

For full details on writing run conditions, see [Conditional runs](https://university.clay.com/docs/conditional-runs).

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

## What are the default sync settings for CRM integrations?

By default, Clay syncs Salesforce imports every 24 hours. When new records or updates occur, this triggers action runs that enrich and export the updated fields.

**How do I turn on or off autoupdate?**

Auto-update can be controlled at two levels:

-   **Table level:** Click your table name in the top bar and select `Disable` or `Enable auto-update`. You can also access run settings via the ⚙️ icon in the bottom-right corner of the table.
-   **Column level:** Open an enrichment column, scroll to **Run settings** at the bottom of the column editor, and toggle **Auto-update** on or off. Column-level auto-update only applies when table-level auto-update is enabled.

## Why does enriching a Salesforce timestamp field cause records to keep re-running?

Salesforce system-managed fields such as `LastModifiedDate` and `SystemModstamp` are automatically updated by Salesforce on every record write — including writes triggered by Clay. If you reference one of these fields as an input in an enrichment that also writes back to Salesforce, you can inadvertently create an ongoing loop: Clay updates a record → Salesforce refreshes `LastModifiedDate` → Clay detects the change and re-runs the enrichment → cycle continues.

The same risk applies to any custom "last enriched" timestamp field that Clay itself populates. If that field is also used as a trigger or input for the same enrichment, the enrichment will keep re-running after every update.

**Workaround:** Instead of sending a Salesforce system-managed timestamp back to Salesforce, create a **formula column** in Clay that generates a timestamp based on a stable field — for example, a formula that returns the current date whenever the record's `Id` field is present. Use this formula column as the value you write back to Salesforce, rather than reading `LastModifiedDate` directly.

For general guidance on identifying and stopping automation loops, see [Infinite loops](infinite-loops.md).

## Is there a way I can test Salesforce enrichments?

Yes. Connect Clay to your Salesforce sandbox org and use that connection when configuring enrichments or sources. This lets you test your Clay workflows with non-production data before running them against your live Salesforce instance.

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

**Note:** If your Salesforce org uses an Integration User license or API-only license, the User Sign In OAuth flow may not work. Use [Client Credentials](https://university.clay.com/docs/salesforce-integration-overview) instead — that method connects server-to-server without a browser login.

## Why can't I set a Salesforce connection as the default, or change which connection is the default?

Setting or changing the default Salesforce connection is restricted to **workspace admins**. Non-admin workspace members do not see the **Set as default** option in the connection menu.

If you need to change the default connection, ask a workspace admin to:

1.  Go to `Settings` → `Connections` and select `Salesforce`.
2.  Find the connection you want to make the default.
3.  Click the `…` menu next to it and select `Set as default`.

To change your own role to admin, ask an existing workspace admin to update it in `Settings` → `Team`.
