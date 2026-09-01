---
title: Webhooks in Clay
description: Real-time data updates enabling application integrations and
  automated workflows.
last_synced: 2026-04-26T01:40:54.241Z
---

# Webhooks in Clay

Real-time data updates enabling application integrations and automated workflows.

Webhooks enable Clay to automatically receive data from other applications through HTTP POST requests in JSON format whenever specific events occur.

Your table updates instantly with new data, eliminating manual entry. This feature is particularly valuable for real-time updates, such as when adding new leads or modifying records based on external triggers.

**Plan availability:** Webhooks are available on **Growth** and **Enterprise** plans.

## **Creating a table with webhook**

1.  In a workbook, click `+ Add` at the bottom.
2.  Search for `Webhooks` and click `Monitor webhook`.
3.  Copy the URL/cURL.
    -   **URL:** Paste this URL into the application sending data to Clay. This URL is where your data will be sent.
    -   **cURL:** Paste the cURL command into your command line to send data directly to Clay.
4.  Optionally, add authentication token. To secure your webhook, you can include an authentication token in the header of your request.
    -   Make sure to copy the token immediately, as you can only access authentication tokens once.

## Limits

The following limits apply to all webhook sources in your workspace:

| Limit | Value |
|---|---|
| Throughput | 10 requests/second, burst up to 20 requests |
| Rate limit scope | Per workspace — all active webhook sources share this budget |
| Max payload size | 100 KB per request |
| Max submissions | 50,000 per webhook source |

**Throughput:** Clay accepts up to 10 incoming HTTP requests per second per workspace. A burst of up to 20 requests is allowed when capacity is available — after a burst, throughput returns to the sustained 10-per-second rate. Each POST counts as one request against this limit, regardless of how many fields or records the payload contains. Exceeding the limit returns a `429 Too Many Requests` response with a `Retry-After: 1` header and this body: `{"type":"TooManyRequests","message":"Too many requests. Wait a bit and retry.","details":null}` — records are dropped and Clay does not queue them. For event-driven integrations where you cannot control the send rate directly (for example, a webhook triggered by a form submission), implement retry logic with exponential backoff on your sending system: wait at least 1 second after receiving a `429` before retrying. To avoid data loss when sending in bulk, pace your requests to 10 per second or fewer. Multiple active webhook sources in the same workspace share this limit.

**Need a higher throughput limit?** If 10 requests/second is too restrictive for your workflow, contact Clay support to request an increase — rate limits can be adjusted for your workspace on request.

**Payload size:** Each HTTP POST to Clay's webhook endpoint must be 100 KB or smaller.

**Submission limit:** Each webhook source accepts up to 50,000 submissions. This is a cumulative lifetime count — every accepted submission increments the counter, and neither deleting nor archiving rows from the table reduces it. Once you reach this limit, Clay returns a `403 Record limit reached for webhook` error and you'll need to create a new webhook to continue receiving data.

