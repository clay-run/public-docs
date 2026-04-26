---
title: Salesforce integration
source_url: https://university.clay.com/docs/salesforce-integration-overview
last_synced: 2026-04-26T01:40:35.308Z
upstream_hash: c40cc0a861c4e1af36565daebd41ff5e3d0ce7d66f5b61350cff95e7f2f41859
---

# Salesforce integration

Cloud-based customer relationship management software.

Salesforce is a customer relationship management (CRM) platform that helps businesses manage their customer data and relationships. This integration lets you sync your Salesforce data with Clay to streamline your workflow.

## Connecting to Salesforce

Clay supports two methods for authenticating your Salesforce account. You can choose the one that fits your organization's setup when adding a new connection or when reconnecting an existing one.

-   **User Sign In** — the default method. You sign in as a Salesforce user via an OAuth browser prompt.
-   **Client Credentials** — a server-to-server method (also referred to as the Integration User flow). No browser sign-in is required; instead, you supply credentials from an external client app configured in your Salesforce org.

### User Sign In

Connect via OAuth as a Salesforce user.

1.  In the home sidebar, click `Settings` → `Connections`.
2.  Click `Add connection` and search for `Salesforce`.
3.  Under `User Sign In`, complete the OAuth sign-in flow in the browser window that appears.

### Client Credentials (Integration User)

Connect to Salesforce via Client Credentials for server-to-server access. No browser sign-in is required.

You will need to set up an external client app in Salesforce and enable the Client Credentials flow before connecting in Clay.

1.  In the home sidebar, click `Settings` → `Connections`.
2.  Click `Add connection` and search for `Salesforce`.
3.  Under `Client Credentials` fill in the following fields:
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

### `Source` Import records from a Salesforce report

**Inputs:**

-   **Report to run:** The report to run in your Salesforce instance.
    -   Only tabular and matrix reports are supported. Salesforce limits reports to a maximum of 2,000 records.
-   **Uniqueness fields:**
    -   Since Salesforce reports lack unique identifiers, select specific fields to identify each row. This prevents duplicate records from appearing when the report updates.
        -   **Important:** If you don't select any fields, Clay will use the entire row content as the unique identifier. This can result in many duplicate entries in your Clay table.

## Enriching data with Salesforce

1.  While in a Clay table, click `Add enrichment` and search for `Salesforce`.
2.  Under `Integrations`, select one of the Salesforce options.
3.  In the modal, you will be asked to `Select Salesforce account`.
    -   If you haven't already connected your Salesforce account, click `+ Add account` and go through authentication.

### `Action` Lookup records via SOQL

Look up records in Salesforce using a SOQL query.

**Inputs:**

-   **SOQL query:** For more information about SOQL and Salesforce, [check out their documentation](https://developer.salesforce.com/docs/atlas.en-us.soql_sosl.meta/soql_sosl/sforce_api_calls_soql.htm).

### `Action` Create record

Use this action to create a new record in Salesforce.

**Inputs:**

-   **Salesforce object:** The object type to look for in your Salesforce.
-   **Duplicate rule override:** When enabled and you have a [duplicate rule](https://help.salesforce.com/s/articleView?id=sf.duplicate_rules_map_of_reference.htm&type=5), Clay will bypass the rule and create a new record, even if it duplicates an existing one.

### `Action` Lookup record

Use this action to find existing records in Salesforce.

**Inputs:**

-   **Salesforce object:** The object type to look for in your Salesforce.
-   **Exact match? (optional):** When enabled, finds exact matches across all search fields.

### `Action` Upsert object

Use this action to create a new record or update an existing one.

_Note: In order for upsert to work, you need to have an_ [_external ID_](https://help.salesforce.com/s/articleView?id=000385174&language=en_US&type=1) _on the object._

**Inputs:**

-   **Salesforce object:** The object type to look for in your Salesforce.

### `Action` Update record

Use this action to modify existing records in Salesforce.

**Inputs:**

-   **Record ID:** The ID of the record to update.
-   **Salesforce object:** The object type to look for in your Salesforce.
-   **Ignore blank values (optional):** When enabled, blank values from Clay will be ignored.

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
