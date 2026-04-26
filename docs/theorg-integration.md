---
title: The Org integration
source_url: https://university.clay.com/docs/theorg-integration
description: Get insights into organizational structures.
last_synced: 2026-04-26T01:40:48.658Z
upstream_hash: a8abaf29e953eac57b678ff2d119c24f22f9cde61243b737287c76b9d148f8f9
---

# The Org integration

Get insights into organizational structures.

The Org integration provides comprehensive insights into organizational structures by leveraging professional profiles or work emails to reveal managerial hierarchies.

With this integration, you can identify reporting relationships, discover management hierarchies, and gain valuable context for strategic networking and outreach.

## **Enriching data with The Org**

1.  While in a Clay table, click `Add enrichment` and search for `The Org`.
2.  Under `Integrations`, select one of the The Org options.
3.  In the modal, you will be asked to `Select The Org account`.
    -   If you have your own account, click `+ Add account` and go through authentication. Otherwise, use the Clay provided key.

### `Action` Get a Person's Manager

Use this action to identify a person's manager using their LinkedIn profile or work email, providing organizational context and insights into reporting structures.

**Inputs**

-   **Work email:** The work email address of the person whose manager you want to find
-   **Social URL:** The professional social URL of the person (e.g., `https://www.linkedin.com/in/username`)

**Output**

**Employee Information**

-   **ID:** Unique identifier for the employee's position
-   **Position ID:** Numeric identifier for the position
-   **Full Name:** Employee's full name
-   **Title:** Employee's job title
-   **LinkedIn URL:** Employee's LinkedIn profile URL (if available)
-   **Manager ID:** Reference ID to the employee's manager
-   **Node Type:** Type of organizational node (typically "position")

**Manager Information**

-   **ID:** Unique identifier for the manager's position
-   **Name:** Manager's full name
-   **Members:** List of manager positions containing:
    -   Position ID
    -   Full Name
    -   Title
    -   LinkedIn URL
    -   Node Type

### **Run settings**

-   **Auto-update**
-   **Only run if:** The enrichment will only run if conditions are met. ([Learn more about conditional formulas here!](https://www.clay.com/university/lesson/ai-formulas-conditional-runs-clay-101))
