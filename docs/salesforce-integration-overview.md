---
title: Salesforce integration
description: Cloud-based customer relationship management software.
last_synced: 2026-05-11T17:47:40.000Z
---

# Salesforce integration

Cloud-based customer relationship management software.

Salesforce is a customer relationship management (CRM) platform that helps businesses manage their customer data and relationships. This integration lets you sync your Salesforce data with Clay to streamline your workflow.

## Connecting to Salesforce

Clay supports two methods for authenticating your Salesforce account. You can choose the one that fits your organization's setup when adding a new connection or when reconnecting an existing one.

-   **User Sign In** — the default method. You sign in as a Salesforce user via an OAuth browser prompt.
-   **Client Credentials** — a server-to-server method. No browser sign-in is required; instead, you supply credentials from an external client app configured in your Salesforce org.

### User Sign In

Connect via OAuth as a Salesforce user.

1.  In the home sidebar, click `Settings` → `Connections`.
2.  Click `Add connection` and search for `Salesforce`.
3.  Under `User Sign In`, choose which environment to connect — click `Sign in with Salesforce` to connect your **production** org, or click `Sign in with Salesforce sandbox` to connect a **sandbox** org — then complete the OAuth sign-in flow in the browser window that opens.

**Tip:** Clay authenticates as whichever Salesforce user is active in the browser during the OAuth flow. If you need to connect as a specific user — for example, a shared integration or service account rather than your personal Salesforce account — sign in to Salesforce as that user before starting the Clay flow. Opening an incognito or private-browser window lets you do this without signing out of your own Salesforce session. For dedicated integration accounts, the **Client Credentials** method below is often a better fit — it requires no browser sign-in and works with Salesforce Integration licenses.

### **Client Credentials (Integration User)**

Connect to Salesforce via Client Credentials for server-to-server access. No browser sign-in is required.

**Setting up in Salesforce**

