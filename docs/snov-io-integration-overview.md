---
title: Snov.io integration
source_url: https://university.clay.com/docs/snov-io-integration-overview
last_synced: 2026-04-26T01:40:42.470Z
upstream_hash: 818d25fb4f7810895eba738bf10e6535b43591b0f367d87eceefadd8c23b2b25
---

# Snov.io integration

Sales automation platform boosting lead generation and outreach effectiveness.

[Snov.io](http://snov.io/) in Clay allows users to enrich person data from LinkedIn URLs or email addresses, and find email addresses based on domain and job title.

## **Enriching data with** [**Snov.io**](http://Snov.io)

1.  While in a Clay table, click `Add enrichment` and search for `Snov.io`.
2.  Under `Integrations`, select one of the [Snov.io](http://Snov.io) options.

### **`Action` Enrich person from LinkedIn URL**

Enriches person data from a LinkedIn profile URL using [Snov.io](http://Snov.io)'s comprehensive database, returning contact information, employment details, and social profiles.

**Inputs**

-   **Contact LinkedIn URL:** The person's LinkedIn profile URL (must be a public profile URL)

**Outputs**

-   Contact LinkedIn URL
-   Contact - Full Name, First Name, Last Name
-   Contact Email - Work, Personal
-   Email Validity Status
-   Company Name, Industry, Size, Type
-   Company LinkedIn URL
-   Domain - Website
-   Contact Job Title
-   Contact Location - Country, State, City, Zip Code

### **`Action` Enrich person from email**

Enriches person data using an email address to retrieve professional information, employment history, and location details.

**Inputs**

-   **Contact Email - Work** or **Contact Email - Personal:** The person's email address

**Outputs**

-   Contact - Full Name, First Name, Last Name
-   Contact Employment Start & End Date
-   Contact Location - Country, State, City, Zip Code, Office Address
-   Contact LinkedIn URL
-   Company Name, Industry, Size, Type
-   Company LinkedIn URL
-   Contact Job Title
-   Domain - Website

### **`Action` Find email**

Finds and retrieves email addresses for a specific person using their name and company domain.

**Inputs**

-   **Contact - Full Name:** The person's complete name
-   **Domain - Website:** The company's website domain (e.g., [`company.com`](http://company.com))

**Outputs**

-   Contact Email - Personal, Work
-   Contact - Full Name, First Name, Last Name
-   Contact Twitter URL
-   Contact LinkedIn URL
-   Company Name
-   Domain - Website
-   Email Validity Status
-   Contact Job Title

### **`Action` Find emails from domain**

Discovers email addresses at a company based on domain and optionally filters by job title to find specific roles.

**Inputs**

-   **Domain - Website:** The company's website domain (e.g., `company.com`)
-   **Contact Job Title (Optional):** Filter by specific job titles or roles (e.g., "Marketing Manager", "VP of Sales")

**Outputs**

-   Contact Email - Personal, Work
-   Contact - Full Name, First Name, Last Name
-   Contact Twitter URL
-   Contact LinkedIn URL
-   Company Name
-   Domain - Website
-   Email Validity Status
-   Contact Job Title

### **`Action` Find company domain**

Identifies and retrieves a company's website domain from their company name.

**Inputs**

-   **Company Name:** Name of the company

**Outputs**

-   Domain - Website

### **`Action` Verify email**

Validates email address deliverability and checks if emails are valid, helping maintain list hygiene and reduce bounce rates.

**Inputs**

-   **Email Address:** The email address to verify

**Outputs**

-   Contact Email - Work, Personal
-   Email Validity Status
-   Contact Job Title
-   Domain - Website
-   Contact Location - State
