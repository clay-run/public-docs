---
title: Fivetran integration overview
description: Platform to centralize data from various sources into cloud warehouses
last_synced: 2026-04-26T01:40:00.431Z
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
