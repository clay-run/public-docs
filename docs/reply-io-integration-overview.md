---
title: Reply.io integration
description: AI-powered sales automation boosting lead generation and meeting bookings.
last_synced: 2026-04-26T01:40:32.677Z
---

# Reply.io integration

AI-powered sales automation boosting lead generation and meeting bookings.

## Integration Overview

With [Reply.io](http://Reply.io) within Clay, you can export your data to run personalized email campaigns, send cold emails, and automate follow ups. In this guide we'll go over:

-   Setting up Reply.io and Clay
-   Actions you for Reply.io you can run within Clay

## Requirements for Setting up Reply.io and Clay

You will need two prepare two steps in advance to set up Reply.io and Clay integration

**Requirement #1: Add your Reply.io API key to Clay**

You will first need to obtain the Reply.io API key, which you can copy from your Reply.io from **Settings > API Key.**

Then upload your key within **Settings > Connections** or via any Reply.io integration panel.

**Requirement #2: Have an existing campaign you are adding leads to**

**‍**To use To use this feature, make sure you have an active campaign set up in Reply.io. Clay can add contacts to existing campaigns but cannot create campaigns directly.

## Available actions for Reply.io within Clay

### `Action` Push Contact to Campaign

Use this action to add an existing contact to a campaign (sequence) in Reply.io. Contacts will only be added if they are not currently active in another campaign.

**Setup Inputs**

-   **Campaign ID**: Choose the campaign (sequence) to add the contact to. If no options appear, try refreshing the fields to load available campaigns.
-   **Email Address**: Enter or select the column with the contact's email address for inclusion in the campaign.

To include additional contact data in Reply.io — such as job title, phone number, or custom fields — add a **Create Contact** column before this step to create or update the contact with those fields first. See the Create Contact action below.

### `Action` Create Contact

Use this action to create a new contact in Reply.io. If the contact already exists, the information will be updated with the latest values provided.

**Setup Inputs**:

-   **Email address**: Enter or select the contact's email address. This is required.
-   **First name**: Provide the contact's first name. This is required.
-   **Last name** (Optional): The last name of the contact.
-   **Company** (Optional): The name of the contact's company or organization.
-   **City** (Optional): The city where the contact is located.
-   **State** (Optional): The state where the contact is located.
-   **Country** (Optional): The country where the contact is located.
-   **Time zone ID** (Optional): A Microsoft timezone ID for the contact (for example, "Eastern Standard Time").
-   **Title** (Optional): The contact's job title or position.
-   **Phone number** (Optional): The contact's phone number.
-   **Personal profile URL** (Optional): A link to the contact's professional networking profile.
-   **Custom fields** (Optional): Any additional custom fields to set for the contact. Only fields that have been defined in your Reply.io account will be updated.

**Tip:** To push contacts to a Reply.io campaign with data beyond just email — such as job title or custom fields — use a two-step workflow: add a **Create Contact** column first to set those fields in Reply.io, then add a **Push Contact to Campaign** column to enroll the contact in the sequence.
