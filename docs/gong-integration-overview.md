---
title: Gong integration
source_url: https://university.clay.com/docs/gong-integration-overview
last_synced: 2026-04-26T01:40:02.764Z
upstream_hash: 0dbaadeabb893991d2d256aac663cde514b7d2eb4bda927f5a751df447a51acc
---

# Gong integration

Obtain call data of your prospects.

[Gong.io](http://Gong.io) empowers revenue teams to enhance sales effectiveness through AI-powered conversation intelligence, analyzing customer interactions across calls, emails, and meetings to provide actionable insights, enable data-driven coaching, and improve deal execution at scale.

Clay's Gong integration lets users push contacts from Clay tables into Gong Engage flows and retrieve call data from Gong—streamlining workflows and improving campaign targeting.

**Heads up!** To use this integration, you will need:

-   A Launch Plan at Clay
-   A Gong Engage subscription

## Creating a table with Gong

1.  In a workbook, click `+ Add` at the bottom.
2.  Search for `Gong` and select from the results.

### `Source` Pull calls from Gong

Retrieve call data from Gong to analyze conversations and enhance workflow insights.

-   **Gong User ID (Optional):** If left empty, calls from all users will be pulled.
-   **Start date**
-   **End date**

## Enriching data with Gong

To connect your Gong account for Clay actions:

1.  In your Clay table, click `Add enrichment` and search for `Gong`.
2.  Under `Integrations`, select one of the Gong actions.
3.  Within the settings side panel, you will be asked to `Select Gong account`.
    -   To connect your Gong account, click `Add account` and go through authentication.

### `Action` Get call details

Use this action to retrieve the information about a Gong call.

**Inputs**

-   **Gong Call ID:** Enter the Gong Call ID of transcript you want to retrieve.
-   **Details to pull:** Select the details you want to pull from the call.

### `Action` Get call transcript

Use this action to retrieve the transcript of a Gong call.

**Note: Due to transcript size limitations, this action can only process one call ID at a time. To view multiple transcripts, access each complete transcript from the action column.**

**Inputs**

-   **Gong Call ID:** Enter the Gong Call ID of transcript you want to retrieve.
-   **Combine transcript text:** By default, the transcript is returned as a list of messages. To merge the result into a single text block, enable this option.

### `Action` Add Prospect to Flow

Use this action to add a prospect to a Gong Engage flow.

**Inputs**

-   **Prospect Owner email:** Email of the Gong Engage user who owns the flow instance. Once this is selected, you'll be able to assign the prospect.
-   **Flow ID:** ID of the Gong Engage flow you want to add the prospect to.
-   **CRM Prospect ID:** This is the CRM ID of the prospect you want to add to the flow (Hubspot, Salesforce, etc.). For this to work properly, you must have the CRM connected to your Gong account.

### `Action` Get Assigned Flows for Prospect

Use this action to retrieve the Gong Engage flows assigned to a prospect.

**Inputs**

-   **CRM Prospect ID:** This is the CRM ID of the prospect you want to add to the flow (Hubspot, Salesforce, etc.). For this to work properly, you must have the CRM connected to your Gong account.

## `Guide` Pushing Gong call into Clay via webhook

Connect Gong to Clay to automatically send new call data in real time. With this setup, you can enrich each call record, generate insights, and keep your systems, like Salesforce or Notion, continuously in sync.

_(For example, use this flow to auto-draft post-meeting follow-ups or update CRM opportunities with call analysis such as MEDDPIC criteria.)_

1.  **Create a webhook rule in Gong:** From the [Gong Admin Panel](https://help.gong.io/docs/create-a-webhook-rule?utm_source=chatgpt.com), create an Automation Rule that triggers **`When a new call is processed`** and sends data **`via Webhook`**.
    -   In Clay, click **`+ Add`** at the bottom of your workbook, search for **`Webhook`**, and select **`Monitor webhook`**. Copy your webhook URL.
    -   Paste it into the Gong rule as the destination.
2.  **Capture call data in Clay:** When the rule fires, Gong sends call information, including `callId`, participants, timestamps, and metadata, into your Clay table as new rows.
3.  **Enrich with full call details:** Add the **`Get call details`** enrichment action.
    -   Map the `callId` column from your webhook data to the **Gong Call ID** input field to retrieve full call details like duration, transcript links, and insights.

Once enriched, you can:

-   Sync call summaries to **Salesforce**, **Snowflake**, or **Google Sheets.**
-   Trigger **follow-up emails**, CRM updates, or analytics workflows in Clay.
