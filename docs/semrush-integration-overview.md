---
title: Semrush integration
source_url: https://university.clay.com/docs/semrush-integration-overview
last_synced: 2026-04-26T01:40:38.598Z
upstream_hash: a594d2f29fce17bfb7ca0762cc8162094cb3ad983d438dfccae6539f20a52f6e
---

# Semrush integration

Online marketing platform boosting visibility, rankings, and strategy optimization.

Semrush is a comprehensive digital marketing tool for competitive analysis, SEO, content marketing, and market research.

With this integration, you can analyze website traffic, discover traffic sources, identify competitors, and track social media engagement.

## **Enriching data with Semrush**

1.  While in a Clay table, click `Add enrichment` and search for `Semrush`.
2.  Under `Integrations`, select one of the Semrush options.
3.  In the modal, you will be asked to `Select Semrush account`.
    -   If you have your own account, click `+ Add account` and go through authentication. Otherwise, use the Clay provided key.

### `Action` Get company traffic sources

Use this action to retrieve a breakdown of traffic by source (direct, referral, search, social, and paid).

**Inputs**

-   **Domain**
-   **Country** **(Optional)**
-   **Display month** **(Optional)**
-   **Traffic type** **(Optional)**
-   **Traffic channel** **(Optional)**
-   **Device type** **(Optional)**

### `Action` Get company social media engagement

Use this action to analyze social media performance across platforms like Facebook, Twitter, Instagram, and YouTube.

**Inputs**

-   **Domain**
-   **Country** **(Optional)**
-   **Display month** **(Optional)**
-   **Device type** **(Optional)**

### `Action` Get traffic analytics

Use this action to analyze website traffic volume and engagement metrics.

**Inputs**

-   **Company URL**
-   **Country** **(Optional)**
-   **Display month** **(Optional)**
-   **Device type** **(Optional)**

### `Action` Get company top pages

Use this action to identify the highest-performing pages on a website.

**Inputs**

-   **Company domain**
-   **Display limit**
-   **Country** **(Optional)**
-   **Display month** **(Optional)**
-   **Device type** **(Optional)**
-   **Target type** **(Optional)**

### `Action` Get company website traffic's geographic distribution

Use this action to see where website visitors are coming from by country.

**Inputs**

-   **Company domain**
-   **Display limit**
-   **Country** **(Optional)**
-   **Geo type** **(Optional)**
-   **Display month** **(Optional)**
-   **Device type** **(Optional)**

### `Action` Get competitors in paid search

Use this action to identify competitors bidding on similar keywords in paid search campaigns.

**Inputs**

-   **Company domain**
-   **Country**
-   **Display month** **(Optional)**

### **Run settings**

-   **Auto-update**
-   **Only run if:** The enrichment will only run if conditions are met. ([Learn more about conditional formulas here!](https://www.clay.com/university/lesson/ai-formulas-conditional-runs-clay-101))
