---
title: Sumble integration
source_url: https://university.clay.com/docs/sumble-integration
last_synced: 2026-04-26T01:40:44.109Z
upstream_hash: 1b604eb87b271baec4a17255fcdeb98ca6a832682c61cdb607386ceb1fd8a036
---

# Sumble integration

Validate whether a company uses specific technologies.

Sumble enables efficient verification of company technology usage by analyzing signals across jobs, people, and teams.

With this integration, you can validate whether a company uses specific technologies, enrich your ICP segments, and strengthen sales and marketing workflows that rely on accurate tech stack insights.

## **Enriching data with Sumble**

1.  While in a Clay table, click `Add enrichment` and search for `Sumble`.
2.  Under `Integrations`, select `Enrich company technologies`.

### `Action` Enrich company technologies

Use this action to confirm whether target companies use specific technologies based on their domain and selected technology filters.

**Inputs**

-   **Company domain (Required)**
-   **Select technologies (Required):** Search and select the technologies you want to check for at the target company.
    -   Begin typing in the search box to see available technologies.
    -   Select one or multiple technologies you want verified.
    -   You will be charged 6 Clay credits for each technology returned.
-   **Last detected date filter (Optional):** Filter by the date a technology was last seen. You can use relative dates like "5 days ago" or a specific date like "2025-01-01" (yyyy-MM-dd format).

**Output**

-   **Technologies Found:** Comma-separated list of technologies detected for the company (e.g., "Python, JavaScript")
-   **Technologies Count:** Total number of technologies detected
-   **Technologies:** Detailed array with information for each technology found:
    -   **Name:** Technology name
    -   **Last Job Post:** Date when the technology was last mentioned in a job posting
    -   **Jobs Count:** Number of job postings mentioning this technology
    -   **Jobs Data URL:** Link to view job postings for this technology
    -   **People Count:** Number of people associated with this technology
    -   **People Data URL:** Link to view people data for this technology
    -   **Teams Count:** Number of teams using this technology
    -   **Teams Data URL:** Link to view teams data for this technology
-   **Organization:** Metadata about the organization (ID, slug, name, domain)
-   **Source Data URL:** A direct link to the company's technology profile on Sumble for further exploration
-   **ID:** Unique identifier for the enrichment request

### **Run settings**

-   **Auto-update**
-   **Only run if:** The enrichment will only run if conditions are met. ([Learn more about conditional formulas here!](https://www.clay.com/university/lesson/ai-formulas-conditional-runs-clay-101))

**Note:** This action charges 6 Clay credits per technology returned. If no technologies are found, credits will be refunded.
