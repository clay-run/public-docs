---
title: LiveData integration
description: Find social profiles using work email or name.
last_synced: 2026-04-26T01:40:16.563Z
---

# LiveData integration

Find social profiles using work email or name.

LiveData is a comprehensive tool for social data enrichment.

With this integration, you can find social profiles using various data points like work email, name, and company information.

## **Enriching data with LiveData**

1.  While in a Clay table, click `Add enrichment` and search for `LiveData`.
2.  Under `Integrations`, select one of the LiveData options.
3.  In the modal, you will be asked to `Select LiveData account`.
    -   If you haven't already connected your LiveData account, click `+ Add account` and go through authentication.
    -   If you have your own account, click `+ Add account` and go through authentication. Otherwise, use the Clay provided key.

### `Action` Find Professional Profile

Use this action to find a person's professional profile using their work email or full name.

**Note:** When using full name as input without an email address, you must also include at least one company identifier — company name, company professional URL, company domain, or company ticker. Providing a full name alone (with no email or company context) returns a "Missing input" error.

**Inputs**

-   **Person's work email (Optional)**
-   **Person's full name (Optional)**
-   **Company name (Optional)**
-   **Company professional URL (Optional)**
-   **Company domain (Optional)**
-   **Company ticker (Optional)**
-   **Person's professional URL (Optional)**
-   **Person's job title (Optional)**
-   **School name (Optional)**
-   **Limit (Optional):** The maximum and default is 5.

### **Run settings**

-   **Auto-update**
-   **Only run if:** The enrichment will only run if conditions are met. ([Learn more about conditional formulas here!](https://www.clay.com/university/lesson/ai-formulas-conditional-runs-clay-101))
