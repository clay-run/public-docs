---
title: Salesforge integration
source_url: https://university.clay.com/docs/salesforge-integration
last_synced: 2026-04-26T01:40:35.967Z
upstream_hash: 0fde59b120d8517cbb1db9d7722725d83d7367c7eec782157d4b6230bb1d66fe
---

# Salesforge integration

Automate enrollment into outreach sequences and synchronizing contact information within workspaces

Salesforge enables streamlined contact management by automating enrollment into outreach sequences and synchronizing contact information within workspaces.

This integration enhances lead engagement, segmentation, and tracking through the use of detailed contact fields and custom variables.

## **Enriching data with Salesforge**

1.  While in a Clay table, click `Add enrichment` and search for `Salesforge`.
2.  Under `Integrations`, select one of the Salesforge options.
    -   Click `+ Add account` to connect your Salesforge account if you haven't already.

### **`Action` Add lead to existing sequence**

Enables automated enrollment of contacts into targeted outreach sequences within a Salesforge workspace for streamlined lead engagement and follow-up.

**Inputs**

-   **Contact details:** Key contact information for personalized engagement
-   **Custom variables:** Additional data fields like address and tags for enhanced segmentation

### **`Action` Upsert Contact into Workspace**

Synchronizes and updates contact information between a Clay table and a workspace, creating new contacts or updating existing ones while maintaining data consistency.

**Inputs**

-   **Contact Information:** Core contact details from your table (name, email, etc.)
-   **Custom Variables:** Additional fields to be mapped to workspace contact properties
-   **Tags:** Labels to organize contacts in the workspace

**Output**

-   **Contact ID:** Unique identifier for the created/updated contact in the workspace
-   **Status:** Confirmation of successful upsert operation
-   **Operation Type:** Indicates whether the contact was created or updated
