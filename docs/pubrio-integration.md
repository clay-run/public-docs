---
title: Pubrio integration
source_url: https://university.clay.com/docs/pubrio-integration
last_synced: 2026-04-26T01:40:30.939Z
upstream_hash: 8b75a9233993fc26ceaa2e47492e352f92626dcdd3615466ce21b4e9085dfaa8
---

# Pubrio integration

Identify key contacts at companies, find phone numbers, analyze tech stacks, and discover job openings.

Pubrio enables efficient identification and contact extraction of key sales and recruiting leads by automating the search and enrichment of personnel information and company tech stacks.

With this integration, you can identify key contacts at companies, find phone numbers, analyze tech stacks, and discover job openings to streamline outreach and analysis processes.

## **Enriching data with Pubrio**

1.  While in a Clay table, click `Add enrichment` and search for `Pubrio`.
2.  Under `Integrations`, select one of the Pubrio options.

### `Action` Find people at company

Search for and identify key contacts at target companies based on role, department, and location filters to build targeted outreach lists.

**Inputs**

-   **Company domain:** The website domain of the company to search within (e.g., `clay.com`)
-   **Company professional profile URL:** (e.g., `https://www.linkedin.com/company/grow-with-clay/`)

_Note: Either company domain or company professional profile URL is required._

**Optional Filters**

-   **Job title:** A comma-separated list of job titles (e.g., "Software Engineer, Product Manager")
-   **Management level:** Filter by management level of the contacts
-   **Department title:** Filter by specific department names
-   **Department function:** Filter by department functions
-   **Company size:** Filter by company size ranges
-   **People locations:** Filter by contact locations
-   **Company locations:** Filter by company locations

**Output**

-   **List of matching contacts (up to 25) with details:**
-   Name and title
-   Company information
-   Department and function
-   Location
-   Professional profile URL (when available)
-   **Total number of people found**
-   **Total number of people returned** (limited to 25 per request)

### `Action` Find phone number (APAC)

The Find phone number action enriches LinkedIn profiles with phone numbers to support efficient and direct outreach.

**Inputs**

-   **Professional profile URL (Required):** The LinkedIn profile URL to find the phone number for. Must be a valid LinkedIn URL in the format `https://www.linkedin.com/in/john-doe-1234567890/`.

**Output**

-   **LinkedIn URL:** The validated LinkedIn profile URL
-   **LinkedIn name:** The LinkedIn profile name in slug format
-   **Phones:** Array of phone number details including:
-   **Value:** The phone number in E.164 format (e.g., `+16468089010`)
-   **Type:** The type of phone number
-   **Status:** Verification status of the phone number (e.g., `Verified`)

### `Action` Enrich company tech stack

Identifies and retrieves technologies used on a company's website by analyzing their domain or professional profile.

**Inputs**

-   **Company domain:** The domain of the company to find the tech stack for. (Required if profile URL not provided)
-   **Company professional profile URL:** The company professional profile URL to find the tech stack for. (Required if domain not provided)

**Output**

-   **Category ID:** Numeric identifier for the technology category
-   **Technologies:** Array of technologies found, including:
-   **Icon:** Technology's icon file name
-   **Name:** Technology name
-   **Tag ID:** Numeric identifier for the technology
-   **Version:** Version number of the technology (if available)
-   **Website:** URL of the technology provider
-   **Location:** Where the technology was detected

### `Action` Find open jobs at company

Find job listings posted by companies using their website domain or professional profile URL, returning up to 25 matching positions.

**Inputs**

-   **Company domain (Optional):** The domain of the company to find jobs for (e.g., `microsoft.com`). One of domain or company professional profile URL is required.
-   **Company professional profile URL (Optional):** The company's professional profile URL. One of domain or company professional profile URL is required.
-   **Job title (Optional):** A comma-separated list of job titles to search for (e.g., "Software Engineer, Product Manager")
-   **Post keywords (Optional):** Words to filter the results by (e.g., "Python, React")
-   **Job locations (Optional):** The locations where the jobs are based
-   **Company headquarters locations (Optional):** Filter by company headquarters location
-   **Date job posted after (Optional):** Filter jobs posted on or after a specific date (e.g., "5 days ago"or "2022-07-31")
-   **Date job posted before (Optional):** Filter jobs posted on or before a specific date (e.g., "5 days ago"or "2022-07-31")

**Output**

-   List of jobs matching the search criteria
-   Total number of jobs found
-   Total number of jobs returned (maximum 25)
-   Job title
-   Company information
-   Location
-   Posting date
-   Job description
-   Other relevant metadata

### **Run settings**

-   **Auto-update**
-   **Only run if:** The enrichment will only run if conditions are met. ([Learn more about conditional formulas here!](https://www.clay.com/university/lesson/ai-formulas-conditional-runs-clay-101))
