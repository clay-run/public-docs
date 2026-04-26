---
title: Openmart integration
source_url: https://university.clay.com/docs/openmart-integration
description: Automate data gathering, verification, and updates across multiple channels.
last_synced: 2026-04-26T01:40:26.706Z
upstream_hash: 50ff3a00cedc0c8396056f975fcd9955c9729f542ac83a26fafb48fafaa2a291
---

# Openmart integration

Automate data gathering, verification, and updates across multiple channels.

The Openmart Integration helps users improve SMB outreach and lead management by analyzing and enriching contact information, technology stacks, and decision-maker details.

This integration automates data gathering, verification, and updates across multiple channels, delivering accurate insights for targeted marketing campaigns.

## **Enriching data with Openmart**

1.  While in a Clay table, click `Add enrichment` and search for `Openmart`.
2.  Under `Integrations`, select one of the Openmart options.

### `Action` Find tech stack

Use this action to identify the technology stack and ordering systems used by small and medium businesses through analysis of their digital presence.

**Inputs**

-   **Company domain (Required):** The domain of the company to find a tech stack for. Only the top-level domain will be used (e.g., `example.com` for `subdomain.example.com`).
-   **Company name (Optional):** The name of the company to find a tech stack for.
-   **Location (Optional):** The city, state, or country of the company. Note: If you provide a postal code, the search will be performed for the entire city where that postal code is located.
-   **Types of technologies to find (Required):** The types of technologies to look for in the company's tech stack (e.g., website builder, payment gateway, hosting provider).
-   **Specific technologies to look for (Optional):** Specific technologies to look for in the company's tech stack.
-   **Instructions for finding the technology (Optional):** Optional instructions to help Openmart's AI find the technology, e.g., "Look at the contact us page."

**Output**

-   **Tech Stack:** A structured list of technologies grouped by type
-   **All Technologies:** A flat list of all detected technologies
-   **Unformatted Technologies:** A text summary of the findings
-   **Source:** The URL where the technology information was found

### `Action` Find businesses

Find local small and medium businesses. Openmart will first try to find businesses in the provided location with a matching domain.

**Inputs**

-   **Parent company identifier (Required):** At least one parent company identifier (domain, professional social media URL, Facebook URL, or Instagram URL) must be provided.
-   **Location (Optional)**
-   **Limit (Optional):** Maximum number of local businesses to return.

**Output**

-   **Email information (if requested):**
    -   Email address
    -   Verification status
-   **Phone numbers (if requested):**
    -   Phone number
    -   Line type
    -   Validation status
    -   Confidence grade
-   **Personal information:**
    -   Full name
    -   First name
    -   Last name
    -   LinkedIn URL

### `Action` Find people at company

Find people in a specific role at a small and medium business (SMB), or at the SMB's parent company.

**Inputs**

-   **Company domain (Required):** The domain of the company to find decision makers for (only the top-level domain will be used)
-   **Company name (Optional):** The name of the company to find decision makers for
-   **Location (Optional):** The city, state, or country of the company
-   **Job title (Optional):** The job title of the decision maker to find (defaults to "owner/decision maker")
-   **Include emails (Optional):** Whether to include email addresses for the decision makers found
-   **Include phone numbers (Optional):** Whether to include phone numbers for the decision makers found
-   **Max people to find (Optional):** Maximum number of decision makers to find per company

**Output**

For each decision maker found, the action returns:

-   **Full Name**
-   **First Name**
-   **Last Name**
-   **Job Title**
-   **LinkedIn URL**
-   **Email (if requested):**
    -   Email address
    -   Verification status
-   **Phone Numbers (if requested):**
    -   Phone number
    -   Line type
    -   Validity status
    -   Confidence grade

### `Action` Enrich and verify email

Use this action to find, verify, and update contact information for professionals at small and medium-sized businesses.

**Inputs**

-   **Company domain (Required):** The domain of the company where the person works (e.g., `example.com`). Only the top-level domain will be used.
-   **Full name (Required):** The person's complete name (must include both first and last name).
-   **Company name (Optional):** The name of the company where the person works.
-   **Location (Optional):** The city, state, or country where the person works. Note: Postal code inputs will search the entire associated city.
-   **Professional URL (Optional):** The person's LinkedIn profile URL (format: `https://www.linkedin.com/in/username`).

**Output**

-   Email address
-   Email verification status
-   Full name
-   First name
-   Last name
-   LinkedIn URL (if found)

### `Action` Enrich and verify phone

Use this action to identify and verify phone numbers for SMB contacts, with confidence grading to ensure reliable outreach.

**Inputs**

-   **Company domain (Required):** The domain of the company where the person works (e.g., `example.com` for `subdomain.example.com`). Only the top-level domain will be used.
-   **Full name (Required):** The full name of the person. Must contain both first and last name.
-   **Company name (Optional):** The name of the company where the person works
-   **Location (Optional):** The city, state, or country where the person works
-   **Professional URL (Optional):** The professional profile URL of the person (e.g., `https://www.linkedin.com/in/colinparsonscom`)

**Output**

-   **Phone:**
    -   Phone Number: The discovered phone number (e.g., `+18167038759`)
    -   Line Type: Type of phone line (e.g., `MOBILE`)
    -   Valid: Boolean indicating if the phone number is valid
    -   Confidence Grade: Confidence rating of the data (e.g., `A`)
-   **Full Name:** The person's complete name
-   **First Name:** The person's first name
-   **Last Name:** The person's last name
-   **LinkedIn URL:** The person's professional profile URL

### **Run settings**

-   **Auto-update**
-   **Only run if:** The enrichment will only run if conditions are met. ([Learn more about conditional formulas here!](https://www.clay.com/university/lesson/ai-formulas-conditional-runs-clay-101))
