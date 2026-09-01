---
title: HG Insights integration
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

**Credit cost**

The `Source Companies by product usage with HG Insights` action charges **8 credits per company per product matched**, capped at your **Max products per company** setting. A company that uses only 1 of your selected products costs 8 credits — the same as a company that uses all 7. Selecting more products only increases total credit spend if companies actually match those additional products.

Running separate per-product searches does not reduce costs. A company that matches 3 of your selected products is billed 24 credits (3 × 8) whether you run one combined search or three separate per-product searches — but in three separate runs, that company appears in each run and is billed each time. **One combined run across all products is the most efficient approach.**

**Lower-cost alternative for building a company universe**

If your goal is to build a list of companies using a vendor's products — without needing to know exactly which products each company uses — the built-in **Technographics** filter in [Find Companies](find-companies.md) costs **3 credits per matching company row** (powered by [BuyerCaddy](https://university.clay.com/docs/buyercaddy-integration)). Use `Source Companies by product usage with HG Insights` when you specifically need the full product breakdown per company.

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

**Checking an existing account list for technology usage**

If you already have a list of companies — for example, accounts imported from Salesforce or a CSV — you can run this enrichment against each row in your table:

1.  In your table, click `Add enrichment`, search for `HG Insights`, and select `Verify technology usage`.
2.  For the **Company domain or HG company ID** input, select the column in your table that contains the company's website domain. The enrichment runs once per row using that column's value as the lookup.
3.  Under **Products**, use the filter to select the specific product or competitor you want to check for.
4.  Click **Save and run** to execute the check across your rows.

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

### "Required inputs missing" error in the Verify Product Usage waterfall

Unlike other tech stack providers that scan all technologies on a domain, the HG Insights **Verify technology usage** action requires you to specify exactly which products to check for — the **Products** field is required. If HG Insights is added to the **Verify Product Usage** waterfall without this field configured, a "Required inputs missing" error appears.

This typically happens when the products you want to look up don't appear in HG Insights' product catalog. To resolve this:

-   **Check HG Insights' data directory.** Browse [HG Data Discovery](https://discovery.hgdata.com/) to see what products and categories HG Insights has indexed, then configure the **Products** field using a product from that catalog.
-   **Remove HG Insights from the waterfall.** If you're running a broad tech stack enrichment and aren't targeting specific named products, click the **delete icon** next to HG Insights in the waterfall sequence to remove it. The remaining providers will run normally without requiring a product selection.

### Technology not found in HG Insights

HG Insights has strong coverage for widely-adopted enterprise technologies, but niche, newer, or less-tracked tools may not appear in its database. If a technology you're looking for returns no results, two fallback approaches work well in Clay:

**1. Try BuiltWith**

BuiltWith detects technologies by scanning a company's public website, so it often has coverage for front-end tools — JavaScript libraries, marketing pixels, and other client-side software — that HG Insights may not track. Before running the enrichment, go to [builtwith.com](https://builtwith.com/) and search the technology name directly. If it appears as a "Technology result" (not just a company overview), BuiltWith has coverage for it. You can then use the [BuiltWith Find Technology Stack](https://university.clay.com/docs/builtwith-integration-overview) action in Clay with the technology name as a keyword filter, or download the list of companies using it from BuiltWith's site and import them into Clay.

**2. Use Claygent**

For technologies not tracked by any database provider, a [Claygent](https://university.clay.com/docs/claygent-builder) column can scan the web for evidence. Add a Claygent column to your table, use the company domain as an input variable, and prompt it to search the company's website and public sources for signs of the technology — for example: *"Does {{company_domain}} use [technology name]? Search the company's website, case studies, and press mentions, and return yes or no with the evidence you found."* Claygent returns structured output, so you can add a boolean field for the yes/no result and a text field for the supporting evidence.

### HG Insights does not return the correct parent company or Group HQ

HG Insights derives corporate hierarchy data — domestic parent, corporate parent, and Group HQ — from its own proprietary database. For some companies, particularly subsidiaries with their own distinct domain (common in financial services, regional holding structures, or recently-acquired companies), HG Insights may not have the parent-subsidiary relationship indexed. In these cases, **Enrich company** returns the queried domain as its own Group HQ, even when a larger real-world parent exists.

**Workaround: add a Claygent fallback column**

Use a [Claygent](claygent-builder.md) column to research the parent company on the web, and set it to run only on rows where HG Insights' hierarchy data is missing or incomplete:

1. Run the **Enrich company** action first to populate the Group HQ fields.
2. Add a **Claygent** column. Use the company domain as an input variable and prompt it to return the parent company domain — for example: *"What is the ultimate parent company domain for {{company_domain}}? If this company is a subsidiary operating under a larger parent, return only the root domain of the parent (for example, parent.com). If this company has no parent, return the same domain."*
3. In the Claygent column's **Run Settings**, add an **Only run if** condition so it fires only when HG Insights returned incomplete hierarchy data:
   - Group HQ domain is empty, **OR**
   - Group HQ domain equals the company domain (meaning HG Insights considers the company to be its own Group HQ)
4. In the model selector, choose **clay-helium** (1 credit per row) — it is sufficient for straightforward parent company lookups and keeps credit costs low.

This ensures Claygent only runs on rows where HG Insights either has no hierarchy data or did not find a parent, so you are not spending credits on rows HG Insights already resolved correctly.
