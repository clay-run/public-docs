---
title: Zeliq integration
source_url: https://university.clay.com/docs/zeliq-integration
description: Verify phone numbers and email addresses in the EMEA region.
last_synced: 2026-04-26T01:40:58.451Z
upstream_hash: 314affc1289d993a8ba0ed0487b545b3d2a6d6447f7f9ba3235409ce87adabe1
---

# Zeliq integration

Verify phone numbers and email addresses in the EMEA region.

Zeliq enhances contact data management by locating and validating phone numbers and email addresses linked to professional profiles, with particular efficacy in EMEA markets and specialized industries like remodeling and construction.

With this integration, you can find and verify phone numbers and email addresses using social profiles or company domain information, ensuring accuracy and efficiency in lead generation workflows.

## **Enriching data with Zeliq**

1.  While in a Clay table, click `Add enrichment` and search for `Zeliq`.
2.  Under `Integrations`, select one of the actions detailed below.

### `Action` Find Phone Number

Use this action to locate and validate phone numbers associated with professional profiles, with a focus on EMEA coverage.

**Inputs**

-   **Professional profile URL:** Person's professional profile URL (e.g., `https://www.linkedin.com/in/johndoe/`)
-   **Work email:** Person's work email address (e.g., `john.doe@clay.com`)

**Output**

-   Email address
-   Phone numbers (array)
-   Most probable phone number
-   LinkedIn profile URL

### `Action` Find email

Use this action to find and verify work email addresses using either a person's professional profile URL or their full name and company domain, with strong coverage in the EMEA region.

**Inputs**

-   **Professional profile URL:** Person's professional profile URL (e.g., `https://www.linkedin.com/in/johndoe/`). Either this or full name and company domain is required.
-   **Person's full name:** Person's full name. Required along with company domain.
-   **Company domain:** Person's company domain (e.g., `clay.com`). Required along with full name.

**Output**

-   **Company domain:** The domain of the company where the person works
-   **Emails:** List of found email addresses with verification status
-   **First name:** Person's first name
-   **Last name:** Person's last name
-   **LinkedIn profile URL:** Person's LinkedIn profile URL
-   **Most probable email:** The most likely correct email address
-   **Most probable email status:** Verification status of the most probable email

### **Run settings**

-   **Auto-update**
-   **Only run if:** The enrichment will only run if conditions are met. ([Learn more about conditional formulas here!](https://www.clay.com/university/lesson/ai-formulas-conditional-runs-clay-101))
