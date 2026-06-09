---
title: Surfe integration
description: Enrich company profiles and individual professional profiles by
  filling in missing data.
last_synced: 2026-04-26T01:40:45.081Z
---

# Surfe integration

Enrich company profiles and individual professional profiles by filling in missing data.

Surfe enhances lead and contact profiling by extracting and verifying contact information such as emails and mobile numbers from multiple data sources including professional socials and company details.

It enriches company profiles and individual professional profiles by filling in missing data, enabling comprehensive lead qualification and targeted outreach.

## **Enriching data with Surfe**

1.  While in a Clay table, click `Add enrichment` and search for `Surfe`.
2.  Under `Integrations`, select one of the Surfe options.

### **`Action` Find email**

The "Find email"feature streamlines the identification and collection of verified email addresses for company owners and founders using enriched company and personal data inputs.

**Inputs**

-   **Full name:** The person's complete name
-   **Company domain:** The company's website domain (e.g., `company.com`)
-   **OR**
-   **Professional URL:** The person's profile URL (must be a public profile URL)

### **`Action` Find mobile phone**

The "Find mobile phone number"action enriches lead profiles by searching for and extracting mobile numbers company data.

**Inputs**

-   **Professional URL:** Profile URL of the person you want to find a phone number for.

### **`Action` Find people at company**

Helps identify senior marketing and advertising leads within target organizations by leveraging domain-based searches and waterfalling with additional data sources for enhanced coverage.

**Inputs**

-   **Company domain:** The website domain of the target company (e.g., `microsoft.com`)
-   **Job title (Optional):** Filter by specific job titles or roles (e.g., "Software Engineer", "Product Manager")
-   **Management level (Optional):** Filter by seniority level (e.g., C-suite, Director, Manager)
-   **Department title (Optional):** Filter by specific departments (e.g., Engineering, Sales, Marketing)
-   **Department function (Optional):** Filter by functional areas
-   **Company size (Optional):** Filter by company employee count ranges
-   **People locations (Optional):** Filter by geographic locations of employees
-   **Company locations (Optional):** Filter by company office locations

### **`Action` Find professional profile**

Uses a combination of name and company information as a secondary enrichment step to find profiles when initial attempts fail.

**Inputs**

-   **Full Name:** Contact's first and last name
-   **Company Domain:** Website domain of the company
-   **Company Name:** Name of the company

### **`Action` Enrich company**

Enrich a company using its domain to get firmographic and company data.

**Inputs**

-   **Company domain**

## FAQs

### A downstream column shows `ERROR_MISSING_INPUT` for rows sourced from Surfe but not for rows from other sources — why?

**Cause:** Surfe returns contact fields using camelCase names — for example, `firstName` and `lastName` — while most other Clay integrations return those same fields as `first_name` and `last_name`. Clay's table UI normalizes both naming conventions to display as "First Name" and "Last Name," so the difference isn't visible at a glance. A downstream column (for example, HubSpot Lookup Contact or Enrich Contact) configured to read `first_name` will find no value in Surfe-sourced rows because the field is stored as `firstName`.

**Fix:** In the downstream column's input field, use the `||` fallback operator to accept either naming convention:

-   Instead of `first_name`, enter `first_name || firstName`
-   Instead of `last_name`, enter `last_name || lastName`

The `||` operator returns the first non-empty value, so the same column works whether the row came from Surfe (camelCase) or another source (snake_case).

Alternatively, add an intermediate formula column that extracts and normalizes the field before passing it to the downstream enrichment.
