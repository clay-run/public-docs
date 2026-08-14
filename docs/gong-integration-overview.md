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

**Requirements:** The Prospect Owner must have a Gong Engage seat — a standard Gong license is not sufficient to enroll prospects in flows.

**Inputs**

-   **Prospect Owner email:** Email of the Gong Engage user who owns the flow instance. Once this is selected, you'll be able to assign the prospect.
-   **Flow ID:** ID of the Gong Engage flow you want to add the prospect to.
-   **CRM Prospect ID:** This is the CRM ID of the prospect you want to add to the flow (Hubspot, Salesforce, etc.). For this to work properly, you must have the CRM connected to your Gong account.
-   **Flow instance description (optional):** A description for this prospect's flow instance, visible to reps. Useful for automatically triggered flows so reps understand the context of who they're engaging and why.
-   **Override flow instance variables (optional):** Set values for custom field placeholder variables defined in the flow. Provide key-value pairs where the key is the variable name from your Gong flow and the value is the Clay data to insert. The values you set apply to the entire flow for this prospect.
-   **Override for step N subject line (optional):** Replace the subject line sent to this prospect in step N (steps 1 through 20). Map a Clay column containing the complete subject — the override replaces the entire subject for that step, so generate the full subject line in Clay before mapping it here.
-   **Override for step N body (optional):** Replace the message body sent to this prospect in step N (steps 1 through 20). Map a Clay column containing the complete body — the override replaces the entire body for that step, so generate the full copy in Clay before mapping it here.

**Important:** The Gong account connected in Clay must belong to the same user whose email is set as Prospect Owner. If a different user's Gong account is connected, there will be a mismatch between the authenticating user and the flow owner, which may prevent the prospect from being enrolled in Gong Engage.

**Troubleshooting: Clay shows "Added to flow" but the prospect doesn't appear in Gong Engage**

If Clay reports a successful enrollment but the prospect isn't visible in the flow, the issue is typically on the Gong or CRM configuration side. Check the following:

1.  **Gong account matches Prospect Owner:** Confirm that the Gong account connected in Clay belongs to the same user set as the Prospect Owner email. Using a different account creates a mismatch between who is authenticating the API call and who owns the flow.
2.  **Salesforce ↔ Gong connection:** In Gong Admin settings, verify that Salesforce is connected and contacts are actively syncing.
3.  **CRM Prospect ID:** Double-check that the Salesforce or HubSpot Contact ID you're passing actually exists in your CRM.
4.  **Gong Engage seat:** The Prospect Owner must have a Gong Engage seat—a standard Gong license is not sufficient.
5.  **Flow is active:** Confirm the flow is published and active in Gong Engage.
6.  **Already enrolled:** If the contact was previously added to the same flow, Gong may skip re-enrolling them.

**Common "Add Prospect to Flow" error messages**

When the action fails, Clay displays an error in the cell. The error text comes directly from Gong's API. Common messages include:

-   **"Prospect opted out"** — the prospect has opted out of Gong Engage outreach and cannot be enrolled in flows. The prospect must opt back in through Gong before re-enrollment is possible.
-   **"Prospect is already assigned to the same flow"** — the prospect is already enrolled in this specific flow. To re-enroll them (for example, after reassigning to a new owner), first remove them using the **Remove Prospect from Flow** action, then run **Add Prospect to Flow** again.

**Capturing error text in a formula column**

To route rows based on whether an enrollment failed and why — for example, to skip opted-out prospects in a downstream step — you can pull the error text from the **Add Prospect to Flow** column into a formula column using `Clay.getCellErrorMessagePreview()`:

```javascript
Clay.getCellErrorMessagePreview({{Add prospect to flow}})
```

See [Formulas — How do I pull an error message from an action column into another column?](formula-generator.md) for full usage details, including limitations on preview behavior and which cells are supported.

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

## `Guide` Populating Gong Engage step content with Clay data

You can inject Clay-enriched data — such as personalized snippets, company details, job titles, or AI-generated copy — into Gong Engage flow steps using the override inputs on the **Add Prospect to Flow** action. This lets you customize each prospect's outreach without creating custom Salesforce fields or configuring Gong's field placeholder setup separately.

**Two override approaches:**

-   **Override subject and body per step:** Use **Override for step N subject line** and **Override for step N body** to replace the full content of a flow step for a specific prospect. Because the override replaces the entire subject or body for that step (not just a placeholder within the existing template), generate the complete copy in Clay first — using an AI column or formula column — and then map that column to the corresponding override input.

-   **Override flow instance variables:** If your Gong flow uses custom field placeholder variables, use **Override flow instance variables** to set their values per prospect. Provide key-value pairs where the key is the placeholder variable name as defined in your Gong flow and the value is the Clay column data to insert. This approach inserts values into the placeholders while keeping the rest of the template intact.

**Setup steps:**

1.  In your Clay table, add an AI column or formula column to generate the personalized content you want in each flow step. You can also reference an existing enriched data column directly.
2.  Add the **Add Prospect to Flow** enrichment action and configure **Prospect Owner email**, **Flow ID**, and **CRM Prospect ID** as usual.
3.  To override a step's content: in the action settings, scroll to **Step N overrides** and map your Clay column to **Override for step N subject line** and/or **Override for step N body**.
4.  To set custom field placeholder values: scroll to **Override flow instance variables** and add key-value pairs — key = the variable name in your Gong flow, value = the Clay column with the data to insert.
5.  Run the action. Each prospect receives the override values from their own row in Clay.