1.  In Salesforce Setup, search for `External Client App Manager` in Quick Find and select it. Create a new external client app — see [**Salesforce's documentation**](https://help.salesforce.com/s/articleView?id=xcloud.create_a_local_external_client_app.htm&language=en_US&type=5) for full creation steps. Set **Distribution State** to `Local`. When configuring the app's OAuth settings:
    -   **Callback URL:** Salesforce requires this field to be populated even for server-to-server flows. You can enter `https://login.salesforce.com/services/oauth/callback`.
    -   **OAuth Scopes:** Add **Access and manage your data (`api`)** — this scope is required; without it, Salesforce returns `invalid_grant: no valid scopes defined` when Clay tries to connect. Adding **Access the identity URL service (`id, profile, email, address, phone`)** is optional but enables Clay's Test Connection feature to display which user and org the connection is authenticated as.

    Once created, click on your app and select `Edit`.
2.  In the `Settings` tab, enable the flow at the app level:
    -   Under `Flow Enablement`, check `Enable Client Credentials Flow`.
3.  In the `Policies` tab, configure access and enable the flow:
    -   Under **Select Permission Sets**, choose only the permission set(s) assigned to your integration user.
    -   Set **Permitted Users** to `Admin approved users are pre-authorized`.
    -   Under `OAuth Flows and External Client App Enhancements`, check `Enable Client Credentials Flow`. This is the setting most commonly missed — if it's off, the flow is blocked regardless of the Settings toggle.
    -   In the `Run As` field, enter the username of the integration user the app will authenticate as.
4.  Click `Save`. See [**Salesforce's documentation**](https://help.salesforce.com/s/articleView?id=xcloud.configure_client_credentials_flow_for_external_client_apps.htm&language=en_US&type=5) for full details on configuring the Client Credentials flow.

**Connecting in Clay**

1.  In the home sidebar, click `Settings` → `Connections`.
2.  Click `Add connection` and search for `Salesforce`.
3.  Under `Client Credentials`, fill in the following fields:
    -   `My Domain URL`: Your Salesforce My Domain URL (e.g. `https://mycompany.my.salesforce.com`).
    -   `Consumer key`: The consumer key from your Salesforce external client app.
    -   `Consumer secret`: The consumer secret from your Salesforce external client app.
4.  Click `Authenticate` to save the connection.

### **Troubleshooting**

-   **`OAUTH_APPROVAL_ERROR_GENERIC` when connecting via User Sign In**

This error appears during the OAuth flow and is most commonly caused by one of the following:

-   **Integration User or API Only license:** These licenses cannot complete the OAuth flow. Use a full Salesforce user license, or switch to `Client Credentials`.
-   **Connected app not pre-approved:** If connected apps require pre-approval, Salesforce may block Clay. In Salesforce Setup, go to `Connected Apps OAuth Usage` and confirm Clay is not blocked. Set `IP Relaxation` to `Relax IP Restrictions` and `Permitted Users` to `All users may self-authorize`.
-   **SSO enforcement:** If SSO is enforced, the OAuth approval screen may be blocked. Try a non-SSO user, or create a non-SSO service account.
-   **Missing permission:** The user's profile may lack `Approve uninstalled connected apps`. Ask a Salesforce admin to grant it, or connect with a System Administrator account.

-   **`invalid_grant: no valid scopes defined` when connecting via Client Credentials**

This error means the Salesforce Connected App (or external client app) has no OAuth scopes configured, so Salesforce rejects Clay's token request entirely. To fix:

1.  In Salesforce, go to `Setup` → `App Manager` (for a traditional Connected App) or `External Client App Manager` (for an external client app), and open the app used for Clay.
2.  Under **OAuth Settings**, add the **Access and manage your data** (`api`) scope.
3.  Click `Save`. Salesforce can take up to 10 minutes to propagate scope changes.
4.  Return to Clay and reconnect: `Settings` → `Connections` → add or reconnect your Salesforce `Client Credentials` connection.

### Testing your connection

To verify a Salesforce connection is working — and to confirm which Salesforce user it is authenticated as:

1.  Navigate to `Settings` → `Connections` and select `Salesforce`.
2.  Click the `…` menu next to the connection you want to test.
3.  Select `Test Connection`.

Clay will confirm the connection is valid and display the Salesforce user (by email) and the Salesforce org the connection is attributed to. Because all data access in Clay is scoped to the permissions of that authenticated user, seeing which user is in the seat makes it easy to debug access issues — for example, if objects or fields are missing, you can immediately check whether the displayed user has the right permissions in Salesforce.

After testing a connection, Clay saves the result and shows the connected user and Salesforce org directly in the connections list — so you can see at a glance which account each connection belongs to without re-testing each time.

### IP allowlisting

On **Enterprise plans**, all Salesforce connections in Clay automatically route through Clay's static IP addresses — no toggle or configuration is needed. If your Salesforce org restricts connections by IP address, contact Clay support to request the current IP list, then allowlist them in Salesforce under `Setup` → `Network Access` → `New`.

For full instructions on setting up a restricted Salesforce user with field-level security and IP allowlisting, see [Creating a restricted Salesforce user](https://university.clay.com/docs/creating-a-restricted-salesforce-user).

## Creating a table with Salesforce

1.  In a workbook, click `+ Add` at the bottom.
2.  Search for `Salesforce` and select from the results.
3.  In the modal, you will be asked to `Select Salesforce account`.
    -   If you haven't already connected your Salesforce account, click `+ Add account` and go through authentication.

### `Source` Import records from a Salesforce list

**Inputs:**

-   **Salesforce object:** The type of object to look for in Salesforce.
-   **List view:** The view to sync into Clay.
    -   Views that are not SOQL-compatible (those that cannot be generated from a SOQL query) have a 2,000-record limit.

**Fields not in your Salesforce list view**

Clay imports exactly the fields that are columns in your selected Salesforce list view. Any field not included in that list view will not appear in your Clay table, even if the data exists in Salesforce. Two types of fields commonly go missing this way:

-   **Custom or optional direct fields** — fields stored on the object itself (for example, a custom LinkedIn URL field on a Contact) that weren't added as a column to your Salesforce list view.
-   **Related (cross-object) fields** — fields stored on a related object (for example, `Account Name` shown in a Contact list view, which is actually stored on the Account object). These are never imported even if they appear as columns in the list view.

To get a missing field into Clay, use one of these approaches:

1.  **Add a Lookup record column in Clay (fastest).** Use the **Lookup record** enrichment to fetch the full record by its Salesforce Object ID (which is always imported). This returns **all** fields on the object — including any custom fields — regardless of what was in your list view. For cross-object fields, use the related object's ID (e.g., `AccountId` on Contact) to look up the related record and pull any field from it.
2.  **Add the field to your Salesforce list view.** In Salesforce, edit the list view to include the missing column, then re-run the source in Clay to pick it up. For cross-object fields, first create a formula text field on the object that copies the related value (for example, a formula field on Contact with the expression `Account.Name`). Once added to the list view in Salesforce, Clay imports it as a direct field. This is useful when you need the value available in multiple Clay tables without a per-row lookup step.

### `Source` Import records from a Salesforce report

**Inputs:**

-   **Report to run:** The report to run in your Salesforce instance.
    -   Only tabular and matrix reports are supported. Salesforce limits reports to a maximum of 2,000 records. If you need to import more than 2,000 records, you have two alternatives: switch to the **Salesforce List source** (import from a list view instead of a report — SOQL-compatible list views support up to 50,000 records), or use the [Salesforce SOQL source](salesforce-soql.md) (write a custom SOQL query that also bypasses this cap, up to 50,000 records per import).
-   **Uniqueness fields:**
    -   Since Salesforce reports lack unique identifiers, select specific fields to identify each row. This prevents duplicate records from appearing when the report updates.
        -   **Important:** If you don't select any fields, Clay will use the entire row content as the unique identifier. This can result in many duplicate entries in your Clay table.
        -   **How deduplication works:** When the report re-syncs, Clay compares each incoming record against your chosen uniqueness field(s). If a record with a matching key already exists in the table, Clay **skips that incoming record** — the existing row's data in Clay is preserved unchanged, and no duplicate is created. Only records with no matching key get inserted as new rows.
        -   **Records no longer in the report are not removed:** When the report re-syncs, any records previously imported into your Clay table that no longer appear in the new report run **stay in your table** — they are not deleted automatically. Clay sources are additive only. If you need accounts to be removed from Clay when they fall off the report — for example, to keep a list that reflects accounts qualifying in and out of a segment each day — use [Clay Audiences](audiences.md) instead. With Audiences you connect Salesforce directly and define your criteria as a segment filter; records are added when they match and removed automatically when they no longer qualify.
        -   **Preserving run history / audit logs:** Because re-synced records that match an existing uniqueness key are skipped (not overwritten), your existing enrichment data for those rows is preserved across syncs. If you need to track every sync event — for example, to log when records entered or left the report — add a **Send Table Data** action after your enrichment columns to push a timestamped snapshot to a separate history table. See [Send table data](send-table-data.md) for setup details.

## Enriching data with Salesforce

1.  While in a Clay table, click `Add enrichment` and search for `Salesforce`.
2.  Under `Integrations`, select one of the Salesforce options.
3.  In the modal, you will be asked to `Select Salesforce account`.
    -   If you haven't already connected your Salesforce account, click `+ Add account` and go through authentication.

### `Action` Lookup records via SOQL

Look up records in Salesforce using a custom SOQL query. Use this when the standard **Lookup record** action returns too many matches, when you need to filter on multiple fields at once (e.g., website AND country code), or when the Lookup record action returns **"Error: Bad Request"** (which occurs when the object's schema has more than 15 cross-object field references — see [Salesforce integration FAQs](salesforce-integration-faqs.md) for details).

**Inputs:**

-   **SOQL query:** A `SELECT` statement with explicitly listed fields. For SOQL syntax reference, see [Salesforce's documentation](https://developer.salesforce.com/docs/atlas.en-us.soql_sosl.meta/soql_sosl/sforce_api_calls_soql.htm).

**Referencing Clay columns in your query**

To insert a Clay table column value into the query, type `/` anywhere in the query field and select a column from the menu that appears. Do **not** type `{{column_name}}` directly — that syntax is not evaluated in the SOQL query editor and will cause the query to return no results.

For example, to match on a Company Domain column and a Country Code column:

```sql
SELECT Id, Name, Website
FROM Account
WHERE Website LIKE '%/Company Domain%'
AND BillingCountryCode = '/Country Code Column'
LIMIT 1
```

*(Here `/Company Domain` and `/Country Code Column` represent Clay columns inserted via the `/` picker — they are replaced with each row's values at run time.)*

**Tips**

-   **Always include `LIMIT`.** If your query matches many Salesforce records (for example, a global brand with regional accounts sharing the same domain), the total response can exceed the 200 kB cell size limit, which produces a "Cell data size exceeds limit (200 kB)" error. Adding `LIMIT 1` or a small number keeps the response size manageable.
-   **Use `LIKE` for website and domain fields.** Salesforce often stores URLs with inconsistent prefixes (`www.example.com`, `https://example.com`, `example.com`). The `LIKE` operator with `%` wildcards matches all formats: `WHERE Website LIKE '%/Company Domain%'`.
-   **Handle missing values with an `OR NULL` fallback.** If the extra filter field is not consistently populated in Salesforce, a strict `AND` will drop valid records. Add a null check so rows with a blank field are still returned: `AND (BillingCountryCode = '/Country Code Column' OR BillingCountryCode = null)`.
-   **Use a waterfall for optional tiebreakers.** To use an extra field as a preference rather than a hard filter, create two SOQL columns — one matching on website + country code, one on website only — and use a Formula column to return the first non-empty result.

### `Action` Create record

Use this action to create a new record in Salesforce.

**Inputs:**

-   **Salesforce object:** The object type to look for in your Salesforce.
-   **Duplicate rule override:** When enabled and you have a [duplicate rule](https://help.salesforce.com/s/articleView?id=sf.duplicate_rules_map_of_reference.htm&type=5), Clay will bypass the rule and create a new record, even if it duplicates an existing one.

**Map fields**

After selecting a Salesforce Object, the **Map fields** section lets you specify which fields to set on the new record. The section starts empty — add only the fields you need.

-   **+ Add field**: Opens a searchable list of all available fields for the selected Salesforce object. Select a field to add it, then map it to a column or value from your Clay table. Repeat for each field you want to set.
-   **Refresh**: Reloads the field list from Salesforce. Use this if you've recently added or modified fields in your Salesforce org and they're not appearing in the picker.

Fields not added here are left blank on the new record.

**Tip: Adding contacts or leads to a Salesforce Campaign**

Clay does not have a dedicated "Add to Campaign" action. To add a contact or lead to a Salesforce Campaign, use **Create Record**, select **Campaign Member** as the Salesforce object, and map both the **ContactId** (or **LeadId**) and **CampaignId** fields. If the record is already a campaign member, Salesforce returns a `DUPLICATE_VALUE` error — you can guard against this by first running a **Lookup record** action with "Campaign Member" as the object to check whether the association already exists.

To also set or update the **Status** of existing Campaign Members — for example, when the same lead or contact may already be in the campaign — use a three-step workflow: a **Lookup records via SOQL** action to check if the person is already a member, a conditional **Create record** if they are not, and a conditional **Update record** if they are. For step-by-step instructions and SOQL query examples, see [How do I add leads or contacts to a Salesforce campaign and update the status of existing campaign members?](salesforce-integration-faqs.md) in the Salesforce integration FAQs.

**Tip: Posting a Salesforce Chatter note**

To post a Chatter note on any Salesforce record (such as an Account, Contact, or Opportunity), use **Create Record**, select **Feed Item** as the Salesforce object, and map two fields: **Parent ID** (the Salesforce ID of the record you want to post to) and **Body** (the text content of the post). **Feed Item** only appears in the object picker if Chatter is enabled in your Salesforce org — if you don't see it, check your Salesforce org's Chatter settings.

### `Action` Lookup record

Use this action to find existing records in Salesforce.

**Inputs:**

-   **Salesforce object:** The object type to look for in your Salesforce.
-   **Exact match? (optional):** When enabled, finds exact matches across all search fields.

**How matching works**

The **Exact match?** toggle controls how Clay queries Salesforce:

-   **Exact match ON:** Clay uses an equality filter (`field = 'value'`). Only records whose field value matches your Clay value exactly are returned.
-   **Exact match OFF (default):** Clay uses a contains filter (`field LIKE '%value%'`). Salesforce returns records where the field value **contains** your Clay value as a substring. This is **not** fuzzy matching — there is no tolerance for typos or partial words.

**Important asymmetry with contains matching:** The search term is always your Clay value, and it must be a substring of the Salesforce field value. This means:

-   If your Clay table has `"Servier Pharmaceuticals"` and Salesforce only has `"Servier"`, **no match is returned** — `"Servier"` does not contain `"Servier Pharmaceuticals"`.
-   If your Clay table has `"Servier"` and Salesforce has `"Servier Pharmaceuticals"`, **a match is returned** — `"Servier Pharmaceuticals"` does contain `"Servier"`.

**Tip:** Name-only matching can be unreliable when names differ in length or format between Clay and Salesforce. For more reliable matching, use unique identifiers like website domain or LinkedIn URL alongside (or instead of) name. If you need multiple fields to match, use the **Lookup records via SOQL** action for full control over the query.

**Note:** Each "field to search for" input accepts one search value at a time. If you add multiple values to a single search field, Clay concatenates them into one string rather than treating them as separate options — for example, adding both `"Acme Corp"` and `"Acme"` to the same "Account Name to search for" field causes Clay to search for `"Acme CorpAcme"` instead of either name. To search across multiple possible values for the same field, use two separate **Lookup record** columns, each with one value.

**Tip:** When using a Lookup Record column to supplement a Salesforce list view source import, make sure both use the **same Salesforce account**. If they use different accounts, the lookup queries a different Salesforce org and returns `No records found` even when the record exists.

### `Action` Upsert object

Use this action to create a new record or update an existing one.

_Note: In order for upsert to work, you need to have an_ [_external ID_](https://help.salesforce.com/s/articleView?id=000385174&language=en_US&type=1) _on the object._

**External ID value requirements**

Salesforce processes the upsert by placing the external ID value directly in the REST API URL path. Values containing URL-special characters — most commonly forward slashes (`/`) — will cause the upsert to fail with **"Upsert Failed"** and no additional error details.

**Characters to avoid:** `/`, `#`, `?`, `&`, `%`, `+`, and spaces.

**Common example:** A value like `linkedin.com/company/acme-corp` contains forward slashes that Salesforce interprets as URL path separators, causing the upsert to fail.

**Recommended format:** Use only alphanumeric characters, hyphens (`-`), and underscores (`_`). Apply the same sanitized format to the corresponding field in Salesforce so records still match — for example, use `acme-corp` instead of `linkedin.com/company/acme-corp`.

**Tips for choosing and handling an upsert key**

-   **Recommended key for account syncs:** Use **domain** as your upsert key when syncing accounts to Salesforce. Domain is the most stable and widely-supported identifier for account matching. LinkedIn URL can serve as a supplemental identifier, but it is not ideal as a primary upsert key — LinkedIn URLs contain forward slashes that cause upsert failures unless sanitized (see above), and format inconsistencies make matching unreliable. Note that Salesforce's upsert API accepts only **one external ID field per call** — combined or compound keys are not supported.

-   **Blank upsert key behavior:** If the upsert key field is blank or null for a row, the action errors out on that row — it does not skip the row or attempt a create. To avoid errors on rows with missing domain values, add a **conditional run** so the Upsert object action only fires when the domain field is populated. See [Conditional runs](https://university.clay.com/docs/conditional-runs) for setup instructions.

-   **Handling a fallback key:** The cleanest approach is to enrich blank domains before your upsert runs — use Clay's enrichment columns (for example, find domain from LinkedIn URL or company name) so every row has a domain value before the action fires. If enrichment isn't possible for all rows, a two-step approach works: use a **Lookup record** column to find the account by domain, fall back to a second **Lookup record** by LinkedIn URL (with the URL sanitized per the format above), then use conditional **Create record** or **Update record** columns based on which lookup succeeded.

**Inputs:**

-   **Salesforce object:** The object type to look for in your Salesforce.

### `Action` Update record

Use this action to modify existing records in Salesforce.

**Inputs:**

-   **Record ID:** The ID of the record to update.
-   **Salesforce object:** The object type to look for in your Salesforce.
-   **Ignore blank values (optional):** When enabled, blank values from Clay will be ignored.
-   **Disable auto-assignment rules (optional):** When enabled, Salesforce will not apply lead and contact assignment rules when the record is updated. Enable this setting if you do not want your Salesforce assignment rules to fire when Clay updates a record.

**Map fields**

After selecting a Salesforce Object, the **Map fields** section lets you specify which fields to update. The section starts empty — add only the fields you need to change.

-   **+ Add field**: Opens a searchable list of all updateable fields for the selected Salesforce object. Select a field to add it, then map it to a column or value from your Clay table. Repeat for each field you want to update.
-   **Refresh**: Reloads the field list from Salesforce. Use this if you've recently added or modified fields in your Salesforce org and they're not appearing in the picker.

Fields not added here are left unchanged in Salesforce.

### `Action` Convert lead

Use this action to convert a lead.

**Inputs:**

-   **Lead ID:** The ID of the lead to convert.
-   **Converted status:** The status to assign to the lead after conversion.
-   **Account ID (optional):** The ID of the account to link to the converted lead.
-   **Contact ID (optional):** The ID of the contact to link to the converted lead.
-   **Create opportunity? (optional):** Whether to create an opportunity for the converted lead.
-   **Opportunity ID (optional):** The ID of the opportunity to link to the converted lead.
-   **Opportunity name (optional):** The name of the opportunity to create.
    -   If not provided, the lead's name will be used.

**Tip: Lead conversion workflow**

A common pattern is to look up an existing contact, create a lead, and then convert it — merging the new lead with the contact found in the lookup step. Here is a three-column setup:

1.  **Lookup record** — Search for an existing contact or account in Salesforce by email address, domain, or another unique identifier. This returns the Contact ID and Account ID if a matching record already exists.
2.  **Create record (conditional)** — Use **Create record** with **Lead** as the Salesforce object to create the lead. Add a [conditional run](conditional-runs.md) tied to the lookup column so this step only fires when no existing contact was found.
3.  **Convert lead** — Map the Lead ID from Step 2 into **Lead ID**. To merge the converted lead with the contact from Step 1 rather than creating a new contact, pass the existing **Contact ID** and **Account ID** from the lookup column into the corresponding optional fields.

## Working with picklist fields

### How picklist fields appear in the Map fields panel

When you add a Salesforce picklist field in **Map fields**, the input looks different from a regular text field:

-   **Text/number fields** show a free-text input with "Type / to Insert column" — click in the box and type `/` to reference a Clay column.
-   **Picklist fields** show a **dropdown** listing the available Salesforce options (for example, "Up" or "Down"). Selecting an option sets a **static value** that every row sends to Salesforce.

**To map a Clay column dynamically** (so each row sends the value from that column), click the **gear icon (⚙️)** to the right of the picklist dropdown. A mode picker appears with two options:

-   **Dropdown** — pick a static value from the Salesforce picklist options (the default)
-   **Text with tokens** — switches to a formula input where you can type `/` to insert a Clay column reference

When using **Text with tokens** mode, the column's value is sent to Salesforce for each row. The value must still exactly match a valid Salesforce picklist option — see format requirements below.

### Single-select picklist (dropdown)

When updating picklist fields in Salesforce from Clay, you need to match the exact format Salesforce expects.

**Format:** Exact text match (case-sensitive)

**Key requirements:**

-   The value in Clay must **exactly match** one of the picklist options in Salesforce
-   Case-sensitive (e.g., `Technology` ≠ `technology`)
-   Use the API value, not the display label

**Example:**

Clay Value: `Technology`

Salesforce Picklist Options: `Technology`, `Healthcare`, `Finance`

✅ This will work

**Important notes:**

-   For unrestricted picklists: If you send a value not in the list, Salesforce creates an "inactive" picklist value
-   For restricted picklists: Invalid values will cause an error
-   Always verify the exact API name in Salesforce field settings

### Multi-select picklist

**Format:** Semicolon-separated values (;)

**Key requirements:**

-   Separate multiple values with semicolons
-   **No spaces after semicolons**
-   Each value must exactly match a Salesforce picklist option (case-sensitive)

**Example:**

Clay Value: `Technology;Healthcare;Finance`

**Important:** Salesforce uses semicolons as delimiters for multi-select picklists, **NOT commas**!

### Common picklist errors

| Error | Cause | Solution |
| --- | --- | --- |
| Bad value for restricted picklist | Text doesn't match picklist | Check exact spelling & case in Salesforce |
| Values not updating | Wrong delimiter used | Use semicolons (;), not commas |
| Field not accepting value | Using display label instead of API name | Verify API name in Salesforce Setup |

### Writing AI-generated values to restricted picklist fields

If you are using an AI column (Claygent or Use AI) to generate values that are then written to a Salesforce restricted picklist via **Update Record**, you may see "bad picklist value" errors even when the output appears correct. AI columns produce free text — a trailing space, different capitalization, or an invisible encoding character is enough for Salesforce to reject the value.

**Fix: use a Select output field to constrain the AI to your exact picklist values**

1.  In your AI column settings, under **Output format**, choose **Fields**.
2.  For the output field that maps to your Salesforce picklist, click the type selector and choose **Select**.
3.  Click **+ Add option** and enter each allowed value exactly as it appears in Salesforce (API name, case, and spacing must match).
4.  The AI will only return one of the defined options, ensuring a character-for-character match every time.

Alternatively, if you are using **JSON Schema** output mode, add an `"enum"` array to the field definition with the exact allowed values:

```json
"industry": {
  "type": "string",
  "description": "Industry classification",
  "enum": ["Technology", "Healthcare", "Finance"]
}
```

Both approaches prevent the AI from producing free-text output that won't match a valid Salesforce restricted picklist option.

### Normalizing enrichment-provided values before writeback

When you enrich records using a data provider — such as Clay's own enrichments, Apollo, ZoomInfo, or Clearbit — the values returned may not match what your Salesforce fields expect. Two common mismatches:

**Picklist taxonomy mismatch**

Enrichment providers use their own industry or category taxonomies, which frequently differ from your Salesforce picklist values. For example, Apollo may return `"information technology & services"` for Industry while your Salesforce restricted picklist only accepts `"Technology"`. Salesforce rejects values that don't exactly match an allowed option.

To fix this, add a formula column or an AI column *after* the enrichment column to translate the enrichment output to the exact Salesforce value before writeback:

-   **Formula column:** Use an `if`/`switch` expression to map each enrichment value to its Salesforce equivalent.
-   **AI column (Claygent or Use AI):** Set the output format to **Fields**, choose **Select** as the field type, and add each allowed Salesforce picklist value as an option. The AI will only return one of the defined options — ensuring an exact match every time.

Map the formula or AI column (not the raw enrichment column) in your **Update Record** or **Create Record** action.

**Revenue range vs. currency field type mismatch**

Salesforce's `AnnualRevenue` field is a **currency (number)** type — it expects a numeric value, not a text string. Many enrichment providers return revenue as a text range: Clay's own CPJ enrichment returns `"$1M-$10M"`, ZoomInfo returns `"$25 mil. - $50 mil."`, and Clearbit's `estimatedAnnualRevenue` field returns `"$10B+"`. Mapping any of these directly to Salesforce's `AnnualRevenue` field fails with a deserialization error — Salesforce cannot convert the text to a number.

To fix this, add a formula column after the enrichment that converts the text range to a single numeric value. Where a provider also returns a separate numeric field (for example, Apollo's `annual_revenue` field returns a number alongside `annual_revenue_printed`), map the numeric field directly instead.

## Batch processing

The `Create record`, `Update record`, and `Upsert object` actions support a **Run in batches** mode. Batch mode is **off by default** — enable it in the action column's **Run settings** to reduce the number of simultaneous Salesforce calls Clay makes.

### How batch mode works

When **Run in batches** is enabled, Clay groups rows and sends them through Salesforce's Composite API in sequential batches (up to 200 records per batch) rather than firing calls for all rows concurrently. This reduces write concurrency, which can help avoid `UNABLE_TO_LOCK_ROW` errors when many rows write to Salesforce records that share a common parent (for example, contacts all belonging to the same Account). For troubleshooting row-lock errors, see [Salesforce integration FAQs](salesforce-integration-faqs.md).

**Benefits:**

-   **Fewer concurrent calls:** Rows are sent in sequential groups rather than all at once
-   **Reduced lock contention:** Useful when bulk-writing to records that share a parent object, such as contacts in the same Account
-   **Individual error handling:** Each record in a batch is processed independently — if one fails, others in the same batch can still succeed

## Best practices

-   **Test before automating:** Start with auto-update disabled when using **Create** or **Update** actions. Test manually with a few rows first before enabling automation.
-   **Begin with lookup records:** Use the free **Lookup records** action first to check for duplicates, enhance data, and screen against suppression lists.
-   **Qualify early:** Use **conditional runs** and free enrichment actions to qualify leads before spending credits on deeper enrichment.
-   **Mind your relationships:** Pay attention to contact-company relationships and duplicates. Plan how to handle unassociated contacts and merge duplicate records to maintain data quality and efficiency.

## FAQs

For troubleshooting connection issues, permissions, OAuth errors, and other common questions, see [Salesforce integration FAQs](https://university.clay.com/docs/salesforce-integration-faqs).