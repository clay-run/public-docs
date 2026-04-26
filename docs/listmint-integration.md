---
title: Listmint integration
source_url: https://university.clay.com/docs/listmint-integration
description: Verify email validity, including automatic catch-all verification
  for domains with catch-all settings.
last_synced: 2026-04-26T01:40:16.231Z
upstream_hash: 492f6b19b721ad9acaa3027b07c62270e5e6656eb60e50919e4d36526e0c48df
---

# Listmint integration

Verify email validity, including automatic catch-all verification for domains with catch-all settings.

Listmint is an email verification service that helps you validate email addresses and improve deliverability in your outreach campaigns.

With this integration, you can verify email validity, including automatic catch-all verification for domains with catch-all settings.

## **Enriching data with Listmint**

1.  While in a Clay table, click `Add enrichment` and search for `Listmint`.
2.  Under `Integrations`, select one of the Listmint options.
3.  In the modal, you will be asked to `Select Listmint account`.
    -   If you haven't already connected your Listmint account, click `+ Add account`, enter your API key, and click `Connect` to authenticate.

### `Action` Verify email

Use this action to verify if email addresses have valid inboxes, including automatic catch-all verification for addresses in catch-all domains.

**Inputs**

-   **Email:** The email address to verify

**Output**

-   **Message:** Confirmation message about the verification process
-   **Results:** Array containing verification results for each email:
    -   **Email:** The email address that was verified
    -   **Result:** The verification status. Possible values include:
        -   `valid` – Email has a valid inbox
        -   `catch_all_valid` – Email is valid and in a catch-all domain
        -   `invalid` – Email does not have a valid inbox
        -   `catch_all_invalid` – Email is invalid and in a catch-all domain

The action displays a visual indicator in the column:

-   ✅ Valid – For `valid` or `catch_all_valid` results
-   ❌ Invalid – For `invalid` or `catch_all_invalid` results

### **Run settings**

-   **Auto-update**
-   **Only run if:** The enrichment will only run if conditions are met. ([Learn more about conditional formulas here!](https://www.clay.com/university/lesson/ai-formulas-conditional-runs-clay-101))
