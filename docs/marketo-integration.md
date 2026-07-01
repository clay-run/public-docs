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

Clay builds the field list for the Lookup object action from Marketo's schema API, which only returns fields that have **API access** enabled. If a custom field doesn't appear in the lookup results, it likely isn't exposed through Marketo's API:

1.  In Marketo, go to **Admin** → **Field Management**.
2.  Find the missing field and open its settings.
3.  Confirm that **API access** is enabled for that field.

Once API access is enabled, the field will be included in Marketo's schema response and returned in future Clay lookup results.

### Field values containing special characters are split incorrectly in Clay

If a lead field value contains an ampersand (`&`) — such as a job title like "VP & Head of Sales" — and you're using a form-encoded payload template in Marketo, the `&` will be interpreted as a field separator, causing the value to be split across multiple fields in Clay. To avoid this, use a JSON-formatted payload template (as shown in step 5 above). JSON handles special characters correctly and will not split values on `&`.

### Marketo 606 rate limit error

Error 606 (`Max rate limit '100' exceeded with in '20' secs`) means Marketo received more than 100 API calls within a 20-second window. To reduce call volume, enable **Run in batches** in the affected action's Run settings. With batching enabled, Clay groups up to 300 rows into a single POST request instead of one call per row, significantly reducing the number of API calls and helping avoid this error.

### Clay returns a 429 error when Marketo sends leads via webhook

When a Marketo smart campaign or Flow Action triggers for many leads at once, Marketo fires a separate HTTP POST to Clay's webhook endpoint for each lead. Clay's webhook endpoint accepts **10 requests per second per workspace**, with a burst of up to 20. When more than 20 requests arrive in rapid succession, Clay returns a `429 Too Many Requests` error — dropped records are **not** queued or retried by Clay, so those leads will not appear in your table.

There is no "batch size" setting for Clay webhooks: each POST creates exactly one row. The practical limit is how many leads Marketo fires within a single second. To avoid data loss, add a **Wait** step between leads in your Marketo campaign flow to pace requests to 10 or fewer per second. If your workflow consistently requires a higher throughput, contact Clay support to request a rate limit increase for your workspace.

For full details on Clay's webhook rate limits and retry guidance, see [Webhooks in Clay](https://www.clay.com/university/guide/webhook-integration-guide).
