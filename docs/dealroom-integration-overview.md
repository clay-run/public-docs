---
title: Dealroom.co integration
source_url: https://university.clay.com/docs/dealroom-integration-overview
description: Startup and tech ecosystem intelligence platform.
last_synced: 2026-04-26T01:39:52.634Z
upstream_hash: 0c1af7c8808bf5e5b8b5bbc1b27502baea97080d02e8487c79929477f7e6dc89
---

# Dealroom.co integration

Startup and tech ecosystem intelligence platform.

[Dealroom.co](http://Dealroom.co) is a data intelligence platform for discovering and tracking innovative companies and their funding activities.

With this integration, you can enrich your Clay tables with company valuation data, investor information, fundraising details, and more from [Dealroom.co](http://Dealroom.co)'s extensive database.

## **Enriching data with** [**Dealroom.co**](http://Dealroom.co)

1.  While in a Clay table, click `Add enrichment` and search for `Dealroom`.
2.  Under `Integrations`, select one of the [Dealroom.co](http://Dealroom.co) options.
3.  In the modal, you will be asked to `Select Dealroom account`.
    -   If you have your own account, click `+ Add account` and go through authentication. Otherwise, use the Clay provided key.

### `Action` Get company investors

Use this action to get a company's investors from [dealroom.co](http://dealroom.co/).

**Inputs**

-   **Company domain**

### `Action` Get company valuation

Use this action to get valuation data for a company from [dealroom.co](http://dealroom.co/).

**Inputs**

-   **Company domain**

### `Action` Get fundraising data for company

Use this action to get fundraising data for a company from [dealroom.co](http://dealroom.co/).

**Inputs**

-   **Company domain**

### `Action` Get investor funds

Use this action to get a list of funds that an investor has received.

**Inputs**

-   **Company domain**

### `Action` Get investors investments

Get a list of companies that an investor has invested in.

**Inputs**

-   **Company domain**

### **Run settings**

-   **Auto-update**
-   **Only run if:** The enrichment will only run if conditions are met. ([Learn more about conditional formulas here!](https://www.clay.com/university/lesson/ai-formulas-conditional-runs-clay-101))
