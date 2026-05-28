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
| Throughput | 10 records/second, burst up to 20 records |
| Rate limit scope | Per workspace — all active webhook sources share this budget |
| Max payload size | 100 KB per request |
| Max submissions | 50,000 per webhook source |

**Throughput:** Clay accepts up to 10 incoming records per second per workspace, with a one-time burst capacity of up to 20 records. Exceeding the limit returns a `429` error and records are dropped — Clay does not queue them. To avoid data loss when sending in bulk, pace your requests to 10 per second or fewer. Multiple active webhook sources in the same workspace share this limit.

**Payload size:** Each HTTP POST to Clay's webhook endpoint must be 100 KB or smaller.

**Submission limit:** Each webhook source accepts up to 50,000 submissions. Rows submitted count toward this limit even if you delete them from the table. Once you reach this limit, Clay returns a `403` error and you'll need to create a new webhook to continue receiving data.

**Enterprise Plan:** Enable [auto-delete](https://www.clay.com/university/guide/auto-delete) (also called passthrough tables) to automatically process and delete rows, allowing unlimited webhook submissions. Learn more in [table management settings](https://www.clay.com/university/guide/table-management-settings).

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