**Enterprise Plan — run a webhook indefinitely:** Enable [auto-delete](https://www.clay.com/university/guide/auto-delete) (also called passthrough tables). When passthrough mode is active, the webhook source takes a separate code path that **bypasses the 50,000 submission limit entirely** — a single webhook URL can keep accepting data indefinitely without ever hitting the cap. This is the recommended approach for automated enrichment pipelines. Auto-delete is available on Enterprise plans and only works for webhook, send-table-data, and signal sources. Learn more in [table management settings](https://www.clay.com/university/guide/table-management-settings).

## Request body format

**One record per POST:** Each HTTP POST to Clay's webhook endpoint creates exactly one new row in your table — Clay does not split array payloads. If you send a JSON array (`[{...}, {...}]`), the entire array becomes the data for a single row rather than one row per element.

**JSON shape:** Any valid JSON object structure is accepted. Both nested objects and flat key structures work — Clay creates columns based on whatever top-level keys you send:

- Nested: `{"contact": {"name": "Jane", "email": "jane@example.com"}}`
- Flat: `{"contact.name": "Jane", "contact.email": "jane@example.com"}`

## Connecting middleware tools

Clay's webhook URL works with any platform that can send HTTP POST requests in JSON format — including automation and middleware tools like Workato, Make, and n8n. These are not native Clay integrations, but they connect to Clay using the same webhook and HTTP API features.

**Note:** Clay webhooks accept structured JSON payloads only. File attachments and binary data are not supported.

### Send data from a middleware tool into Clay

1. In your Clay workbook, create a table using **Monitor webhook** as the source (see [Creating a table with webhook](#creating-a-table-with-webhook)).
2. Copy the webhook URL Clay generates.
3. In your middleware tool, configure your flow or recipe to POST JSON data to that Clay webhook URL.

### Send enriched data from Clay to a middleware tool

1. In your middleware tool, set up a webhook trigger and copy the endpoint URL it provides.
2. In your Clay table, add an **HTTP API** enrichment column.
3. Set the method to **POST** and paste the middleware endpoint URL.
4. Configure the JSON request body to include the Clay columns you want to send.

For a complete example using Zapier, see [Send Clay data to Zapier](https://www.clay.com/university/guide/clay-to-zapier).

**Rate limits and retry for outbound calls:** Clay applies a default rate limit of **100 requests per second per workspace** on outbound HTTP API enrichment calls. If the receiving service enforces a stricter limit, configure the **Custom rate limit** setting inside your HTTP API column settings to match it. By default, the HTTP API enrichment **retries failed requests automatically** when the receiving service returns a `408`, `413`, or `429` status code, or a network-level connection error — up to 1 retry by default, configurable up to 5. For details on both settings, see the [HTTP API guide](https://www.clay.com/university/guide/http-api-integration-overview).

**Note:** The 10 requests/second throughput limit in the [Limits](#limits) section above applies only to data *arriving at* Clay through a webhook source. It does not apply to outbound HTTP API calls your table makes to external services.

## FAQs

### How can I see webhook logs?

Clay does not have a built-in webhook log UI. The two places to check webhook activity are:

- **Your webhook table in Clay:** Every payload Clay successfully receives creates a row in your webhook table immediately. The row count in the table is your record of accepted deliveries — if a row exists, Clay received and stored that payload. To see all rows, make sure no filter is active (look for a number badge on the filter icon in the table toolbar).

- **Your sending system's delivery logs:** For delivery history, retry records, or to investigate failed attempts, check the logs in the tool sending the webhook (for example, Zapier, Make, HubSpot, Salesforce, or a custom script). These systems typically maintain a delivery history where you can see each request's status code and optionally replay events that failed.

**Note:** Clay does not queue or retry incoming webhook requests. If a payload was rejected (for example, because of a `429` rate limit error or a `400` bad request), it is not stored and no row appears in the table. See [Why aren't any rows arriving in my webhook table?](#why-arent-any-rows-arriving-in-my-webhook-table) for troubleshooting.

### Why does my webhook source show a higher row count than my table?

The webhook source node in the workbook view shows the **total number of records stored by the source** since it was created. This count increases with every accepted payload and does not decrease when you delete rows from the table.

The table node shows the **current number of rows** in your table.

So if your source displays more rows than your table (for example, 162 vs. 92), the difference is typically caused by one or both of the following:

-   **Deleted rows.** Rows that were ingested at some point but later deleted from the table are still counted by the source. Deleting a row from the table does not reduce the source count.
-   **Table filters.** If a filter is active on your table, only the rows matching that filter are shown in the table count. The source count always reflects all stored records, regardless of any filters.

**Note:** Records that Clay rejected with a `429` rate limit error were never stored and do not appear in either count. See the [Limits](#limits) section above for guidance on keeping requests within the 10/second throughput limit to avoid dropped records.

### My webhook is sending data successfully but new rows aren't visible in my table

If your external tool reports a successful delivery (for example, a `200 OK` response from Clay's webhook endpoint) but new rows aren't showing up in your table view, the most likely cause is an **active view filter** hiding the incoming rows.

Filters in Clay are display-only — they control which rows appear in the current view, but they do not block or drop incoming webhook data. Every accepted payload creates a row in your table regardless of any active filters. Rows that don't match the filter criteria are still stored; they simply don't appear in the filtered view.

**To check for an active filter:** Look at the table toolbar — when a filter is active, you'll see a number badge on the filter icon and the row count will display as **X/Y rows**, where X is the filtered count and Y is the total. Open the filter panel and click **Clear filters** to remove all active filters and see every row.

If you clear the filters and the expected rows still don't appear, see [Why aren't any rows arriving in my webhook table?](#why-arent-any-rows-arriving-in-my-webhook-table) for configuration-level troubleshooting.

### Why aren't any rows arriving in my webhook table?

If your webhook isn't creating rows — even on a brand-new webhook that has never received a submission — check these common causes:

1. **Missing `Content-Type: application/json` header** — Clay requires this header on every request. Without it, Clay rejects the request with a `400 Bad Request` error and no row is created. Make sure every request includes:

   ```
   -H "Content-Type: application/json"
   ```

2. **Incorrect URL** — Confirm you copied the full webhook endpoint URL from the **Monitor webhook** section in your table source settings (not a partial URL or the cURL command itself).

3. **Missing or wrong authentication token** — If you added an auth token when creating the webhook, it must be included in every request as a header. Clay returns `401 Unauthorized` when the token is absent or does not match. The token is only displayed once at creation — if you didn't copy it, you'll need to delete and recreate the webhook to generate a new one.

4. **Submission limit reached** — See the [Limits](#limits) section. Once a webhook source hits 50,000 submissions, Clay returns a `403 Record limit reached for webhook` error and stops creating rows. This limit is cumulative — it counts all submissions since the webhook was created, and neither deleting nor archiving rows resets it. **Enterprise plan:** Enable [auto-delete](https://www.clay.com/university/guide/auto-delete) to bypass this limit entirely — when passthrough mode is active, the 50,000 cap is skipped and the webhook can accept data indefinitely.

**Quick isolation test:** To confirm whether the issue is in your request or on Clay's side, try the simplest possible payload:

```
curl -X POST YOUR_CLAY_WEBHOOK_URL \
  -H "Content-Type: application/json" \
  -d '{"test": "hello"}'
```

If a row appears in your table, the issue is in your original request's formatting, headers, or auth token. If no row appears on a brand-new webhook, contact support.

### What HTTP status codes does Clay's webhook endpoint return?

Clay's webhook endpoint returns the following status codes:

| Status code | Meaning | What to do |
|---|---|---|
| `200 OK` or `202 Accepted` | Request accepted; row created successfully | No action needed — treat any `2xx` as success |
| `400 Bad Request` | Invalid payload — `Content-Type: application/json` header is missing, the body is not valid JSON, or the payload exceeds 100 KB | Fix the request format and resend |
| `401 Unauthorized` | Auth token is missing or does not match | Verify you are sending the correct token in the `x-clay-webhook-auth` request header |
| `403 Forbidden` | Webhook source has reached the 50,000-submission limit | Create a new webhook source, or enable [auto-delete](https://www.clay.com/university/guide/auto-delete) on an Enterprise plan to bypass this limit |
| `429 Too Many Requests` | Workspace-level throughput limit exceeded (10 requests/second) | Retry after the value in the `Retry-After` response header, using exponential backoff |

Only a `2xx` response guarantees that a row was created in your table. Any other status code means no row was created and no credits were consumed.

### Can I restrict webhook access to specific IP addresses?

No — IP-based access restrictions are not available for webhook sources. The authentication token is the sole security layer for your webhook endpoint. To keep your webhook secure:

- Store the token in a secrets manager rather than hardcoding it.
- Rotate the token immediately if you suspect it has been leaked — rotating it invalidates the old token right away.

To rotate the token, open the webhook source settings in your Clay table and generate a new one. Update any external systems that send to this webhook with the new token before retiring the old one.

### How can I tell which webhook source a row came from?

Clay records which webhook source sent each row at ingestion time, so you can filter the table by source without any extra setup.

**Note:** The **Webhook** filter field only appears in the filter panel if this table has at least one webhook source directly connected to it. If you open the filter panel and don't see a Webhook field, this table has no webhook source attached — rows may be arriving from another Clay table (via Send Table Data) that itself has a webhook source.

**To filter by webhook source:**

1. Open the filter panel (click the filter icon in the table toolbar).
2. Set the field to **Webhook**, the condition to **is from source**, then pick a source from the dropdown. The dropdown lists every webhook source connected to this table by name.
3. The table now shows only the rows that arrived from that source. Switch the dropdown to a different source to see its rows instead.

**To show the source on each row as a column (optional):** Add a field to the payloads you send — for example, `"source": "webhook_a"`. That field will arrive as its own column in the table, so you can see the source directly on every row without needing to filter.

### How do I find which table a webhook URL belongs to?

There is no customer-facing search to look up a Clay table by its webhook URL. If you have a webhook URL from an external system and need to identify which Clay table it's connected to, contact Clay support with the URL — the team can look it up on your behalf.

**Tip:** To avoid this situation in the future, give each webhook table a descriptive name when you create it (for example, "HubSpot MQL ingest" or "Salesforce lead flow"). Since every table generates a unique webhook URL, a clear name makes it easy to match a URL back to the right table later.

### What happens to my webhook URL if I duplicate a table?

When you duplicate a table that has a webhook source, Clay generates a **brand new, unique webhook URL** for the duplicate. The original table's URL continues working as before — it is not affected by the duplication.

Because the duplicate has a different URL, any external system currently sending data to the original table will not automatically send to the new table. To start receiving data in the duplicate, update your sending system (for example, Zapier, Make, a custom script, or another tool) to POST to the new URL.

To find the new webhook URL: open the duplicated table, click the webhook source column, and copy the URL shown there.

### Does Clay prevent the same webhook record from being processed more than once?

**No — unlike CRM sources, webhooks do not deduplicate by record identity.** Every HTTP POST creates a new row, regardless of whether identical data already exists in the table. Clay assigns each incoming payload a fresh unique identifier, so sending the same contact or event a second time will create a second row and trigger enrichments again.

This is different from CRM sources such as HubSpot and Salesforce, which track every record they have ever imported and automatically skip any record they have already seen — even if you delete the row from the table.

**To prevent the same record from being enriched multiple times,** enable [auto-dedupe](https://www.clay.com/university/guide/table-management-settings#auto-dedupe) on a column containing a unique identifier for your records (such as an email address or a CRM contact ID). When a second submission arrives with the same value in that column, auto-dedupe detects and removes the duplicate row.

**Note:** Auto-dedupe may not catch duplicates when two payloads arrive within milliseconds of each other. See the [simultaneous insert limitation](https://www.clay.com/university/guide/table-management-settings#auto-dedupe) in the auto-dedupe docs for details and workarounds.

### Why are my credits being consumed faster than expected?

When Auto-run is enabled on a table (the default for new tables), each new row that arrives automatically triggers your enrichment columns to run — consuming credits for every row processed. A webhook that receives data at high frequency can therefore drive rapid credit consumption: every incoming payload creates a new row, and Auto-run immediately queues and executes enrichments on that row.

**To stop or slow credit consumption from a webhook table:**

- **Disable table-level Auto-run** — Open table settings (click the `⛭` icon in the toolbar, or click the table name → **Run Settings**), then toggle **Auto-run** off. Enrichments stop running automatically; new rows from the webhook continue arriving but are not enriched until you trigger them manually. When you're ready to process the accumulated rows, re-enable Auto-run and choose **Update cells**, or run columns manually from the column header.
- **Disable Auto-run on specific columns** — In **Edit column → Run settings**, toggle Auto-run off for any enrichment column you don't want firing on every new row. This lets you keep some enrichments automated while pausing others.
- **Add a run condition** — In **Edit column → Run settings**, enable **Only run if** and set a condition (for example, `Email is not empty`). The enrichment only fires when the condition is met, skipping rows that don't qualify and saving credits on those rows.
- **Pause the webhook source itself** — Turning off Auto-run does **not** stop the webhook from receiving new rows — the webhook source and Auto-run operate independently. To stop new rows from arriving entirely, disable the webhook source in your sending system.

See [Auto-run](auto-run.md) for full details on table-level and column-level controls, and [Ways to save Clay credits](clay-credit-conservation.md) for additional cost-management strategies.

### Can Clay replay webhook events that were acknowledged but not processed?

No — Clay does not have a built-in replay function for webhook events. Once Clay returns a `200 OK` for an incoming payload, that acknowledgment is final. There is no admin endpoint, UI control, or automatic retry that can reprocess or re-deliver those events from within Clay.

To recover events that were acknowledged by Clay but did not appear as rows in your table, you will need to **re-trigger them from your source system's delivery logs**. Most webhook senders (HubSpot, Zapier, Make, Salesforce, and others) maintain a delivery history where you can replay or resend individual events. Check your source system's documentation for how to replay past webhook deliveries.

**To prevent data loss going forward,** pace requests within Clay's [throughput limits](#limits) and ensure your source system implements retry logic with exponential backoff for `429` responses.

### What happens when I map a webhook field to an existing column — and why did my data disappear?

When you click a cell in your webhook column, open **Cell details**, hover over a field, and select **Add as column → Map to an existing column**, Clay changes the destination column's formula to pull from the webhook source. What happens next depends on what was already in that column:

-   **Manually-entered data** (typed directly or imported from a CSV): Clay shows a "Data overwrite" warning before proceeding. If you confirm, all existing values in that column are permanently replaced — the column becomes formula-driven by the webhook field, and rows that didn't arrive via the webhook will show as empty.
-   **Enrichment-based data** (already driven by an enrichment formula): No overwrite occurs. Clay appends the webhook source as a fallback, so the column formula becomes `{{EnrichmentResult}} || {{WebhookField}}`. Existing enrichment-based values are preserved; the webhook fills in where the enrichment is empty.

**To keep existing data while also bringing in webhook data,** don't map to the original column. Instead:

1.  Use **Add as column → Create new column** to extract the webhook field into a separate new column (for example, "Email from webhook").
2.  Add a [Merge column](https://university.clay.com/docs/table-columns-overview#merge-columns) that references both the original column and the new webhook column — it returns the first non-empty value per row, preserving your original data for older rows while populating from the webhook for new arrivals.

**Note:** Clay's Table Versioning feature can restore a table's column schema and formula configuration from a previous snapshot, but it cannot recover lost manually-entered or CSV-imported cell data values. If you confirmed the overwrite and lost that underlying data, re-import the original source and use the approach above going forward.

### A webhook field isn't showing in the "/" picker when I write a Claygent or Use AI prompt

When you type `/` in a Claygent or Use AI column prompt to reference your webhook data, Clay discovers available sub-fields by sampling rows from the top of the current table view. If a field was added to your webhook payloads after some records had already been received — for example, you started including an `emailDomain` key in your payloads a week after the first submissions arrived — that field may not appear in the `/` picker because the rows sampled (which are near the top of the view) don't contain it yet.

You can confirm this is the case if the field appears in the webhook column's **Setup mapping** panel (click the webhook column header → **Edit source** → **Setup mapping**) but not in the `/` picker when writing a prompt.

**To make the field appear in the picker:**

1.  Sort or filter the table view so that rows containing the missing field appear at the top. For example, add a filter that requires the field to have a value, or sort descending by a date column so the most recent rows (which include the new field) come first.
2.  Hard-refresh the page (Ctrl+Shift+R on Windows, Cmd+Shift+R on Mac).
3.  Open your Claygent or Use AI column, type `/`, and expand the Webhook column — the field should now be listed.

Once the field is selectable in your prompt, you can remove the temporary filter or sort to restore your original view.

**Alternative:** If you frequently need to reference a webhook sub-field in prompts across multiple columns, extract it as a standalone column. Click a cell in the webhook column, open **Cell details**, hover over the field, and select **Add as column → Create column**. The extracted column is then always available in the `/` picker without needing to sort the view first.
