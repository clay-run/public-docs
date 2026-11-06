---
title: Connect Clay to Marketo via a webhook
description: Connect Marketo to your Clay table.
last_synced: 2026-04-26T01:40:20.143Z
---

# Connect Clay to Marketo via a webhook

Connect Marketo to your Clay table.

This guide outlines how to connect your Marketo instance to Clay.

## Steps

### Set up Clay table

Step 1: Copying the Webhook URL from Clay

In your Clay workbook, click **+ Add**, search for **Webhooks**, and add a webhook source to create a table that receives data (see [Creating a table with webhook](https://www.clay.com/university/guide/webhook-integration-guide)). Once the webhook source is added, the table sidebar shows a **Webhook URL** section with **URL** and **cURL** tabs. Copy the value on the **URL** tab — this is the URL where you will send data via a POST request to integrate with Clay. To find the webhook URL again later, open the table, hover over the webhook source column header, and click the **Edit source** icon.

### Configure Marketo Webhook

**Step 2: Go to the Admin area in Marketo**

**Step 3: Click on Wehooks in the left hand menu**

**Step 4: Click New Webhook to create a new webhook**

**Step 5: Name and configure your Webhook.**

To properly configure Marketo’s webhook to send data to Clay, please fill in the following details exactly as shown:

-   URL: The webhook URL you copied from Step 1
-   Payload Template: first\_name={{lead.First Name:default=editme}} &last\_name={{lead.Last Name:default=editme}} &company={{company.Company Name}} &title={{lead.Job Title}} &email={{lead.Email Address:default=editme}} &id={{[lead.Id](http://lead.id/)}}
-   Request Token Encoding: None
-   Request Type: Post
-   Response Format: JSON

**Step 6: Click Create webhook**

Congratulations, you are all set up!
