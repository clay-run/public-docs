---
title: ContactOut integration
source_url: https://university.clay.com/docs/contactout-integration
description: Find accurate professional emails and phone numbers.
last_synced: 2026-04-27T18:09:39.654Z
upstream_hash: a850a8ef3467f1e1b3591324cb9d465118b43533d1c335b79dcc17d617350f2e
---

# ContactOut integration

Find accurate professional emails and phone numbers.

ContactOut is a lead generation tool for finding accurate contact information and professional data.

With this integration, you can enrich your Clay data with verified email addresses, phone numbers, and other professional details about your prospects.

## **Enriching data with ContactOut**

1.  While in a Clay table, click `Add enrichment` and search for `ContactOut`.
2.  Under `Integrations`, select one of the ContactOut options.
3.  In the modal, you will be asked to `Select ContactOut account`.
    -   If you have your own account, click `+ Add account` and go through authentication. Otherwise, use the Clay provided key.

### `Action` Find Mobile Number from Profile

Use this action to retrieve a person’s mobile number directly from their profile URL.

**Inputs**

-   **Social URL**: Input the profile URL of the person whose mobile number you want to retrieve.

### `Action` Find Personal Email from Profile

This action retrieves a person’s personal email address from their profile URL.

**Inputs**

-   **Social URL**: Enter or select the profile URL of the contact.

### `Action` Find social URL from personal email

This action retrieves a person’s social media profile from their personal email.

**Inputs**

-   **Personal email**

### **Run settings**

-   **Auto-update**
-   **Only run if:** The enrichment will only run if conditions are met. ([Learn more about conditional formulas here!](https://www.clay.com/university/lesson/ai-formulas-conditional-runs-clay-101))
