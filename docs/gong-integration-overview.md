---
title: Gong integration
description: Obtain call data of your prospects.
last_synced: 2026-04-26T01:40:02.764Z
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
    -   **Note:** Your Gong user must have API access enabled to connect. If you see an "Insufficient permissions" error on Gong's authorization screen, ask your Gong admin to enable API access for your account in Gong's Admin settings.

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

**Important:** The Gong account connected in Clay must belong to the same user whose email is set as Prospect Owner. If a different user's Gong account is connected, there will be a mismatch between the authenticating user and the flow owner, which may prevent the prospect from being enrolled in Gong Engage.

**Troubleshooting: Clay shows "Added to flow" but the prospect doesn't appear in Gong Engage**

If Clay reports a successful enrollment but the prospect isn't visible in the flow, the issue is typically on the Gong or CRM configuration side. Check the following:

1.  **Gong account matches Prospect Owner:** Confirm that the Gong account connected in Clay belongs to the same user set as the Prospect Owner email. Using a different account creates a mismatch between who is authenticating the API call and who owns the flow.
2.  **Salesforce ↔ Gong connection:** In Gong Admin settings, verify that Salesforce is connected and contacts are actively syncing.
3.  **CRM Prospect ID:** Double-check that the Salesforce or HubSpot Contact ID you're passing actually exists in your CRM.
4.  **Gong Engage seat:** The Prospect Owner must have a Gong Engage seat—a standard Gong license is not sufficient.
5.  **Flow is active:** Confirm the flow is published and active in Gong Engage.
6.  **Already enrolled:** If the contact was previously added to the same flow, Gong may skip re-enrolling them.

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

## `Guide` Reassigning a prospect to a new flow owner

To move a prospect from one Gong Engage flow owner to another—for example, when reassigning an overdue SLA contact to a new rep:

1.  **Remove the prospect from their current flow:** Add a **Remove Prospect from Flow** enrichment action. Provide the current owner's email, the Flow ID, and the CRM Prospect ID (the contact's Salesforce or HubSpot ID).
2.  **Look up the new owner's email:** If your table doesn't already have the new owner's email, add a **Salesforce Lookup Record** enrichment column set to look up the **User** object using the contact's `OwnerId` field and pull back the `Email` field.
3.  **Re-enroll the prospect under the new owner:** Add an **Add Prospect to Flow** enrichment action. Map the new owner's email to **Prospect Owner email**, provide the Flow ID, and map the CRM Prospect ID.