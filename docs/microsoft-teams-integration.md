---
title: Microsoft Teams integration
source_url: https://university.clay.com/docs/microsoft-teams-integration
description: Send messages to Microsoft Teams channels directly from Clay.
last_synced: 2026-04-26T01:40:22.139Z
upstream_hash: fe6780487730a348bdf3b817f73c4a23f739894e2b31959abf019d3bb44b8b31
---

# Microsoft Teams integration

Send messages to Microsoft Teams channels directly from Clay.

Microsoft Teams is a collaboration platform that enables seamless communication within teams and organizations.

With this integration, you can send messages to Microsoft Teams channels directly from Clay, enabling automated notifications and updates to your team.

## **Enriching data with Microsoft Teams**

1.  While in a Clay table, click `Add enrichment` and search for `Microsoft Teams`.
2.  Under `Integrations`, select one of the Microsoft Teams options.
3.  In the modal, you will be asked to `Select Microsoft Teams account`.
    -   If you haven't already connected your Microsoft Teams account, click `+ Add account` and go through authentication.

**Required permissions:**

When you connect your Microsoft Teams account to Clay, you'll be asked to authorize the following permissions:

-   **offline\_access** - Allows Clay to maintain access to your Teams account
-   **ChannelMessage.Send** - Enables sending messages to Teams channels
-   **Team.ReadBasic.All** - Allows Clay to read basic team information
-   **Channel.ReadBasic.All** - Allows Clay to read basic channel information

These permissions ensure Clay can send messages to your selected Teams channels while maintaining secure access to your Microsoft Teams workspace.

### **`Action` Send message to Teams channel**

Use this action to send messages to a Microsoft Teams channel directly from Clay for notifications, alerts, or team updates.

**Inputs**

-   **Team:** Select the team where you want to post (required)
    -   Dynamic dropdown populated with all teams you've joined
-   **Channel:** Select the channel to post in (required)
    -   Dynamic dropdown populated based on the team you selected
    -   You must select a team first before channels will load
-   **Message body:** The message content to send to the Teams channel (required)
    -   Supports HTML formatting:
        -   `<strong>bold</strong>` for bold text
        -   `<em>italic</em>` for italic text
        -   \`\` for line breaks
        -   `<ul><li>lists</li></ul>` for bullet lists
        -   `<p>paragraphs</p>` for paragraphs

**Output**

-   **Was Sent:** Boolean confirmation that the message was successfully sent
-   **Message ID:** The unique identifier assigned to the message in Microsoft Teams
-   **Web URL:** Direct link to view the message in Microsoft Teams
