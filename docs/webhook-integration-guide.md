---
title: Webhooks in Clay
source_url: https://university.clay.com/docs/webhook-integration-guide
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

| Limit | Value |
|---|---|
| Throughput | 10 requests/second, burst up to 20 requests |
| Rate limit scope | Per workspace — all active webhook sources share this budget |
| Max payload size | 100 KB per request |
| Max submissions | 50,000 per webhook source |

**Throughput:** Clay accepts up to 10 incoming HTTP requests per second per workspace. A burst of up to 20 requests is allowed when capacity is available — after a burst, throughput returns to the sustained 10-per-second rate. Each POST counts as one request against this limit, regardless of how many fields or records the payload contains. Exceeding the limit returns a `429` error and records are dropped — Clay does not queue them. To avoid data loss when sending in bulk, pace your requests to 10 per second or fewer. Multiple active webhook sources in the same workspace share this limit.

**Need a higher throughput limit?** If 10 requests/second is too restrictive for your workflow, contact Clay support to request an increase — rate limits can be adjusted for your workspace on request.

**Payload size:** Each HTTP POST to Clay's webhook endpoint must be 100 KB or smaller.

**Submission limit:** Each webhook source accepts up to 50,000 submissions. This is a cumulative lifetime count — every accepted submission increments the counter, and deleting rows from the table does **not** reduce it. Once you reach this limit, Clay returns a `403` error and you'll need to create a new webhook to continue receiving data.

**Enterprise Plan — run a webhook indefinitely:** Enable [auto-delete](https://www.clay.com/university/guide/auto-delete) (also called passthrough tables). When passthrough mode is active, the webhook source takes a separate code path that **bypasses the 50,000 submission limit entirely** — a single webhook URL can keep accepting data indefinitely without ever hitting the cap. This is the recommended approach for automated enrichment pipelines. Auto-delete is available on Enterprise plans and only works for webhook, send-table-data, and signal sources. Learn more in [table management settings](https://www.clay.com/university/guide/table-management-settings).

## Request body format

Each HTTP POST to Clay's webhook endpoint creates **exactly one new row** in your table.

**One record per POST:** Clay does not split array payloads into multiple rows. If you send a JSON array (`[{...}, {...}]`), the entire array becomes the data for a single row rather than creating one row per element. For one row per record, send one POST per record.

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

## FAQs

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

3. **Missing or wrong authentication token** — If you added an auth token when creating the webhook, it must be included in every request as a header. The token is only displayed once at creation — if you didn't copy it, you'll need to delete and recreate the webhook to generate a new one.

4. **Submission limit reached** — See the [Limits](#limits) section. Once a webhook source hits 50,000 submissions, Clay returns a `403` error and stops creating rows. This limit is cumulative — it counts all submissions since the webhook was created, and deleting rows does not reset it. **Enterprise plan:** Enable [auto-delete](https://www.clay.com/university/guide/auto-delete) to bypass this limit entirely — when passthrough mode is active, the 50,000 cap is skipped and the webhook can accept data indefinitely.

**Quick isolation test:** To confirm whether the issue is in your request or on Clay's side, try the simplest possible payload:

```
curl -X POST YOUR_CLAY_WEBHOOK_URL \
  -H "Content-Type: application/json" \
  -d '{"test": "hello"}'
```

If a row appears in your table, the issue is in your original request's formatting, headers, or auth token. If no row appears on a brand-new webhook, contact support.

### How do I find which table a webhook URL belongs to?

There is no customer-facing search to look up a Clay table by its webhook URL. If you have a webhook URL from an external system and need to identify which Clay table it's connected to, contact Clay support with the URL — the team can look it up on your behalf.

**Tip:** To avoid this situation in the future, give each webhook table a descriptive name when you create it (for example, "HubSpot MQL ingest" or "Salesforce lead flow"). Since every table generates a unique webhook URL, a clear name makes it easy to match a URL back to the right table later.
