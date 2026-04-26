---
title: Crossbeam integration
source_url: https://university.clay.com/docs/crossbeam-integration
description: Import accounts and customize outreach based on overlap with key partners.
last_synced: 2026-04-26T01:39:49.408Z
upstream_hash: 1068d65642f55695318ca41af557c18a0999ff0e3e59cbe643318da89500e650
---

# Crossbeam integration

Import accounts and customize outreach based on overlap with key partners.

The Crossbeam integration imports accounts based on overlaps with key partners and generates customized outreach that syncs with your sales engagement tools.

This feature helps your sales team deliver partner-aligned messages to speed up deal cycles and support ecosystem-led growth.

## **Creating a table with Crossbeam**

1.  In a workbook, click `+ Add` at the bottom.
2.  Search for `Crossbeam` and select from the results.
3.  In the modal, you will be asked to `Select Crossbeam account`.
    -   If you haven't already connected your Crossbeam account, click `+ Add account` and go through authentication.

### `Source` Import from Crossbeam

Import accounts that overlap with a specific partner.

**Inputs**

-   **Organization**
-   **Partner:** Limits the results to a specific partner.
-   **Populations**
-   **Limit:** Sets the maximum number of overlaps to import (default: 1,000).

## **Enriching data with Crossbeam**

1.  While in a Clay table, click `Add enrichment` and search for `Crossbeam`.
2.  Under `Integrations`, select one of the Crossbeam options.
3.  In the modal, you will be asked to `Select Crossbeam account`.
    -   If you haven't already connected your Crossbeam account, click `+ Add account` and go through authentication.

### `Action` **Enrich Company with Partner Data**

Use this action to get data about all Crossbeam partners linked to a company, including their relationship status (e.g., Customer, Prospect, Opportunity).

**Inputs**

-   **Organization**
-   **Company domain**
-   **Partner (Optional):** Limits the results to a specific partner.
-   **Partner populations**

### **Run settings**

-   **Auto-update**
-   **Only run if:** The enrichment will only run if conditions are met. ([Learn more about conditional formulas here!](https://www.clay.com/university/lesson/ai-formulas-conditional-runs-clay-101))

## FAQs

### **What fields are imported from Crossbeam?**

Clay imports all fields available through Crossbeam's account overlaps endpoint, including partner owner, record email, record website, Crossbeam ID, and additional data points.

### **Is re-authentication with Crossbeam required for each new table?**

No. Once you authenticate Crossbeam as a source in Clay, you can use it for any new table without re-authenticating.

### **Can multiple partners be selected in a single table?**

Yes. You can include multiple partners in a single table by adding a separate source for each partner. This lets you create tables with data from multiple partners.
