---
title: HG Insights integration
source_url: https://university.clay.com/docs/hg-insights-integration-overview
description: Uncover enterprise-grade technographic and parent company data
  while enriching foundational company data.
last_synced: 2026-04-26T01:40:07.697Z
---

# HG Insights integration

Uncover enterprise-grade technographic and parent company data while enriching foundational company data.

The HG Insights integration brings enterprise-grade technology intelligence data points, enabling teams to access proprietary data such as:

-   **Technology Intelligence:** In-depth details about a company's tech stack that typically is hard to find.
-   **Firmographic Data:** Insights into company size, revenue, and more.
-   **Corporate Hierarchy Data Points:** Accurate mapping of parent-child relationships within target companies.

## **Creating a table with HG Insights**

1.  In a workbook, click `+ Add` at the bottom.
2.  Search for `HG Insights` and select from the results.
3.  In the modal, you will be asked to `Select HG Insights account`.
    -   If you haven't already connected your HG Insights account, click `+ Add account` and go through authentication.

### `Source Companies by product usage with HG Insights`

Build lists of companies based on what technology they use, including "back of house" tools that you won't find on a website.

**Inputs**

-   **Vendor domains**
-   **Product categories**
-   **Product attributes**
-   **Products**
-   **Max products per company**
-   **Max companies:** Limits the number of companies returned. Defaults to **100** if not specified — increase this value if you need to capture more target accounts.
-   **Revenue**
-   **Employee count**
-   **Allowed industries (HG Insights):** Filter companies by their HG Insights-defined industry.
-   **Allowed industries (NAICS):** Filter companies by their NAICS-defined industry.
-   **Allowed industries (SIC):** Filter companies by their SIC-defined industry.
-   **Allowed locations**
-   **Domains to exclude**
-   **Include total product locations count**
-   **Include total product signals count**
-   **Include product first verified date**

## **Enriching data with HG Insights**

1.  While in a Clay table, click `Add enrichment` and search for `HG Insights`.
2.  Under `Integrations`, select one of the HG Insights options.
3.  In the modal, you will be asked to `Select HG Insights account`.
    -   If you have your own account, click `+ Add account` and go through authentication. Otherwise, use the Clay provided key.

### `Action` Enrich company

Enrich your company records to provide you critical, hard-to-find data, such as parent-child company relationships and revenue numbers, alongside foundational details like the company domain.

**Inputs**

-   **Company domain or HG company ID**

### `Action` Verify technology usage

Determine whether specific companies use a particular product.

For example, you can find out if a company uses Salesforce for their CRM or Netsuite for their ERP. This helps you better targeted users based on their technology stack.

**Inputs:**

-   **Company domain or HG company ID**
-   **Vendor domains (Optional)**
-   **Product categories (Optional)**
-   **Product attributes (Optional)**
-   **Products**
-   **Include total product locations count (Optional)**
-   **Include total product signals count (Optional)**
-   **Include product first verified date (Optional)**
-   **Max product (Optional)**

### `Action` **Find company corporate structure**

Find all corporate parents, domestic parents, and lower level entities managed by a group headquarters company.

-   **Company domain or HG company ID**

### `Action` **Find domain from company name**

Guess the domain of a company based on their company name.

**Inputs**

-   **Company name**
-   **Location (Optional)**

### **Run settings**

-   **Auto-update**
-   **Only run if:** The enrichment will only run if conditions are met. ([Learn more about conditional formulas here!](https://www.clay.com/university/lesson/ai-formulas-conditional-runs-clay-101))

## How HG Insights detects technologies

HG Insights uses a broader set of signals than tools that rely solely on website scanning. Instead of crawling public-facing frontend code, HG Insights mines signals from job postings, resumes, white papers, cloud data, SDK fingerprints, server events, and historical install data. This means HG Insights can surface backend and internally-deployed technologies that aren't visible in a company's public website source.

By contrast, tools like [BuiltWith](https://university.clay.com/docs/builtwith-integration-overview) detect technology by scanning a website's public source code, which works well for client-side tools (e.g., marketing pixels, JavaScript libraries) but may miss technologies deployed behind the login wall or on the server side.

To verify a technology detected by HG Insights, you can search the company's website (e.g., privacy policy or terms of service pages) for the technology name, or use a targeted query like `site:[DOMAIN] "[TECHNOLOGY_NAME]"`.

## Troubleshooting

### Fewer companies returned than expected

The `Source Companies by product usage` action returns up to **100 companies by default**. If your target accounts aren't all appearing, increase the **Max companies** input to capture more results. Keep in mind that a higher limit will consume more enrichment credits.
