---
title: PredictLeads integration
source_url: https://university.clay.com/docs/predictleads-integration-overview
description: Identify recent news, open jobs, and connections for targeted
  business insights.
last_synced: 2026-04-26T01:40:29.966Z
upstream_hash: 82cc3e57dc2bdc26aab52e49f43fe453f3eb918931a1dd29fe7acfae9868838a
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
-   **News Found Date (Optional):** Filter news from a specific date or range.

### `Action` Find Connections

Identify recent business connections associated with a company, such as vendors, customers, and investors.

**Inputs**

-   **Domain:** Company domain to retrieve connections.
-   **Connection Types (Optional):** Specify connection types to filter results.

### `Action` Find Open Jobs

Retrieve active job listings from a company, providing insights into hiring trends and areas of expansion.

**Inputs**

-   **Domain:** Company domain to find job openings.
-   **Departments** **(Optional):** Filter by department.
-   **Days Since Posted (Optional):** Specify the age of job postings.

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
