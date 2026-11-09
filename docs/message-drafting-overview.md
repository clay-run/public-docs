---
title: Message drafting overview
description: Write personalized message sequences with AI, conditionals and more.
last_synced: 2026-04-26T01:40:21.472Z
---

# Message drafting overview

Write personalized message sequences with AI, conditionals and more.

## Message drafting overview

The **Message drafting** feature streamlines the process of creating personalized, dynamic messages for export to your chosen sequencer.

This is particularly useful for automating outbound campaigns, such as sales outreach, as well as creating personalized intake messages for signups.

## Steps to using the message drafting feature

**Step 1: Open message drafting feature**

Access the message drafting tool through the export menu: **Tools > Export > Export Messages to Sequencer**.

**Step 2: Select your sequencer**

Choose the sequencer you want to export your messages to from the list.

**Note:** Each sequencer has unique export requirements and settings. For details, refer to the notes on sequencer-specific settings below.

**Step 3: Write your message(s)**

Within the **Message Drafting Panel**, craft your messages.

Be mindful of your sequencer's export settings to ensure compatibility.

**Step 4: Configure field mappings**

Click **Continue** to review and verify the field mappings for custom fields with your sequencer.

**Tip:** Some sequencers require fields to be pre-configured, while others allow you to create fields directly from within the action.

**Step 5: Verify run settings and run the enrichment**

Check your auto-update and conditional run-settings, as well as any other setting within your action to verify exporting.

## Message drafting panel components

The **Message Drafting Panel** is composed of several key components that work together to help you create dynamic, personalized messages efficiently.

### **Subject line**

-   Enter your desired subject line in the **Subject** field.

### **Message body**

-   Write your message directly in the **Body** field.
-   Use **AI Snippets** to generate suggestions or enhance your content.
-   Add **Conditional Snippets** to include dynamic content based on specific conditions, such as field values or logical operators.

### **AI model and account settings**:

-   Select the desired AI model for drafting (e.g., gpt-4o-mini).
-   Ensure the correct account is connected to access the AI functionality.

### **Run action settings**

-   Toggle **Auto-update** to refresh message drafts automatically with updated data.
-   Configure the **Only Run If** condition to control when the action should execute (e.g., only if a specific field exists).
-   Toggle **Auto-run AI snippets** to control whether AI snippet columns in your draft run automatically when rows are added or their inputs change. This toggle appears only when your draft contains at least one AI snippet. When off, AI snippet cells do not auto-run and the footer shows a plain **Save** button instead of the save-and-run dropdown. Auto-run is on by default for new drafts.

## **AI Snippets**

Create dynamic, tailored content directly within your message drafter using AI snippets.

## **Conditional snippets**

Conditional Snippets allow you to add dynamic logic to your messages, displaying specific content based on defined conditions.

### **Key Features**

