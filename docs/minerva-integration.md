---
title: Minerva integration
description: Automatically acquire LinkedIn URLs using professional identifiers
  and validate them with confidence scores.
last_synced: 2026-04-26T01:40:22.462Z
---

# Minerva integration

Automatically acquire LinkedIn URLs using professional identifiers and validate them with confidence scores.

The Minerva Integration enhances contact and demographic information by filling gaps and verifying data—including professional profiles and social media details—to provide comprehensive profiles.

With this integration, you can automatically acquire professional social profile URLs using professional identifiers and validate them with confidence scores, improving your networking and outreach efforts.

## **Enriching data with Minerva**

1.  While in a Clay table, click `Add enrichment` and search for `Minerva`.
2.  Under `Integrations`, select one of the Minerva options.
    -   If you have your own account, click `+ Add account` and go through authentication. Otherwise, use the Clay provided key.

### `Action` Enrich person

Provides comprehensive profiles by supplementing missing or incomplete contact and demographic information.

**Inputs**

-   **Full name:** The full name of the person you are trying to enrich (Required)
-   **Email:** The person's personal or work email address (Required if phone number is not provided)
-   **Phone number:** The phone number of the person you are trying to enrich (Required if email is not provided)

**Output**

-   **Match score and validation**
-   **Personal information:**
    -   Name details
    -   Age
    -   Gender
-   **Contact information:**
    -   Email addresses
    -   Phone numbers
-   **Social media profiles:**
    -   LinkedIn
    -   Facebook
-   **Professional details:**
    -   Work experience
    -   Education history
-   **Demographics:**
    -   Age
    -   Gender
    -   Marital status
-   **Additional information:**
    -   Remote work status
    -   Retirement status
    -   Unique identifiers (Minerva IDs)

### `Action` Find professional profile

Uses email addresses or phone numbers to automatically find and validate LinkedIn profiles, enabling efficient contact data enrichment and professional networking.

**Inputs**

-   **Email:** Personal or work email address of the person (Required if phone not provided)
-   **Phone number:** Phone number of the person (Required if email not provided)
-   **Full name (Optional):** The person's full name (increases match accuracy)

**Output**

-   Direct link to the person's professional profile
-   **Match score:** Confidence level of the match (`0-100`)
-   **Match status:** Whether a profile was successfully matched
-   **Validation status:** Indicates if the provided information is valid and processable

### `Action` Enrich person wealth & income

Finds a person's estimated income tier and net worth tier based on their professional profile or contact details. Available on all paid plans (10 credits per enriched row).

**Inputs** (one of the following combinations is required)

-   **Professional profile URL:** The person's professional profile URL
-   **Full name + Email:** The person's full name and personal or work email address
-   **Full name + Phone number:** The person's full name and phone number

**Output**

-   **Estimated income flag:** Income tier — High Earner ($250k–$500k annual income), Very High Earner ($500k–$1M), or Ultra High Earner ($1M+)
-   **Estimated wealth flag:** Net worth tier — High Net Worth Individual ($2M–$5M wealth), Very High Net Worth Individual ($5M–$20M), or Ultra High Net Worth Individual ($20M+)
-   **Match score:** Confidence level of the match (`0–100`)
-   **Social profiles:** Professional profile URL, Facebook URL, and other social profile URLs
-   **Professional details:** Professional title and industry
-   **Location:** Current city and state
-   **Contact information:** Personal and professional email addresses, phone numbers

### **Run settings**

-   **Auto-update**
-   **Only run if:** The enrichment will only run if conditions are met. ([Learn more about conditional formulas here!](https://www.clay.com/university/lesson/ai-formulas-conditional-runs-clay-101))
