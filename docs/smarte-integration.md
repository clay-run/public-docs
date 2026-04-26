---
title: SMARTe integration
source_url: https://university.clay.com/docs/smarte-integration
last_synced: 2026-04-26T01:40:41.821Z
upstream_hash: 369862b81367fee6ed0e6985f89a7431f263b83e23f24bdedd8b1ac4ebf3eff2
---

# SMARTe integration

Enrich company details and find emails/phone numbers.

SMARTe is a data enrichment tool that finds accurate contact and company information.

This integration allows you to enrich your data with company details, contact information, mobile numbers, and work emails.

## **Enriching data with SMARTe**

1.  While in a Clay table, click `Add enrichment` and search for `SMARTe`.
2.  Under `Integrations`, select one of the SMARTe enrichment options.
3.  In the modal, you will be asked to `Select SMARTe account`.
    -   If you have your own account, click `+ Add account` and complete authentication. Otherwise, use the Clay provided key.

### `Action` Enrich Company

Use this action to enrich company data using a social URL, personal email, or full name with company information.

**Inputs**

-   **Company name (Optional)**
-   **Company URL (Optional)**
-   **Company social URL (Optional)**

### `Action` Enrich Contact

Use this action to enrich contact data using a social URL, personal email, or full name with company information. _Required: Starter Plan or above._

**Inputs**

-   **Person's social URL (Optional)**
-   **Person's email address (Optional)**
-   **Person's full name (Optional)**
-   **Company name (Optional)**
-   **Company URL (Optional)**

### `Action` Find **Mobile Number**

Use this action to find a person's mobile number using their social URL, personal email, or full name with company information. _Required: Starter Plan or above._

**Inputs**

-   **Person's social URL (Optional)**
-   **Person's email address (Optional)**
-   **Person's full name (Optional)**
-   **Company name (Optional)**
-   **Company URL (Optional)**

### `Action` Find Work Email

Use this action to find a person's work email using their social URL, personal email, or full name with company information.

**Inputs**

-   **Person's social URL (Optional)**
-   **Person's email address (Optional)**
-   **Person's full name (Optional)**
-   **Company name (Optional)**
-   **Company URL (Optional)**

### **Run settings**

-   **Auto-update**
-   **Only run if:** The enrichment will only run if conditions are met. ([Learn more about conditional formulas here!](https://www.clay.com/university/lesson/ai-formulas-conditional-runs-clay-101))
