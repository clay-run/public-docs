---
title: LiveData integration
source_url: https://university.clay.com/docs/livedata-integration
description: Live professional profile enrichment.
last_synced: 2026-04-26T01:40:13.000Z
---

# LiveData integration

Live professional profile enrichment.

LiveData is a real-time data enrichment tool that provides up-to-date professional profile information for contacts. With this integration, you can find social profiles using various data points like email, name, company domain, and more.

## Connecting to LiveData

1.  In the home sidebar, click `Settings` → `Connections`.
2.  Click `Add connection` and search for `LiveData`.
3.  Log in to your Livedata account or click `Use Clay's API key`.
    -   If you have your own account, click `+ Add account` and go through authentication. Otherwise, use the Clay provided key.

## Enriching data with LiveData

1.  While in a Clay table, click `Add enrichment` and search for `Livedata`.
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
