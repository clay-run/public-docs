---
title: Marketo integration
description: Create, update, and lookup Marketo objects directly from Clay.
last_synced: 2026-04-26T01:40:20.477Z
---

# Marketo integration

Create, update, and lookup Marketo objects directly from Clay.

Marketo is a marketing automation platform for managing leads and campaigns. With this integration, you can create, update, and look up Marketo objects directly from Clay, and connect Marketo via webhook to enrich inbound leads in real time.

## Enriching data with Marketo

1.  While in a Clay table, click `Add enrichment` and search for `Marketo`.
2.  Under `Integrations`, select one of the Marketo options.
3.  In the modal, you will be asked to `Select Marketo account`.
    -   If you haven't already connected your Marketo account, click `+ Add account` and go through authentication.

**Note:** When setting up a role in Marketo to connect with Clay, the role requires two minimum permissions: `Read-Write Schema Standard Field` and `Read-Write Schema Custom Field`. You will also need to grant access to any objects you'd like to work with in Clay (e.g., Leads, Companies). You can edit the role later to include other objects.

### `Action` Create object

Use this action to create a new object in Marketo.

**Inputs**

Required:

-   Object type: The Marketo object type you want to create. Select `Person` (leads) or `Company`.
-   Fields: Dynamic fields that appear after selecting an object type. For `Person`, `Email` is required. For `Company`, `Company Name` is required.

Optional:

-   Fields: All remaining fields for the selected object type, populated dynamically from your Marketo schema.

### `Action` Lookup object

Use this action to look up an existing object in Marketo.

**Inputs**

Required:

-   Object type: The Marketo object type you want to look up. Select `Person` (leads) or `Company`.
-   Filter type: The field to filter on, populated dynamically from the searchable fields for the selected object type.
-   Filter values: The value(s) to filter on. Accepts a comma-separated list. Matching is case-insensitive and uses OR logic.

Optional:

-   Remove blank values from results: When enabled, blank values are removed from the returned object — helpful for reducing response size. Defaults to on.

### `Action` Update object

Use this action to update an existing object in Marketo.

**Inputs**

Required:

-   Object type: The Marketo object type you want to update. Select `Person` (leads) or `Company`.
-   Marketo object ID: The ID of the Marketo object to update. You can retrieve this using the `Create object` or `Lookup object` action.

Optional:

-   Ignore blank values: When enabled, blank values from Clay will be ignored in Marketo. When disabled, blank values will overwrite existing Marketo field values. Defaults to on.
-   Fields: The fields to update, populated dynamically from your Marketo schema.

### Run settings

