---
title: PredictLeads integration
description: Identify recent news, open jobs, and connections for targeted
  business insights.
last_synced: 2026-04-26T01:40:29.966Z
---

# PredictLeads integration

Identify recent news, open jobs, and connections for targeted business insights.

The PredictLeads integration in Clay allows users to access comprehensive business data, including recent company news, connections, job openings, and tech stack insights.

## **Enriching data with PredictLeads**

1.  While in a Clay table, click `Add enrichment` and search for `PredictLeads`.
2.  Under `Integrations`, select one of the PredictLeads options.
3.  In the modal, you will be asked to `Select PredictLeads account`.
    -   If you have your own account, click `+ Add account` and go through authentication. Otherwise, use the Clay provided key.

### `Action` Find Most Recent News

Retrieve the latest news articles related to a specific company.

**Inputs**

-   **Domain**: Company domain to search for news.
-   **News Categories (Optional):** Filter news by category.
-   **News Found Date (Optional):** Filter by when PredictLeads first discovered the news — not the article's original publication date. Accepts an ISO date (e.g. `2024-01-15`) or a relative value (e.g. `30 days ago`).
    -   _Note: When PredictLeads is used alongside other providers in the same enrichment column, the date filter shown in the column's quick-setup overview may only apply to other providers (such as Intellizence). Open the PredictLeads action settings directly to ensure the date filter takes effect._

### `Action` Find Connections

Identify recent business connections associated with a company, such as vendors, customers, and investors.

**Inputs**

-   **Domain:** Company domain to retrieve connections.
-   **Connection Types (Optional):** Specify connection types to filter results.

### `Action` Find Open Jobs

Retrieve active job listings from a company, providing insights into hiring trends and areas of expansion.

**Inputs**

-   **Domain:** Company domain to find job openings.
-   **Departments (Optional):** Filter by department (e.g. Sales, Engineering, Support).
-   **Filter for Job Title (Optional):** Filter for specific words or phrases in job titles, separated by commas (e.g. "engineer, marketing, accountant"). Does not accept AND/OR logic. Works best when combined with a **Departments** filter.
-   **Filter for Job Description (Optional):** Filter for specific words or phrases in job descriptions, separated by commas (e.g. "Salesforce, HubSpot"). Does not accept AND/OR logic. Works best when combined with a **Departments** filter.
-   **Days Since Posted (Optional):** Filter for jobs posted within the last X days.
-   **Only jobs tied to a location? (Optional):** When enabled, returns only jobs tied to a specific geographical area.
-   **Include Subdomains? (Optional):** When enabled, includes results from subdomains of the company domain.

**Output limit:** This action returns up to 10 matching jobs per run. When more matches exist, the **More Matches Than We Can Display** output field is set to `true` and **Total Count of Active Jobs** shows the full count from the provider. The table cell preview shows "10+ matching jobs" in this case. To work with all matching jobs, hover over the **Jobs** field in the cell details panel and click **Take action on list → Write each item to new row in other table**.

> **Credit note:** PredictLeads charges Clay for every lookup regardless of whether any jobs are returned. If a company has no open roles matching your filters, the enrichment will return "no jobs found" but credits are still consumed. To avoid charges on rows where no match is expected, use the `Only run if` condition to gate the enrichment.

### `Action` Find Technology Stack

Looks at a company's historical job descriptions and aggregates all of the technologies that have been mentioned in those job openings.

**Inputs**

-   **Domain**: Company domain for tech stack information.
-   **Technology Names (Optional):** Filter by specific technologies.
-   **Last Detected Date After (Optional):** Filter by last detection date.

### `Action` Find Financing Events

Find the financing events for a company using the company domain.

**Inputs**

-   **Domain**
-   **Financing Events First Seen Date (Optional)**

### **Run settings**

-   **Auto-update**
-   **Only run if:** The enrichment will only run if conditions are met. ([Learn more about conditional formulas here!](https://www.clay.com/university/lesson/ai-formulas-conditional-runs-clay-101))

## Troubleshooting

### Authentication errors

If a PredictLeads enrichment fails with an authentication error, your API credentials may be incorrect or expired. PredictLeads connections use your PredictLeads email address and API key.

To update your credentials in Clay:

1.  Go to `Settings` → `Connections`.
2.  Find your PredictLeads connection and click `…` → `Edit`.
3.  Re-enter your PredictLeads email address and API key, then save.

To confirm your credentials are valid, log in to your PredictLeads account and check that your API key is active. If the issue persists, contact PredictLeads support.
