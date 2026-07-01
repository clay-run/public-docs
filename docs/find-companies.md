---
title: Find Companies in Clay
description: Find companies that match your specific criteria within Clay's
  proprietary dataset.
last_synced: 2026-04-26T01:39:58.486Z
---

# Find Companies in Clay

Find companies that match your specific criteria within Clay's proprietary dataset.

The `Find Companies` source lets you build targeted lists of companies using filters like industry, size, location, and keywords.

It's perfect for creating sales prospect lists, identifying competitors, and conducting market research.

**Looking for similarity-based discovery?** You can switch to **Find lookalikes** mode using the mode dropdown in the filter panel header. See [Clay Lookalikes](clay-lookalikes.md) for documentation on the lookalike source and enrichments.

## **Creating a table with Find Companies**

1.  In a workbook, click `+ Add` at the bottom.
2.  Search for `Find Companies`.

## `Source` **Find Companies**

1.  Configure the source to your preferences:
    -   **Industries** to include and exclude
    -   **Company size** — The self-reported size band on the company's profile (e.g., 11–50, 51–200). Select one or more bands from the dropdown.
    -   **Annual revenue ranges** — Filter by revenue brackets from $0–$500K up to $100B+.
    -   **Funding raised** — Filter by total funding raised. Select one or more brackets from Under $1M up to $250M+, or select **Funding unknown** to include companies with no recorded funding data.
    -   **Company types** — Privately Held, Public Company, Partnership, Self Employed, Non Profit, Educational, Self Owned, or Government Agency.
    -   **Keywords** to include or exclude
        -   **Exact phrase matching:** Wrap multi-word terms in single or double quotes to search for that exact phrase. For example, searching for "Google Cloud" finds companies with "Google Cloud" in their description — not just companies that mention Google and cloud separately. Note: Special characters (#, +, !) and stopwords ('a', 'an', 'of', 'the') are stripped out even with quoted phrases.
    -   **Semantic company description** — Enter a free-text description to help rank results based on how closely they match your ideal company profile (e.g., "B2B fintech company selling to mid-market banks").
    -   **Location** — Filter by company office location. Sub-filters: **Country**, **City**, **State or province**, **Region** (EMEA, NAM, APAC, or LATAM), and **Postal code**. Use **Is Headquarters** to restrict results to companies whose primary office is in the specified location. All sub-filters support include and exclude.
    -   **Estimated employee count** — Filter by a numeric count of estimated employees (enter a minimum and/or maximum). This is a separate field from **Company size** — see the [FAQ below](#why-do-company-sizes-and-estimated-employee-count-return-different-results-for-the-same-range) for why the same numeric range can surface different companies.
    -   **AI filters** — Clay-generated attributes applied to company profiles:
        -   **Industries** and **Subindustries** (include or exclude) — see [the FAQ below](#what-are-the-available-ai-subindustry-filter-values) for the full list of AI Subindustry values
        -   **Revenue streams** — e.g., Subscriptions/Recurring, Professional Services, Transaction Fees, Advertising, Licensing/IP
        -   **Business types** — B2B, B2C, or Nonprofit
    -   **Technographics** — Filter by installed technology, powered by [BuyerCaddy](https://university.clay.com/docs/buyercaddy-integration). Costs **3 credits per matching company row** — cheaper in most cases than pulling a broad list and running a technographic enrichment afterward, since you pay only for companies that already match your tech criteria. Technographics data is also included when sending company rows to Audiences; the same 3-credit cost per matching row applies.
        -   **Vendors** — e.g., AWS, Salesforce, HubSpot
        -   **Products** — e.g., Amazon EC2, Salesforce Sales Cloud
        -   **Main categories** and **Parent categories**
        Product and vendor names in the filter come from BuyerCaddy's catalog and may not match a company's public brand name exactly. To identify what a product name refers to, run the search and check the **Vendor** field in the cell details for any returned row — it shows the company behind the product.
    -   **Domain filters:**
        -   **Has domain** — Whether a company has a resolved domain.
        -   **Domain is live** — Whether the company's domain is currently active.
        -   **Domain redirects to another domain** — Whether the domain redirects elsewhere.
    -   **Lookalike companies** *(only visible when editing an existing saved search that already includes seed companies — not shown for new searches)* — Find companies similar to a set of seed companies you provide. Enter up to 10 company identifiers; professional network company profile URLs give the best results, but company domains, Sales Navigator company URLs, and Sales Navigator company IDs are also accepted. Combine with other filters — **Industries**, **Company size**, **Location**, **Company types** — to focus results on a specific segment. For the most targeted results, use seed companies that are closely similar to each other; mixing seeds from very different industries or sizes produces broader results. To start a new lookalike search, use **Find lookalikes** mode instead (see the tip at the top of this page).
    -   **Exclude companies:** Exclude up to 3 different sets of companies from your search using Clay tables, CSVs, or manual lists. You can exclude up to 300,000 companies total (100,000 per source). Exclusions require a company domain or professional network company URL. Available on Launch plan and above.
    -   **Limit results** — Defaults to 10,000. Maximum 10,000.
2.  Click `Preview companies` and `Import to new table` when the results look good.
3.  Select import options:
    -   Add additional enrichments like `Company Headcount Growth` or `Most Recent News`. Any enrichments you select here run on import and **consume Data Credits** (the wizard shows the estimated cost per row). To avoid credit spend at this step, skip optional enrichments and add them as table columns after the table is created instead.
    -   **For trial accounts:** The **Enrich Company** enrichment is pre-selected and cannot be removed during import.
    -   Enable or disable auto-update and auto-dedupe.
4.  Click `Continue`.

**Outputs:**

Each result includes one or more **Structured Location** entries in the cell details with geocoded, normalized fields — so you don't need additional AI columns to parse or reformat location data. These fields work with informal location names like "Greater Chicago Area." Use **Is Headquarters** to identify the company's primary location when multiple entries are returned.

-   **City**
-   **State**
-   **Region**
-   **Country Iso**
-   **Postal Code**
-   **Is Headquarters**

## FAQs

### When should I use Find Companies vs a custom table?

**Find Companies** is a Clay-native sourcing flow that discovers companies from Clay's proprietary dataset based on filters you set — industry, size, location, revenue, and more. When you import results, Clay creates a **Company table** (shown with a building icon in your workbook navigation). Use it when you want to prospect for net-new companies and don't have a list yet.

A **custom table** (shown with the table icon in your workbook) is a blank canvas for data you already have — for example, a list of companies from your CRM, a CSV export, or a manually curated set of records. Create one by clicking `+ Create new` and selecting `Blank table`, or by [importing a CSV](csv-import-overview.md).

**In short:** Choose **Find Companies** when you need to discover new companies from scratch; choose a **custom table** (or CSV import) when you're starting from a list you already own.

**Keeping related tables in the same workbook**

In Clay, a workbook is a container for related tables. It's common to keep linked tables together in one workbook — for example, a Find Companies table and the Find People table created from it — so the workflow is easy to navigate and share as a template. Create a new workbook when you're working on a distinct project or campaign (for example, separate workbooks for different clients or different outbound plays).

### Can I filter by job title or role in company search?

No — `Find Companies` only filters by company-level attributes (industry, size, location, revenue, etc.). There is no job title filter in company search. Job title is a person-level attribute available only in People search.

**To find people with specific roles (e.g., CEO, Founder, Owner) at companies in your list, you have two options:**

-   **From your company table** — Click **Tools** → **Find People at These Companies**. Under **Job title keywords**, enter your target titles comma-separated (e.g., `CEO, Founder, Owner, Co-founder`). This returns only those roles at the companies already in your table.
-   **Start a fresh People search** — Click `+ Add` at the bottom of your workbook, search for `Find People`, and use the **Job title** filter alongside company attributes (industry, size, location).

For more detail on both workflows, see [Guide: Finding companies and people in Clay](finding-companies-and-people-in-clay.md).

### Can I filter companies by the year they were founded?

Founded year is not available as a filter when building a `Find Companies` search — you can't narrow results by founding date before importing.

However, `Find Companies` automatically includes a **Founded** column in your table showing the founding year for each company. Once you've imported your results, you can filter or sort that column to focus on companies founded within a specific range — for example, filtering to companies founded after 2020 to target early-stage startups.

### What if the industry I'm looking for isn't in the dropdown?

The **Industries** filter matches against categories companies have self-selected on their profiles, so niche subcategories may not appear as suggestions. If you can't find your specific industry, select the closest available broader category and use the **Description keywords to include** field to narrow results to companies that operate in your specific niche.

For example, if you're targeting a specialized type of event company that doesn't have its own industry entry, select **Event Services** as the industry and enter keywords describing your target company type in **Description keywords to include**. The combination returns companies that fall under the broader industry AND mention those terms in their profile description.

For more guidance on balancing industry and keyword filters, see [Guide: Finding companies and people in Clay](finding-companies-and-people-in-clay.md).

### Does importing from Find Companies cost credits?

**No, unless you use technographics filters or select enrichments during import.** Importing companies using standard filters — industry, size, location, revenue, company type, AI filters — consumes no Actions and no Data Credits.

If you enable **technographics filters**, each company row that matches your criteria costs **3 Data Credits**.

Any enrichments you select during the import wizard, or add to the table afterward (e.g., finding emails, enriching headcount), consume their own Actions and Data Credits as usual — only pulling company records from Clay's dataset is free.

### Why does my table show fewer rows than the preview count?

**The import may still be in progress.** Find Companies imports process asynchronously — rows are added in batches. If you check right after clicking Import, the row count will be lower than the final total. Wait a minute and refresh to see the complete count.

If the count still doesn't match after the import finishes, the **preview count** (e.g., "Showing 50 of ~39,869 results") is an approximate figure — the `~` tilde prefix in the UI indicates the total is estimated using a fast approximate count, not an exact query. The actual import can return a slightly different total, and this is normal.

Also check your **Limit results** setting: the import won't exceed whatever limit you've configured (default 10,000).

### My search preview shows more than 10,000 results — how do I import all of them?

Find Companies caps imports at 10,000 results per search. When your filters match more than 10,000 companies, the import stops at that limit — there is no way to raise it within a single search.

To capture the full universe, split your search into smaller segments so each import stays under the cap. Use any filter dimension to divide the space:

-   **By location** — Run separate searches for each region, country, or group of states.
-   **By industry** — Run one search per industry category or group of categories.
-   **By company size** — Split across size bands (for example, 1–50 employees, 51–200 employees, and so on).

Each segmented search imports into its own table.

### What does the Estimated employee count filter measure?

The **Estimated employee count** filter reflects the number of professional profiles associated with a company. Because this can include profiles from people who are no longer current employees — as well as anyone who has listed the company in their profile — the count may run higher than the company's actual active headcount.

Use it as a directional signal for company size rather than a precise figure. For a second data point, compare with **Company size** (the self-reported size band the company has set on its own profile), which measures something different — see [Why do Company sizes and Estimated employee count return different results for the same range?](#why-do-company-sizes-and-estimated-employee-count-return-different-results-for-the-same-range).

### Why do Company sizes and Estimated employee count return different results for the same range?

These two filters measure different things:

-   **Company sizes** is a dropdown that selects categorical size bands — 11–50, 51–200, 201–500, etc. — reflecting the size range a company has reported on its profile.
-   **Estimated employee count** is a numeric min/max filter based on a separately computed count of estimated employees derived from profile data.

Because the two values are sourced independently, a company whose reported size band is "51–200" may have a computed employee count of 250 — or vice versa. Filtering on one versus the other can return a different set of companies even when the numbers appear to overlap.

### Re-running Find Companies shows far fewer results than my original run

This is expected behavior. The Find Companies source deduplicates new results against rows already in your table — re-running returns only the net-new companies not yet present in the table.

**Example:** If your table already has 29,000 companies from a previous import, re-running with the same filters returns only the companies genuinely new since the last run — for example, 32 new companies. The existing 29,000 remain in your table; they are not replaced or removed.

Deduplication is based on each company's unique profile ID, not your filter configuration. A company already in the table is skipped on re-run regardless of whether your filters changed.

**To re-import the full result set** (for example, when testing): delete the existing rows from your table first, then re-run the source. Once the rows are cleared, the search re-imports all matching companies from scratch.

### What are the available AI Subindustry filter values?

The **Industries** filter (the standard one at the top of the filter panel) and the **`Industry` output column** use a standardized industry taxonomy drawn from company profile data. Clay recognizes approximately 457 common values (examples: *Software Development, Financial Services, Insurance, Healthcare and Life Sciences, Information Technology and Services, Marketing and Advertising, Non-profit Organization Management*). Because these come from what companies set on their professional profiles, the list is open-ended rather than a fixed picklist.

The **AI Subindustries filter** (under **AI filters**) is different. Clay generates a subindustry classification for each company using its own AI model, and this uses a fixed taxonomy of **110 categories**. These are the only values the filter accepts.

The full set, grouped by parent category:

-   **Software and IT:** AI and ML Platforms, Agriculture and Forestry Software, Blockchain and Web3, Carriers and ISPs, Cloud and Infrastructure Software, Consumer Software, Data and Analytics Software, Developer Tools and Platforms, Enterprise Software Solutions, Financial Services Software, Government and Public Sector Software, Hardware and Networking, Healthcare Software, IoT and Embedded Systems Software, IT Services and Cybersecurity, Manufacturing Software, Metaverse, AR/VR and Other Emerging Platforms, Quantum Computing Software, Real Estate and PropTech Software, Retail and Ecommerce Software, Security and Identity Software

-   **Healthcare and Life Sciences:** Biotechnology and Pharmaceuticals, Digital Health and Telemedicine, Hospitals, Clinics and Outpatient Care, Medical Devices and Diagnostic Equipment, Medical Testing and Clinical Laboratories, Mental Health and Rehabilitation Services, Pharma Distribution and CRO Services

-   **Finance and Insurance:** Banking and Lending, Capital Markets and Cryptocurrency, Cryptocurrency and Blockchain Services, Financial Services Platforms, Insurance and InsurTech, Investment Management and WealthTech, Venture Capital and Private Equity

-   **Energy, Utilities and Environmental Services:** Electric Power and Grid Management, Nuclear and Advanced Generation, Oil and Gas Exploration, Production and Services, Renewable Energy and Clean Tech, Sustainability Tech and Environmental Consulting, Water, Waste and Environmental Management

-   **Industrial Manufacturing and Materials:** 3D Printing and Advanced Manufacturing, Building Materials and Chemicals, Consumer Goods and Appliances, Electronics and Computer Equipment, Food, Beverage and Tobacco Production, Industrial Machinery and Equipment, Mining, Metals and Natural Resources

-   **Real Estate and Construction:** Architecture, Urban Planning and Green Building, Commercial Real Estate Development and Leasing, Construction and Civil Engineering Services, Property and Facility Management, Residential Real Estate Development and Brokerage, Specialty Construction Products

-   **Retail and Consumer Channels:** Automotive Service and Collision Repair, Brick-and-Mortar Retail, Media and Entertainment Retail, Online Commerce and Marketplaces, Retail Technology, Specialty Auctions and Collectibles, Wholesale and Distribution

-   **Transportation and Logistics:** Autonomous Vehicles and Drone Delivery, Car and Truck Rental, Freight and Cargo, Logistics Technology, Passenger Transit and Mobility, Warehousing, Fulfillment and 3PL Services

-   **Professional, Business and Legal Services:** Accounting, Audit and Financial Advisory, Advertising, Marketing and Multimedia Design, Defense and Government Services, Facilities Management and Commercial Cleaning, Human Resources, Staffing and Recruitment, Legal Services and Regulatory Compliance, Management Consulting and Strategy Consulting, Translation, Document and Information Management

-   **Education and Training:** Corporate Training and Learning and Development, E-Learning Platforms and EdTech, K-12 and Higher Education Institutions, Test Prep, Tutoring and After-School Services, Vocational Training and Certification Programs

-   **Media, Entertainment and Culture:** Digital Publishing and Streaming Platforms, Film, Television and Broadcasting, Gaming, Esports and Interactive Entertainment, Live Events, Experiences and Ticketed Attractions, Museums, Art Galleries and Cultural Preservation, Music, Audio and Podcast Services, Sports and Recreation

-   **Hospitality, Food and Travel Services:** Food and Beverage Services, Hospitality and Lodging, Travel Agencies and Leisure Services

-   **Personal and Home Services:** Funeral Homes and Related Services, Home Services, Personal Care and Wellness, Veterinary Care and Pet Services

-   **Agriculture, Forestry and Fisheries:** AgriTech and Precision Farming, Aquaculture and Fisheries, Crop Farming and Livestock Production, Farming Equipment and Supplies, Forestry, Logging and Wood Products, Mining and Extraction

-   **Automotive, Aerospace and Defense Manufacturing:** Aviation and Aerospace Component Manufacturing, Automotive and Rental Retail, Commercial Space Innovation, Defense Systems and Marine Manufacturing, Motor Vehicle and Parts Manufacturing

-   **Non-Profit, Public Sector and Education (Non-Commercial):** Government Administration and Municipal Services, NGOs, Charities and Community Organizations, Public Healthcare and Social Services, Public/Private Research Institutions and Educational Foundations, Student Organizations and Campus Services

**Note:** AI Subindustries is a filter input, not an output column. It controls which companies are returned in Find Companies, but does not add a dedicated Subindustry column to your table.