-   Auto-update: Recommended when writing enriched data back to Marketo, so that new or updated rows are automatically pushed.
-   Run in batches: When enabled, groups up to 300 rows into a single API request instead of sending one request per row. This reduces the total number of API calls Clay makes to Marketo and is recommended if you are hitting Marketo's 606 rate limit error. Available for the Create object and Update object actions.
-   Only run if: The enrichment will only run if conditions are met. ([**Learn more about conditional formulas here!**](https://www.clay.com/university/lesson/ai-formulas-conditional-runs-clay-101))

## Common workflows

### Check prior Marketo outreach before adding leads to a new cadence

Use the Marketo **Lookup object** action to check a lead's existing Marketo record — including any status, campaign, or custom outreach fields your Marketo instance tracks — before adding them to a new email sequence.

1.  Add a Marketo enrichment to your Clay table and select **Lookup object**.
2.  Set **Object type** to `Person`.
3.  Set **Filter type** to `Email`.
4.  Set **Filter values** to the email column in your table.

The action returns the lead's full Marketo record. You can use the returned fields — such as a lead status or last-contacted date — in a Clay formula or an **Only run if** condition to skip leads who have already been reached out to.

If expected custom fields are missing from the results, see [Custom fields are missing from Lookup object results](#custom-fields-are-missing-from-lookup-object-results) below.

### Write outreach results back to a Marketo lead after a cadence

Use the Marketo **Update object** action to stamp a lead as contacted or update a field in Marketo once emails have gone out from your cadence tool.

The Update object action matches on the Marketo internal ID (not email). If your table does not already have Marketo IDs, run a **Lookup object** (filtered by email) first to retrieve them.

1.  Add a Marketo **Lookup object** enrichment filtered by email to get each lead's Marketo ID, if you don't already have it.
2.  Add a Marketo **Update object** enrichment.
3.  Set **Object type** to `Person`.
4.  Set **Marketo object ID** to the Marketo ID column from step 1.
5.  Under **Fields**, select the field to update — for example, a lead status field or a custom "Contacted" field — and map the value from your table.
6.  Enable **Auto-update** in Run settings so that rows are pushed back to Marketo automatically as cadence results come in.

## Connecting Marketo via webhook

Use webhooks to send data from Marketo to Clay for real-time lead enrichment. This is ideal for capturing inbound leads as they arrive — such as form fills, demo requests, or other lead events. After enrichment, you can use the Marketo enrichment actions above to write the enriched data back to Marketo.

1.  **Copy the webhook URL from Clay.** In a new or existing Clay table, locate the `Webhook URL` option and copy it. This is the endpoint Marketo will POST lead data to.
2.  **Go to the Admin area in Marketo.** Navigate to the `Admin` section in your Marketo instance.
3.  **Open Webhooks.** In the Admin area, click `Webhooks` in the left-hand menu.
4.  **Create a new webhook.** Click `New webhook` to begin configuration.
5.  **Configure the webhook.** Fill in the following details:
    -   `URL`: The webhook URL copied in step 1.
    -   `Header`: Add a custom header with the key `Content-Type` and the value `application/json`.
    -   `Request type`: POST
    -   `Request token encoding`: None
    -   `Response format`: JSON
    -   `Payload template`: Use the JSON template below, customizing fields as needed.

`{ "id": "{{lead.Id}}", "first_name": "{{lead.FirstName}}", "last_name": "{{lead.LastName}}", "email": "{{lead.EmailAddress}}", "title": "{{lead.JobTitle}}", "company": "{{lead.CompanyName}}", "industry": "{{lead.Industry}}", "country_code": "{{lead.Country}}" }`

## Troubleshooting

### Custom fields are missing from Lookup object results

Clay builds the field list for the Lookup object action from Marketo's schema API. The schema API only returns fields that your API user's role has permission to read. If custom fields are missing from the lookup results, the API user's Marketo role likely lacks the required schema permissions:

1.  In Marketo, go to **Admin** → **Users & Roles**.
2.  Open the role assigned to your API user.
3.  Confirm that both **Read-Write Schema Standard Field** and **Read-Write Schema Custom Field** are enabled for that role.

Once the role permissions are updated, the schema API will return the accessible fields and they will appear in future Clay lookup results.

### Field values containing special characters are split incorrectly in Clay

If a lead field value contains an ampersand (`&`) — such as a job title like "VP & Head of Sales" — and you're using a form-encoded payload template in Marketo, the `&` will be interpreted as a field separator, causing the value to be split across multiple fields in Clay. To avoid this, use a JSON-formatted payload template (as shown in step 5 above). JSON handles special characters correctly and will not split values on `&`.

### Webhook records containing multi-line text aren't arriving in Clay

If a Marketo lead field contains paragraph-style text with line breaks — such as a "Webform Comments" or "Notes" field from a form submission — those records may not arrive in Clay at all even though Marketo reports a successful delivery. The cause is that a literal newline character inside a JSON string value produces invalid JSON. Clay's webhook requires a valid JSON payload; a malformed request is rejected and the record is dropped.

**Solution: use Marketo's JSON token encoding**

In your Marketo webhook settings, set `Request Token Encoding` to **JSON**. When JSON encoding is selected, Marketo automatically quotes and escapes each token value before building the payload — turning line breaks into `\n`, escaping internal quotes, and handling other characters — so the resulting JSON is always valid regardless of what the contact typed.

**Important:** When `Request Token Encoding` is set to JSON, Marketo adds the surrounding double quotes around each string value automatically. Do **not** also wrap token values in manual quotes in your template — doing so produces double-quoted strings (`""value""`) that break the JSON. Keep quotes only around the field keys, not the token values:

Correct (no manual quotes around token values — JSON encoding adds them):

```
{
  "id": {{lead.Id}},
  "email": {{lead.EmailAddress}},
  "form_comments": {{lead.WebformComments}}
}
```

Incorrect (manual quotes combined with JSON encoding produces invalid JSON):

```
{
  "id": "{{lead.Id}}",
  "email": "{{lead.EmailAddress}}",
  "form_comments": "{{lead.WebformComments}}"
}
```

Keep `Response type` set to JSON. With JSON encoding enabled, Marketo handles all escaping — multi-line comments, embedded quotes, ampersands, and line breaks all come through as valid JSON string values.

### Marketo 606 rate limit error

Error 606 (`Max rate limit '100' exceeded with in '20' secs`) means Marketo received more than 100 API calls within a 20-second window. To reduce call volume, enable **Run in batches** in the affected action's Run settings. With batching enabled, Clay groups up to 300 rows into a single POST request instead of one call per row, significantly reducing the number of API calls and helping avoid this error.

### Clay returns a 429 error when Marketo sends leads via webhook

When a Marketo smart campaign or Flow Action triggers for many leads at once, Marketo fires a separate HTTP POST to Clay's webhook endpoint for each lead. Clay's webhook endpoint accepts **10 requests per second per workspace**, with a burst of up to 20. When more than 20 requests arrive in rapid succession, Clay returns a `429 Too Many Requests` error — dropped records are **not** queued or retried by Clay, so those leads will not appear in your table.

There is no "batch size" setting for Clay webhooks: each POST creates exactly one row. The practical limit is how many leads Marketo fires within a single second. To avoid data loss, add a **Wait** step between leads in your Marketo campaign flow to pace requests to 10 or fewer per second. If your workflow consistently requires a higher throughput, contact Clay support to request a rate limit increase for your workspace.

For full details on Clay's webhook rate limits and retry guidance, see [Webhooks in Clay](https://www.clay.com/university/guide/webhook-integration-guide).