-   [**Conditional Logic**](https://www.clay.com/university/guide/conditional-statements): Define "if/else" conditions to display different content based on recipient-specific data, such as including a personalized greeting if a first name exists.
-   [**Logical Operators**](https://www.clay.com/university/guide/logical-operators): Combine multiple conditions using operators like AND (e.g., First Name exists AND Company Name does not include "Clay") or OR.
-   [**Comparison Operators**](https://www.clay.com/university/guide/comparison-operators): Compare data values (e.g., check if a field "equals," "does not equal," or "contains" specific information) to tailor your message logic.
-   **Custom Fields**: Insert dynamic fields from your data for tailored messaging.

### **How to Use Conditional Snippets**

1.  **Insert a Conditional Snippet**:
    -   In your message body, type `/` to open the conditional snippet panel.
2.  **Define Your Conditions**:
    -   Use the **Where** fields to set conditions based on your data.
    -   Add multiple conditions using **AND** or **OR** to refine your logic branches.
    -   Example: Check if a field (`First Name`) exists or if another field (`Company Name`) contains specific text.
3.  **Set the "If" Output**:
    -   Define the content that will appear if the conditions are met.
    -   Use placeholders to dynamically insert data (e.g., `Hey {{First Name}}`,).
4.  **Set the "Else" Output**:
    -   Provide fallback content for cases where the conditions aren't met (e.g., `Hey there`).
5.  **Save and Test**:
    -   Save your snippet and test it with sample data to verify that the correct content displays for both "if" and "else" scenarios.

## Lemlist

Lemlist's custom fields support HTML. Note that message draft editor newlines get replaced with spaces so for new lines within Lemlist use <br> or <p> tags.

For more information on Lemlist's actions, refer to the [Lemlist documentation](https://www.clay.com/university/guide/lemlist-integration-overview).

## Smartlead

Smartlead's custom fields support HTML and newlines. You are able to create new custom fields from your Clay action panel.

For more information on Smartlead's actions, refer to the [Smartlead documentation](https://www.clay.com/university/guide/smartlead-integration-overview).

## Instantly

Smartlead's custom fields support HTML and newlines.

For more information on Instantly's actions, refer to the [Instantly documentation](https://www.clay.com/university/guide/instantly-integration-overview).

## Outreach

When you export messages to Outreach using **Export Messages to Sequencer**, Clay generates a **Subject** column and a **Body** column containing your drafted message. These are mapped to Outreach **prospect custom fields** — this does not create a native saved email draft in Outreach's composer. The generated content is stored in the custom fields and referenced from an Outreach sequence template.

We recommend reserving specific Prospect custom fields (e.g. custom10 to custom15) for Clay usage to avoid conflicts with other custom field data. You will have to manually map your messages to these custom fields.

### For existing prospects

For prospects who already exist in Outreach, use the **Lookup Prospect** action to retrieve the prospect record, then use the **Update Prospect** action to write the generated subject and body into the reserved custom fields. Avoid using **Create Prospect** for existing records — it will create duplicate prospects in Outreach.

Recommended setup:

1. Reserve two Outreach prospect custom fields for Clay, for example `custom10` (email subject) and `custom11` (email body).
2. Map the generated **Subject** and **Body** columns to those custom fields in the message-drafting action panel.
3. Add a **Lookup Prospect** column to retrieve the existing prospect by email or prospect ID.
4. Add an **Update Prospect** column and map the generated subject and body to the reserved custom fields.
5. Reference those custom fields in your Outreach sequence template so the personalized content is used when the sequence sends.

If you need a **native saved email draft** in Outreach's Outbox rather than a sequence, Clay's native Outreach integration does not currently support this. You can use an [HTTP API](https://university.clay.com/docs/http-api-integration-overview) column to call Outreach's `POST /api/v2/mailings` endpoint with `state` set to `draft`.

### HTML formatting

Outreach sequence emails are rendered as HTML, so plain newlines in custom field values collapse into spaces when the email displays. Use `<br>` tags to produce visible line breaks.

To add `<br>` tags to AI-generated email bodies, choose one of the following approaches:

-   **Claygent or AI column prompt**: add formatting instructions to your prompt, for example: *"Use `<br>` at the end of each line and `<br><br>` between paragraphs. Do not use plain line breaks."* Apply this to the email body field only — a `<br>` tag inside a subject line appears as literal text, so keep the subject plain.
-   **Formula column**: add a Formula column after your AI column that replaces each `\n` with `<br>`, then map that formula column to the Outreach custom field in the Update Prospect enrichment instead of the raw AI output.

For more information on Outreach's actions, refer to the [Outreach documentation](https://www.clay.com/university/guide/outreach-integration-interview).

## Salesloft

Salesloft's custom fields do not support HTML or newlines.

Custom fields must be manually defined in Salesloft before they can be exported from Clay. You will have to manually map your messages to these custom fields.

For more information on Salesloft's actions, refer to the [Salesloft documentation](https://www.clay.com/university/guide/salesloft-integration-overview).

## Reply.io

Reply.io's custom fields support HTML. Use <br> or <p> tags for newlines.

Note that there is a default maximum of 50 custom variables in total.

For more information on Reply.io's actions, refer to the [Reply.io documentation](https://www.clay.com/university/guide/reply-io-integration-overview).

## HeyReach

HeyReach's custom fields only support alphanumeric characters.

For more information on Salesloft's actions, refer to the [Heyreach documentation](https://www.clay.com/university/guide/heyreach-integration-overview).

## La Growth Machine

La Growth Machine's custom attributes support HTML. Use <br> or <p> tags for newlines.

La Growth Machine supports a maximum of 10 custom attributes per lead. Each custom attribute can be up to 250 characters long.

For more information on La Growth Machine's actions, refer to the [La Growth Machine documentation](https://www.clay.com/university/guide/la-growth-machine-integration-overview).

## Customer.io

Customer.io's attributes support HTML. Use <br> or <p> tags for newlines.

Each attribute has a maximum length of 250 characters.

For more information on Customer.io's actions, refer to the [Customer.io documentation](http://www.clay.com/university/guide/customer-io-integration-overview).
