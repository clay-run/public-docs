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

Use this action to retrieve the full org chart for a company given its domain. The action returns all position nodes in the hierarchy, including names, titles, manager links, work emails, and professional profile URLs. It costs **25 credits per org chart** regardless of how many positions are returned. Clay refunds the credit if no org chart data is found for the domain.

**Input**

-   **Company domain:** The website domain of the company whose org chart you want to find (e.g., `clay.com`).

**Output**

-   **Total positions found:** Number of position nodes returned
-   **Positions:** Array of position records, each containing:
    -   **Full Name:** Person's full name
    -   **Title:** Job title
    -   **Work Email:** Work email address (if available)
    -   **Professional profile URL:** Professional network profile URL (if available)
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

#### Surfacing the hierarchy and building an org chart

After running **Find company org chart**, the table may initially show only Name, Title, Work Email, and Professional profile URL as columns. Manager ID and Position ID are returned by the source but need to be added explicitly — click `+` to add a column and select those fields from the source output.

**How the hierarchy is encoded:** Each row represents one position. Position ID is that person's unique identifier. Manager ID contains the Position ID of their manager (another row in the same table). The person at the top of the org — typically the CEO — has no Manager ID. This parent-child link is the complete reporting structure returned by the source.

**Connecting each person to their manager by name:** Add a Lookup column that finds the row whose Position ID matches the current row's Manager ID and returns that row's Full Name. This gives you a readable "reports to" label you can group and filter by.

**Clay has no built-in org chart view.** Tables display as a grid — there is no tree or hierarchical view inside Clay. To visualize the reporting structure, export the table with Full Name, Title, Position ID, and Manager ID, then use an external tool such as Claude or ChatGPT to generate a visual chart. The Position ID and Manager ID columns are all a charting tool needs to build the tree; names and titles become the labels.

**Teams and departments are not available from this source.** The Org does not return team or department fields directly. To group people by function:
-   Add a **Use AI** column that classifies each person's Title into functional labels (for example: Engineering, Sales, Marketing).
-   Use **ZoomInfo** enrichment to add seniority, departments, and sub-departments as structured fields.

**Coverage:** Manager links are not complete for every person at every company. Some rows will return without a Manager ID even where name and title are present. Coverage varies by company size and how well-indexed the company is in The Org's data.

### **Run settings**

-   **Auto-update**
-   **Only run if:** The enrichment will only run if conditions are met. ([Learn more about conditional formulas here!](https://www.clay.com/university/lesson/ai-formulas-conditional-runs-clay-101))
