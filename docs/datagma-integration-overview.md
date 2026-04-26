---
title: Datagma integration
source_url: https://university.clay.com/docs/datagma-integration-overview
last_synced: 2026-04-26T01:39:52.316Z
upstream_hash: e04d6d55f5854afc88037bc0c123fe3b5bb3a4fec2b0468593af9a9e0d11853d
---

# Datagma integration

Enrich contacts with accurate data for seamless B2B outreach.

Datagma is a B2B data enrichment platform that provides verified contact information and company intelligence from multiple data sources. Within Clay, you can use Datagma to enrich person and company profiles, find work emails and mobile numbers, locate professional social profiles, and identify employees at a target company.

## Enriching data with Datagma

1.  While in a Clay table, click `Add enrichment` and search for `Datagma`.
2.  Select any of the `Datagma` actions detailed below.
3.  In the modal, you will be asked to `Select Datagma account`.
    -   If you have your own account, click `+ Add account` and enter your Datagma API key. You can find this in your Datagma account settings. Otherwise, use Clay's managed Datagma account.

### `Action` Enrich Person

Enriches a person's profile using a work email, professional social URL, or company website combined with their full name.

**Inputs**

-   **Person Search Criteria (Required):** A work email address, professional social URL, or company website. If a company website is provided, the Full Name field is also required.
-   **Full Name (Optional):** The full name of the person to enrich. Required when Person Search Criteria is a company website.
-   **Include Phone Number Data? (Optional):** Toggle on to have Datagma attempt to return the person's phone number. Note: enabling this option incurs an additional credit cost.
-   **Include All Person Data? (Optional):** Toggle on to return the person's full work history and education.
-   **Include Company Data? (Optional):** Toggle on to return firmographic data for the person's current company. Note: enabling this option incurs an additional credit cost.

**Output**

-   **Person:** The enriched person record, including:
    -   Basic info: Name, First Name, Last Name, Location, Country, Region, Job Title, Company, Professional Social URL, Extracted Role, Extracted Seniority, Extracted Gender, Person Confidence Score, Company Confidence, Explanation
    -   Phone data (when enabled): Phone number details
    -   Full person data (when enabled): Past work experience and education history
    -   Company data (when enabled): Firmographic details for the person's current company

### `Action` Enrich Company

Enriches a company record with firmographic and business intelligence data using a company name or website.

**Inputs**

-   **Company Search Criteria (Required):** The company name or website (e.g., `microsoft.com`).

**Output**

-   **Name:** The company's name
-   **URL:** The company's professional social profile URL
-   **About:** A description of the company
-   **Employees Amount:** The number of employees listed on the company's professional profile
-   **Headquarters:** The company's headquarters location
-   **Headquarter Address:** Full headquarters address details
-   **Number of Locations:** Total number of office locations
-   **Subsidiary:** A list of subsidiary addresses
-   **Website:** The company's website URL
-   **Industries:** Industry classification
-   **Company Size:** Employee count range (e.g., `10001+`)
-   **Type:** Company type (e.g., Public Company)
-   **Founded:** Year the company was founded
-   **Specialties:** Areas of focus or specialization
-   **Similar Companies:** A list of similar companies
-   **Funding Rounds Summary:** Summary of funding activity
-   **Revenue Range:** Estimated revenue range
-   **Legal Name:** The company's legal entity name
-   **Funding Stage:** Current funding stage
-   **Contact Email:** A publicly listed contact email for the company

### `Action` Find Work Email

Finds the work email address of an employee given their full name and company domain.

**Inputs**

-   **Employee Full Name (Required):** The full name of the person whose email you are looking for.
-   **Company Domain (Required):** The website domain of the company (e.g., `clay.com`).
-   **Company Professional Social URL (Optional):** The company's professional social profile URL. Providing this improves email-finding accuracy.
-   **Employee Location (Optional):** The employee's geographic location (e.g., `Japan`). Useful for finding region-specific email formats.

**Output**

-   **Email:** The found work email address
-   **Email Domain:** The domain portion of the email address
-   **Status:** Email verification status (e.g., `Valid`)
-   **Patterns:** The email format patterns identified (e.g., `Firstname.Lastname`)
-   **MX Found:** Whether a valid mail exchange record was found for the domain
-   **SMTP Check:** Whether the email passed an SMTP check
-   **Catch All:** Whether the domain accepts catch-all emails
-   **Flags:** Validation flags (e.g., `has_dns`)
-   **Correlation ID:** A unique identifier for the lookup request

### `Action` Find Mobile Number

Finds the mobile phone number of a person using a professional social URL or email address.

**Inputs**

-   **Professional Social URL (Required - at least one):** The person's professional social profile URL. If provided, the email field will be ignored.
-   **Work or Personal Email (Required - at least one):** The person's email address. Used when no professional social URL is available.

**Output**

-   **Number:** The found mobile number
-   **Display:** The formatted phone number (e.g., `516-426-8822`)
-   **Display International:** The internationally formatted phone number (e.g., `+1 516-426-8822`)
-   **Country Code:** The country dialing code
-   **Type:** The number type (e.g., `mobile`)
-   **Valid Since:** The date this number was first observed
-   **Last Seen:** The date this number was most recently observed

### `Action` Find Professional Profile

Finds a person's professional social profile URL using their full name and company domain or email.

**Inputs**

-   **Full Name (Required):** The person's full name (e.g., `John Doe`).
-   **Company Domain (Required - at least one):** The company's website domain (e.g., `clay.com`). Recommended — provides a higher match rate.
-   **Email (Required - at least one):** The person's email address. May have a lower match rate.

**Output**

-   **Full Name:** The matched person's full name
-   **Social URL:** The person's professional social profile URL

### `Action` Find Employees at Company

Returns a list of employees at a company filtered by job title, with optional location filtering.

**Inputs**

-   **Company Search Criteria (Required):** The company name or website.
-   **Job Titles (Required):** The job titles to search for. Accepts a comma-separated list (e.g., `Software Engineer, Marketer`). A maximum of 6 job titles can be searched per run.
-   **\# of Employees (Optional):** The maximum number of employees to return. Maximum of 10.
-   **Employee Country (Optional):** Filter results to employees located in a specific city or country (e.g., `Tokyo, Japan`).

**Output**

-   **Employees:** A list of matching employee records. Each record includes:
    -   Name, First Name, Last Name
    -   Location, Job Title, Company
    -   Professional Social URL
    -   Extracted Role, Extracted Seniority, Extracted Gender
    -   Person Confidence Score, Employee Job Score, Employee Company Score

## Run settings

-   **Auto-update**
-   **Only run if:** The enrichment will only run if conditions are met. ([Learn more about conditional formulas here!](https://www.clay.com/university/lesson/ai-formulas-conditional-runs-clay-101))
