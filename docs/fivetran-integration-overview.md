---
title: Fivetran integration overview
source_url: https://university.clay.com/docs/fivetran-integration-overview
last_synced: 2026-04-26T01:40:00.431Z
upstream_hash: a3e9b46aa7e40f6e28da1e9a6d584e8e048dc3b36556da570f1e3f9c2e4fdb5d
---

# Fivetran integration overview

Platform to centralize data from various sources into cloud warehouses

## Fivetran Overview

Use the Fivetran integration in Clay to seamlessly send data to a Fivetran webhook destination, enabling automated data transfer and synchronization.

## Setting up Fivetran and Clay integration

To set up the Fivetran integration, you will need:

-   **Webhook URL**: The destination URL provided by Fivetran to receive the data.
-   **Payload**: Key-value pairs defining the data you want to send to the webhook.

## **Available Actions with the Fivetran Integration**

### `Action` Send Data to Webhook

Use this action to send data to a Fivetran webhook destination directly from Clay.

**Setup Inputs**

-   **Webhook URL**: Enter or select a column containing the URL of the Fivetran webhook destination where you’d like to send the data.
-   **Payload**: Define the data to send by adding key-value pairs. Use this section to specify the content of your webhook message.
