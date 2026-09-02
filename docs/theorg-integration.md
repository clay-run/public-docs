---
title: The Org integration
description: Get insights into organizational structures.
last_synced: 2026-04-26T01:40:48.658Z
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

### `Source` Find company org chart

Use this action to retrieve the full org chart for a company given its domain. The action returns all position nodes in the hierarchy, including names, titles, manager links, work emails, and LinkedIn profile URLs. It costs **25 credits per org chart** regardless of how many positions are returned. Clay refunds the credit if no org chart data is found for the domain.

**Input**

-   **Company domain:** The website domain of the company whose org chart you want to find (e.g., `clay.com`).

**Output**

-   **Total positions found:** Number of position nodes returned
-   **Positions:** Array of position records, each containing:
    -   **Full Name:** Person's full name
    -   **Title:** Job title
    -   **Work Email:** Work email address (if available)
    -   **Professional profile URL:** LinkedIn URL (if available)
    -   **Manager ID:** Internal reference ID of the person's manager
    -   **Id / Position ID:** Internal identifiers for the position node

#### Enriching a list of companies with org charts

**Find company org chart** is a source-type enrichment — the Company domain field accepts a single fixed value only and cannot be mapped to a column of domains. To pull org charts for multiple companies row-by-row, use The Org's HTTP API directly via Clay's **HTTP API** enrichment column instead:

1.  Obtain your own API key from your The Org account settings.
2.  In your Clay table, click `Add enrichment` and select **HTTP API**.
3.  Configure the HTTP API column to call The Org's API endpoint with your API key in the request headers. Save the credentials as an HTTP API (Headers) account to reuse them across tables.
4.  Map your company domain column as a dynamic input to the URL or request body. Unlike the source-type enrichment, the HTTP API column accepts column references and sends a separate API call for each row.
5.  Parse the JSON response to extract the org chart fields you need.

For setup details on the HTTP API enrichment column, see [HTTP API](http-api-integration-overview.md).

### **Run settings**

-   **Auto-update**
-   **Only run if:** The enrichment will only run if conditions are met. ([Learn more about conditional formulas here!](https://www.clay.com/university/lesson/ai-formulas-conditional-runs-clay-101))
