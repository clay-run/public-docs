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
