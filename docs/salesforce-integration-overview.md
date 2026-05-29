---
title: Salesforce integration
source_url: https://university.clay.com/docs/salesforce-integration-overview
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
3.  Under `User Sign In`, complete the OAuth sign-in flow in the browser window that appears.

**Tip:** Clay authenticates as whichever Salesforce user is active in the browser during the OAuth flow. If you need to connect as a specific user — for example, a shared integration or service account rather than your personal Salesforce account — sign in to Salesforce as that user before starting the Clay flow. Opening an incognito or private-browser window lets you do this without signing out of your own Salesforce session. For dedicated integration accounts, the **Client Credentials** method below is often a better fit — it requires no browser sign-in and works with Salesforce Integration licenses.

### **Client Credentials (Integration User)**

Connect to Salesforce via Client Credentials for server-to-server access. No browser sign-in is required.

**Setting up in Salesforce**

1.  In Salesforce Setup, search for `External Client App Manager` in Quick Find and select it. Create a new external client app — see [**Salesforce's documentation**](https://help.salesforce.com/s/articleView?id=xcloud.create_a_local_external_client_app.htm&language=en_US&type=5) for full creation steps. Once created, click on your app and select `Edit`.
2.  In the `Settings` tab, enable the flow at the app level:
    -   Under `Flow Enablement`, check `Enable Client Credentials Flow`.
3.  In the `Policies` tab, enable the flow at the org level. This is the setting most commonly missed — if it's off, the flow is blocked regardless of the Settings toggle:
    -   Under `OAuth Flows and External Client App Enhancements`, check `Enable Client Credentials Flow`.
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

### Testing a connection

After adding a Salesforce connection, you can verify it from `Settings` → `Connections`. Click **Test** on any Salesforce connection to confirm it is active. The test result displays the Salesforce user attributed to that connection token — so you can confirm which account Clay will use when making API calls. This is especially helpful for debugging permission issues and for verifying that an integration user is configured correctly.

### **Troubleshooting**

-   **`OAUTH_APPROVAL_ERROR_GENERIC` when connecting via User Sign In**

This error appears during the OAuth flow and is most commonly caused by one of the following:

-   **Integration User or API Only license:** These licenses cannot complete the OAuth flow. Use a full Salesforce user license, or switch to `Client Credentials`.
-   **Connected app not pre-approved:** If connected apps require pre-approval, Salesforce may block Clay. In Salesforce Setup, go to `Connected Apps OAuth Usage` and confirm Clay is not blocked. Set `IP Relaxation` to `Relax IP Restrictions` and `Permitted Users` to `All users may self-authorize`.
-   **SSO enforcement:** If SSO is enforced, the OAuth approval screen may be blocked. Try a non-SSO user, or create a non-SSO service account.
-   **Missing permission:** The user's profile may lack `Approve uninstalled connected apps`. Ask a Salesforce admin to grant it, or connect with a System Administrator account.

### Testing your connection

To verify a Salesforce connection is working — and to confirm which Salesforce user it is authenticated as:

1.  Navigate to `Settings` → `Connections` and select `Salesforce`.
2.  Click the `…` menu next to the connection you want to test.
3.  Select `Test Connection`.

Clay will confirm the connection is valid and display the Salesforce user (by email) that the connection token is attributed to. Because all data access in Clay is scoped to the permissions of that authenticated user, seeing which user is in the seat makes it easy to debug access issues — for example, if objects or fields are missing, you can immediately check whether the displayed user has the right permissions in Salesforce.

### IP allowlisting

If your Salesforce org restricts connections by IP address, you can enable **Use static IP?** when adding or editing your Salesforce connection in Clay. This option is available on **Enterprise plans** and routes all Clay requests through a fixed set of IP addresses.

When enabled, Clay routes requests through one of these IP addresses, which you can allowlist in Salesforce under `Setup` → `Network Access` → `New`:

-   `52.7.81.233`
-   `18.209.121.250`
-   `35.170.109.137`
-   `54.86.28.41`

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

**Related (cross-object) fields are not imported**

Salesforce list views can display fields from related objects — for example, a Contact list view can include `Account Name`, which is stored on the Account object. Clay's list view import only pulls **direct fields** on the selected object; related fields are not imported even if they appear as columns in your Salesforce list view.

To get a related field into Clay, use one of these approaches:

1.  **Add a Lookup record column in Clay (fastest).** Use the **Lookup record** enrichment to query the related object using an ID field that _is_ imported. For example, a Contact import includes `AccountId` — use that to look up the Account record and pull `Name` (or any other Account field you need).
2.  **Create a formula field in Salesforce.** Add a formula text field on the object that copies the related value (for example, a formula field on Contact with the expression `Account.Name`). Once added to the list view in Salesforce, Clay imports it as a direct field. This is useful when you need the value available in multiple Clay tables without a per-row lookup step.

### `Source` Import records from a Salesforce report

**Inputs:**

-   **Report to run:** The report to run in your Salesforce instance.
    -   Only tabular and matrix reports are supported. Salesforce limits reports to a maximum of 2,000 records. If you need to import more than 2,000 records, use the [Salesforce SOQL source](salesforce-soql.md) instead — SOQL queries bypass this cap and support up to 50,000 records per import.
-   **Uniqueness fields:**
    -   Since Salesforce reports lack unique identifiers, select specific fields to identify each row. This prevents duplicate records from appearing when the report updates.
        -   **Important:** If you don't select any fields, Clay will use the entire row content as the unique identifier. This can result in many duplicate entries in your Clay table.
        -   **How deduplication works:** When the report re-syncs, Clay compares each incoming record against your chosen uniqueness field(s). If a record with a matching key already exists in the table, Clay **updates that existing row** with the latest data — it does not create a new row. Only records with no matching key get inserted as new rows.
        -   **Records no longer in the report are not removed:** When the report re-syncs, any records previously imported into your Clay table that no longer appear in the new report run **stay in your table** — they are not deleted automatically. Clay sources are additive only. If you need accounts to be removed from Clay when they fall off the report — for example, to keep a list that reflects accounts qualifying in and out of a segment each day — use [Clay Audiences](audiences.md) instead. With Audiences you connect Salesforce directly and define your criteria as a segment filter; records are added when they match and removed automatically when they no longer qualify.
        -   **Preserving run history / audit logs:** Because re-synced records overwrite the same row, the previous enrichment results and run state are replaced. If you need to keep a history of every sync event, the recommended pattern is to keep your source table deduped on a stable identifier (e.g., `Account.Id`), then add a **Send Table Data** action after your enrichment columns to push a snapshot — including a timestamp column — to a separate history table. This keeps your main table clean while building a full audit trail in the history table. See [Send table data](send-table-data.md) for setup details.

## Enriching data with Salesforce

1.  While in a Clay table, click `Add enrichment` and search for `Salesforce`.
2.  Under `Integrations`, select one of the Salesforce options.
3.  In the modal, you will be asked to `Select Salesforce account`.
    -   If you haven't already connected your Salesforce account, click `+ Add account` and go through authentication.

### `Action` Lookup records via SOQL

Look up records in Salesforce using a custom SOQL query. Use this when the standard **Lookup record** action returns too many matches or when you need to filter on multiple fields at once (e.g., website AND country code).

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

**Tip: Adding contacts or leads to a Salesforce Campaign**

Clay does not have a dedicated "Add to Campaign" action. To add a contact or lead to a Salesforce Campaign, use **Create Record**, select **Campaign Member** as the Salesforce object, and map both the **ContactId** (or **LeadId**) and **CampaignId** fields. If the record is already a campaign member, Salesforce returns a `DUPLICATE_VALUE` error — you can guard against this by first running a **Lookup record** action with "Campaign Member" as the object to check whether the association already exists.

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

**Note on converted leads:** When looking up Lead records, Salesforce retains converted leads (records where `IsConverted = true`) as regular records — they are not deleted, just marked converted and linked to the associated contact and account. The Lookup record action returns these converted leads if they match your search criteria. When you click the CRM link for a converted lead in Clay, Salesforce automatically redirects to the associated contact record, which can make it appear as though a contact was returned instead of a lead. To restrict results to unconverted leads only, use the **Lookup records via SOQL** action and add `IsConverted = false` to the WHERE clause:

```sql
SELECT FIELDS(ALL) FROM Lead WHERE Email = '/Email Column' AND IsConverted = false LIMIT 5
```

**Note: blank search values are silently dropped.** When a row's value for one of your Object Fields is blank or empty, Clay omits that field from the search query entirely. If your lookup has multiple Object Fields and only some of them are blank, the query runs using only the fields that still have values — which can produce unexpected results. For example, if you configure Campaign ID and Lead ID as Object Fields and a row's Lead ID is blank, Clay searches only on Campaign ID and can return up to 5 campaign members for that campaign rather than the specific one tied to that row. If all Object Fields are blank for a row, the action fails with a missing-input error. To prevent unintended lookups on rows with missing values, add a **conditional run** on the lookup column to skip rows where the key search field is empty.

### `Action` Upsert object

Use this action to create a new record or update an existing one.

_Note: In order for upsert to work, you need to have an_ [_external ID_](https://help.salesforce.com/s/articleView?id=000385174&language=en_US&type=1) _on the object._

**External ID value requirements**

Salesforce processes the upsert by placing the external ID value directly in the REST API URL path. Values containing URL-special characters — most commonly forward slashes (`/`) — will cause the upsert to fail with **"Upsert Failed"** and no additional error details.

**Characters to avoid:** `/`, `#`, `?`, `&`, `%`, `+`, and spaces.

**Common example:** A value like `linkedin.com/company/acme-corp` contains forward slashes that Salesforce interprets as URL path separators, causing the upsert to fail.

**Recommended format:** Use only alphanumeric characters, hyphens (`-`), and underscores (`_`). Apply the same sanitized format to the corresponding field in Salesforce so records still match — for example, use `acme-corp` instead of `linkedin.com/company/acme-corp`.

**Inputs:**

-   **Salesforce object:** The object type to look for in your Salesforce.

### `Action` Update record

Use this action to modify existing records in Salesforce.

**Inputs:**

-   **Record ID:** The ID of the record to update.
-   **Salesforce object:** The object type to look for in your Salesforce.
-   **Ignore blank values (optional):** When enabled, blank values from Clay will be ignored.
-   **Disable auto-assignment rules (optional):** When enabled, Salesforce will not apply lead and contact assignment rules when the record is updated. Enable this setting if you do not want your Salesforce assignment rules to fire when Clay updates a record.

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

## Working with picklist fields

When updating picklist fields in Salesforce from Clay, you need to match the exact format Salesforce expects.

### Single-select picklist (dropdown)

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

## Batch processing

The `Create record`, `Update record`, and `Upsert object` actions support batch mode, which processes multiple records simultaneously for improved performance with large datasets. Batch mode is automatically enabled when running these actions across multiple rows in your Clay table. No additional configuration is required.

### How batch mode works

When you run these actions on multiple rows in Clay, they automatically use Salesforce's Composite API to process records in batches rather than one at a time.

**Benefits:**

-   **Faster execution:** Process multiple records in a single API call
-   **Better performance:** Reduced overhead when working with hundreds or thousands of records
-   **Individual error handling:** Each record in the batch is processed independently—if one fails, others can still succeed

## Best practices

-   **Test before automating:** Start with auto-update disabled when using **Create** or **Update** actions. Test manually with a few rows first before enabling automation.
-   **Begin with lookup records:** Use the free **Lookup records** action first to check for duplicates, enhance data, and screen against suppression lists.
-   **Qualify early:** Use **conditional runs** and free enrichment actions to qualify leads before spending credits on deeper enrichment.
-   **Mind your relationships:** Pay attention to contact-company relationships and duplicates. Plan how to handle unassociated contacts and merge duplicate records to maintain data quality and efficiency.

## FAQs

For troubleshooting connection issues, permissions, OAuth errors, and other common questions, see [Salesforce integration FAQs](https://university.clay.com/docs/salesforce-integration-faqs).
