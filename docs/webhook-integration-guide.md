---
title: Webhooks in Clay
source_url: https://university.clay.com/docs/webhook-integration-guide
description: Real-time data updates enabling application integrations and
  automated workflows.
last_synced: 2026-04-26T01:40:54.241Z
upstream_hash: 4541a1fcc8e1603dc707ab5b91839353a0179daa726fe2ee1513df79a7e7a65b
---

# Webhooks in Clay

Real-time data updates enabling application integrations and automated workflows.

Webhooks enable Clay to automatically receive data from other applications through HTTP POST requests in JSON format whenever specific events occur.

Your table updates instantly with new data, eliminating manual entry. This feature is particularly valuable for real-time updates, such as when adding new leads or modifying records based on external triggers.

## **Creating a table with webhook**

1.  In a workbook, click `+ Add` at the bottom.
2.  Search for `Webhooks` and click `Monitor webhook`.
3.  Copy the URL/cURL.
    -   **URL:** Paste this URL into the application sending data to Clay. This URL is where your data will be sent.
    -   **cURL:** Paste the cURL command into your command line to send data directly to Clay.
4.  Optionally, add authentication token. To secure your webhook, you can include an authentication token in the header of your request.
    -   Make sure to copy the token immediately, as you can only access authentication tokens once.

**Note:** Webhook sources are limited to 50,000 submissions, and this limit persists even after deleting rows. Once you reach this limit, you’ll need to create a new webhook to continue receiving data.  

**Enterprise Plan:** Enable [auto-delete](https://www.clay.com/university/guide/auto-delete) (also called passthrough tables) to automatically process and delete rows, allowing unlimited webhook submissions. Learn more in [table management settings](https://www.clay.com/university/guide/table-management-settings).
