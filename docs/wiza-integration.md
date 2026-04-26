---
title: Wiza integration
source_url: https://university.clay.com/docs/wiza-integration
description: Streamline contact enrichment workflows
last_synced: 2026-04-26T01:40:55.218Z
upstream_hash: 38659dc6de86afe2eea2676129df012b616bbc857ac2e37721c4c094c98f9538
---

# Wiza integration

Streamline contact enrichment workflows

Wiza enhances contact data management by automating the discovery and validation of emails, professional profiles, and phone numbers.

With this integration, you can streamline contact enrichment workflows, reducing manual effort while enhancing the accuracy and completeness of lead information.

## **Enriching data with Wiza**

1.  While in a Clay table, click `Add enrichment` and search for `Wiza`.
2.  Under `Integrations`, select one of the Wiza options.
3.  Under `Integrations`, select one of the Wiza options.
    -   If you have your own account, click `+ Add account` and go through authentication. Otherwise, use the Clay provided key.

### `Action` Find email

Use this action to locate and verify a person's work email address using their name and company information.

**Inputs**

-   **Full Name:** The full name of the person (required with company information)
-   **Company Name:** The person's company name
-   **Company Domain:** The company's domain name
-   **Professional Profile URL:** LinkedIn profile URL (can be used instead of name/company)
-   **Email Options:** Choose from:
    -   Work Email (default)
    -   Personal Email
    -   Both

**Output**

-   Returns email addresses based on the selected options.

### `Action` Find professional profile

Use this action to discover and enrich professional profile information using contact details.

**Inputs**

-   **Email:** The email address of the person whose professional profile you want to find
-   **Full name:** The person's full name (must be used with company name)
-   **Company name:** The company where the person works
-   **Company domain (Optional):** The company's website domain for better matching accuracy

**Output**

-   **Name:** The person's full name
-   **Title:** Current job title
-   **Company:** Current company name
-   **Location:** Geographic location
-   **Company domain:** Company website domain
-   **LinkedIn profile URL:** Direct link to the person's professional profile

### `Action` Find phone number

Use this action to locate and enrich contact records with phone numbers using LinkedIn profile URLs.

**Inputs**

-   **Full Name:** The full name of the person (required with company details)
-   **Company Name:** The company name of the person
-   **Company Domain:** The company domain of the person
-   **Professional Profile URL:** The LinkedIn profile URL (e.g., `https://www.linkedin.com/in/colinparsonscom`)

**Output**

-   **Name:** The contact's full name
-   **Mobile Phone:** The contact's mobile phone number
-   **Phone Number:** Any additional phone numbers found
-   **Title:** The contact's job title
-   **Phones:** Array of all phone numbers found with additional details

### **Run settings**

-   **Auto-update**
-   **Only run if:** The enrichment will only run if conditions are met. ([Learn more about conditional formulas here!](https://www.clay.com/university/lesson/ai-formulas-conditional-runs-clay-101))
