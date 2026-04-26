---
title: Lemlist integration
source_url: https://university.clay.com/docs/lemlist-integration-overview
last_synced: 2026-04-26T01:40:15.254Z
upstream_hash: 103faa28bb97436ba51089c658cf5450bbea4ae85b1b96b01dfbf0e84b6198c2
---

# Lemlist integration

Automated multichannel outreach tool.

The Lemlist integration in Clay allows users to send per-lead data from Clay (including personalized email copy) directly to Lemlist for email campaigns.

## Setting up the Lemlist integration

1.  While in a Clay table, click `Add enrichment` and search for Lemlist.
2.  Under `Integrations`, select one of the Lemlist options.
3.  In the modal, you will be asked to `Select Lemlist account`.
    1.  If you haven’t already connected, click `+ Add account` and enter your Lemlist API key.
    2.  You can find your API key [here](https://www.notion.so/Lemlist-1227e66eb01480ffaadad64810aabda3?pvs=21), under `Settings` → `Integrations`.

**Note:** To use this integration, you must already have a [campaign](https://help.lemlist.com/en/articles/4452686-create-a-campaign) set up in Lemlist.

## Using the Lemlist integration

### `Action` Add Lead to Campaign

**Inputs**

-   **Campaign ID**
-   **Other optional inputs include:**
    -   Email Address
    -   LinkedIn URL
    -   Name
    -   Phone Number
    -   And more…

**Run settings**

-   **Auto-update**
-   **Only run if:** The enrichment will only run if conditions are met. ([Learn more about conditional formulas here!](https://www.clay.com/university/lesson/ai-formulas-conditional-runs-clay-101))

### **`Action` Update Lead in Campaign**

**Inputs**

-   **Campaign ID**
-   **Email Address or Lead ID**
-   **Other optional inputs include:**
    -   LinkedIn URL
    -   Name
    -   Phone Number
    -   And more…

**Run settings**

-   **Auto-update**
-   **Only run if:** The enrichment will only run if conditions are met. ([Learn more about conditional formulas here!](https://www.clay.com/university/lesson/ai-formulas-conditional-runs-clay-101))

### **`Action` Lookup Lead in Campaign**

Check if lead exists in a campaign in Lemlist via email.

**Inputs**

-   **Email Address or Lead ID**

**Run settings**

-   **Auto-update**
-   **Only run if:** The enrichment will only run if conditions are met. ([Learn more about conditional formulas here!](https://www.clay.com/university/lesson/ai-formulas-conditional-runs-clay-101))
