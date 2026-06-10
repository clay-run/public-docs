---
title: Find Companies in Clay
source_url: https://university.clay.com/docs/find-companies
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
    -   **Industries** to include and exclude — drawn from **LinkedIn's industry taxonomy** (the categories companies self-report on their LinkedIn profiles). The dropdown lists all available options (~450 in total); scroll or type to search within it. For a complete reference list, see [What industries are available in the "Industries to include" filter?](#what-industries-are-available-in-the-industries-to-include-filter) in the FAQ below.
    -   **Company size** — The self-reported size band on the company's profile (e.g., 11–50, 51–200). Select one or more bands from the dropdown.
    -   **Annual revenue ranges** — Filter by revenue brackets from $0–$500K up to $100B+.
    -   **Funding amount**
    -   **Company types** — Privately Held, Public Company, Partnership, Self Employed, Non Profit, Educational, Self Owned, or Government Agency.
    -   **Keywords** to include or exclude
        -   **Exact phrase matching:** Wrap multi-word terms in single or double quotes to search for that exact phrase. For example, searching for "Google Cloud" finds companies with "Google Cloud" in their description — not just companies that mention Google and cloud separately. Note: Special characters (#, +, !) and stopwords ('a', 'an', 'of', 'the') are stripped out even with quoted phrases.
    -   **Semantic company description** — Enter a free-text description to help rank results based on how closely they match your ideal company profile (e.g., "B2B fintech company selling to mid-market banks").
    -   **Location** — Filter by country, and separately by city or state. Both support include and exclude.
    -   **Estimated employee count** — Filter by a numeric count of estimated employees (enter a minimum and/or maximum). This is a separate field from **Company size** — see the [FAQ below](#why-do-company-sizes-and-estimated-employee-count-return-different-results-for-the-same-range) for why the same numeric range can surface different companies.
    -   **AI filters** — Clay-generated attributes applied to company profiles:
        -   **Industries** and **Subindustries** (include or exclude) — uses Clay's own AI-generated taxonomy, separate from the LinkedIn-based **Industries** filter above. Provides broader normalized groupings like "Software and IT" or "Healthcare and Life Sciences".
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
    -   **Exclude companies:** Exclude up to 3 different sets of companies from your search using Clay tables, CSVs, or manual lists. You can exclude up to 300,000 companies total (100,000 per source). Exclusions require a domain or LinkedIn URL.
    -   **Limit results** — Defaults to 10,000. Maximum 10,000.
2.  Click `Preview companies` and `Import to new table` when the results look good.
3.  Select import options:
    -   Add additional enrichments like `Company Headcount Growth` or `Most Recent News`.
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

### Does importing from Find Companies cost credits?

**No, unless you use technographics filters.** Importing companies using standard filters — industry, size, location, revenue, company type, AI filters — consumes no Actions and no Data Credits.

If you enable **technographics filters**, each company row that matches your criteria costs **3 Data Credits**.

Any enrichments you add to the table afterward (e.g., finding emails, enriching headcount) consume their own Actions and Data Credits as usual — only the import itself is free.

### Why does my table show fewer rows than the preview count?

**The import may still be in progress.** Find Companies imports process asynchronously — rows are added in batches. If you check right after clicking Import, the row count will be lower than the final total. Wait a minute and refresh to see the complete count.

If the count still doesn't match after the import finishes, the **preview count** (e.g., "Showing 50 of ~39,869 results") is an approximate figure — the `~` tilde prefix in the UI indicates the total is estimated using a fast approximate count, not an exact query. The actual import can return a slightly different total, and this is normal.

Also check your **Limit results** setting: the import won't exceed whatever limit you've configured (default 10,000).

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

### What industries are available in the "Industries to include" filter?

The **Industries to include** filter (under **Company Attributes**) uses **LinkedIn's industry taxonomy** — the same industry values that companies self-select on their LinkedIn profiles. Clay's dataset includes approximately 450 industry options, limited to industries with at least 100 companies represented in Clay's database.

To browse the full list interactively, open the **Find Companies** source and expand the **Industries to include** dropdown. You can type to search within it.

**Note:** The **Industries** and **Subindustries** filters under **AI filters** use a separate, Clay-generated taxonomy — not LinkedIn's. Those are distinct classification systems used for broader, AI-normalized groupings.

The complete list of available LinkedIn-taxonomy industries is:

- Abrasives and Nonmetallic Minerals Manufacturing
- Accessible Architecture and Design
- Accommodation Services
- Accounting
- Administration of Justice
- Administrative and Support Services
- Advertising Services
- Agricultural Chemical Manufacturing
- Agriculture, Construction, Mining Machinery Manufacturing
- Air, Water, and Waste Program Management
- Airlines and Aviation
- Alternative Dispute Resolution
- Alternative Medicine
- Ambulance Services
- Amusement Parks and Arcades
- Animal Feed Manufacturing
- Animation
- Animation and Post-production
- Apparel Manufacturing
- Apparel and Fashion
- Appliances, Electrical, and Electronics Manufacturing
- Architectural and Structural Metal Manufacturing
- Architecture and Planning
- Armed Forces
- Artists and Writers
- Arts and Crafts
- Audio and Video Equipment Manufacturing
- Automation Machinery Manufacturing
- Automotive
- Aviation & Aerospace
- Aviation and Aerospace Component Manufacturing
- Baked Goods Manufacturing
- Banking
- Bars, Taverns, and Nightclubs
- Bed-and-Breakfasts, Hostels, Homestays
- Beverage Manufacturing
- Biomass Electric Power Generation
- Biotechnology
- Biotechnology Research
- Blockchain Services
- Blogs
- Boilers, Tanks, and Shipping Container Manufacturing
- Book Publishing
- Book and Periodical Publishing
- Breweries
- Broadcast Media Production and Distribution
- Building Construction
- Building Equipment Contractors
- Building Finishing Contractors
- Building Materials
- Building Structure and Exterior Contractors
- Business Consulting and Services
- Business Content
- Business Intelligence Platforms
- Business Supplies and Equipment
- Capital Markets
- Caterers
- Chemical Manufacturing
- Chemical Raw Materials Manufacturing
- Child Day Care Services
- Chiropractors
- Civic and Social Organizations
- Civil Engineering
- Claims Adjusting, Actuarial Services
- Clay and Refractory Products Manufacturing
- Climate Data and Analytics
- Climate Technology Product Manufacturing
- Coal Mining
- Collection Agencies
- Commercial Real Estate
- Commercial and Industrial Equipment Rental
- Commercial and Industrial Machinery Maintenance
- Commercial and Service Industry Machinery Manufacturing
- Communications Equipment Manufacturing
- Community Development and Urban Planning
- Community Services
- Computer Games
- Computer Hardware
- Computer Hardware Manufacturing
- Computer Networking
- Computer Networking Products
- Computer and Network Security
- Computers and Electronics Manufacturing
- Conservation Programs
- Construction
- Construction Hardware Manufacturing
- Consumer Electronics
- Consumer Goods
- Consumer Goods Rental
- Consumer Services
- Cosmetics
- Cosmetology and Barber Schools
- Courts of Law
- Credit Intermediation
- Dairy
- Dairy Product Manufacturing
- Dance Companies
- Data Infrastructure and Analytics
- Data Security Software Products
- Defense & Space
- Defense and Space Manufacturing
- Dentists
- Design
- Design Services
- Desktop Computing Software Products
- Digital Accessibility Services
- Distilleries
- E-Learning
- E-Learning Providers
- Economic Programs
- Education
- Education Administration Programs
- Education Management
- Electric Lighting Equipment Manufacturing
- Electric Power Generation
- Electric Power Transmission, Control, and Distribution
- Electrical Equipment Manufacturing
- Electronic and Precision Equipment Maintenance
- Embedded Software Products
- Emergency and Relief Services
- Engineering Services
- Engines and Power Transmission Equipment Manufacturing
- Entertainment
- Entertainment Providers
- Environmental Quality Programs
- Environmental Services
- Equipment Rental Services
- Events Services
- Executive Offices
- Executive Search Services
- Fabricated Metal Products
- Facilities Services
- Farming, Ranching, Forestry
- Farming
- Fashion Accessories Manufacturing
- Financial Services
- Fine Art
- Fine Arts Schools
- Fire Protection
- Fisheries
- Flight Training
- Food & Beverages
- Food and Beverage Manufacturing
- Food and Beverage Retail
- Food and Beverage Services
- Food Production
- Footwear Manufacturing
- Forestry and Logging
- Freight and Package Transportation
- Fruit and Vegetable Preserves Manufacturing
- Fundraising
- Funds and Trusts
- Furniture
- Furniture and Home Furnishings Manufacturing
- Gambling Facilities and Casinos
- Geothermal Electric Power Generation
- Glass Product Manufacturing
- Glass, Ceramics and Concrete Manufacturing
- Golf Courses and Country Clubs
- Government Administration
- Government Relations
- Government Relations Services
- Graphic Design
- Ground Passenger Transportation
- HVAC and Refrigeration Equipment Manufacturing
- Health and Human Services
- Health, Wellness and Fitness
- Higher Education
- Highway, Street, and Bridge Construction
- Historical Sites
- Holding Companies
- Home Health Care Services
- Horticulture
- Hospitality
- Hospitals
- Hospitals and Health Care
- Hotels and Motels
- Household Appliance Manufacturing
- Household Services
- Household and Institutional Furniture Manufacturing
- Housing Programs
- Housing and Community Development
- Human Resources
- Human Resources Services
- Hydroelectric Power Generation
- IT Services and IT Consulting
- IT System Custom Software Development
- IT System Data Services
- IT System Design Services
- IT System Installation and Disposal
- IT System Operations and Maintenance
- IT System Testing and Evaluation
- IT System Training and Support
- Import and Export
- Individual and Family Services
- Industrial Automation
- Industrial Machinery Manufacturing
- Industry Associations
- Information Services
- Information Technology and Services
- Insurance
- Insurance Agencies and Brokerages
- Insurance Carriers
- Insurance and Employee Benefit Funds
- Interior Design
- International Affairs
- International Trade and Development
- Internet Marketplace Platforms
- Internet News
- Internet Publishing
- Investment Advice
- Investment Banking
- Investment Management
- Janitorial Services
- Landscaping Services
- Language Schools
- Laundry and Drycleaning Services
- Law Enforcement
- Law Practice
- Leasing Non-residential Real Estate
- Leasing Residential Real Estate
- Leather Product Manufacturing
- Legal Services
- Legislative Offices
- Leisure, Travel & Tourism
- Libraries
- Loan Brokers
- Luxury Goods and Jewelry
- Machinery Manufacturing
- Manufacturing
- Maritime
- Maritime Transportation
- Market Research
- Marketing Services
- Mattress and Blinds Manufacturing
- Measuring and Control Instrument Manufacturing
- Meat Products Manufacturing
- Mechanical or Industrial Engineering
- Media & Telecommunications
- Media Production
- Medical Devices
- Medical Equipment Manufacturing
- Medical Practices
- Medical and Diagnostic Laboratories
- Mental Health Care
- Metal Ore Mining
- Metal Treatments
- Metal Valve, Ball, and Roller Manufacturing
- Metalworking Machinery Manufacturing
- Military and International Affairs
- Mining
- Mobile Computing Software Products
- Mobile Food Services
- Mobile Gaming Apps
- Motor Vehicle Manufacturing
- Motor Vehicle Parts Manufacturing
- Movies and Sound Recording
- Movies, Videos and Sound
- Museums
- Museums, Historical Sites, and Zoos
- Music
- Musicians
- Nanotechnology Research
- Natural Gas Distribution
- Newspaper Publishing
- Non-profit Organization Management
- Non-profit Organizations
- Nonmetallic Mineral Mining
- Nonresidential Building Construction
- Nuclear Electric Power Generation
- Nursing Homes and Residential Care Facilities
- Office Administration
- Office Furniture and Fixtures Manufacturing
- Oil and Gas
- Oil, Gas, and Mining
- Online Audio and Video Media
- Online Media
- Online and Mail Order Retail
- Operations Consulting
- Optometrists
- Outpatient Care Centers
- Outsourcing and Offshoring Consulting
- Outsourcing/Offshoring
- Packaging and Containers
- Packaging and Containers Manufacturing
- Paint, Coating, and Adhesive Manufacturing
- Paper and Forest Product Manufacturing
- Paper and Forest Products
- Performing Arts
- Performing Arts and Spectator Sports
- Periodical Publishing
- Personal Care Product Manufacturing
- Personal Care Services
- Personal and Laundry Services
- Pet Services
- Pharmaceutical Manufacturing
- Philanthropic Fundraising Services
- Philanthropy
- Photography
- Physical, Occupational and Speech Therapists
- Physicians
- Plastics Manufacturing
- Plastics and Rubber Product Manufacturing
- Political Organizations
- Primary Metal Manufacturing
- Primary and Secondary Education
- Printing Services
- Professional Organizations
- Professional Services
- Professional Training and Coaching
- Program Development
- Public Assistance Programs
- Public Health
- Public Policy
- Public Policy Offices
- Public Relations and Communications Services
- Public Safety
- Radio and Television Broadcasting
- Rail Transportation
- Railroad Equipment Manufacturing
- Ranching
- Real Estate
- Real Estate Agents and Brokers
- Real Estate and Equipment Rental Services
- Recreational Facilities
- Religious Institutions
- Renewable Energy Equipment Manufacturing
- Renewable Energy Power Generation
- Renewable Energy Semiconductor Manufacturing
- Renewables & Environment
- Repair and Maintenance
- Research
- Research Services
- Residential Building Construction
- Restaurants
- Retail
- Retail Apparel and Fashion
- Retail Appliances, Electrical, and Electronic Equipment
- Retail Art Dealers
- Retail Art Supplies
- Retail Books and Printed News
- Retail Building Materials and Garden Equipment
- Retail Florists
- Retail Furniture and Home Furnishings
- Retail Gasoline
- Retail Groceries
- Retail Health and Personal Care Products
- Retail Luxury Goods and Jewelry
- Retail Motor Vehicles
- Retail Musical Instruments
- Retail Office Equipment
- Retail Office Supplies and Gifts
- Retail Pharmacies
- Retail Recyclable Materials & Used Merchandise
- Reupholstery and Furniture Repair
- Robotics Engineering
- Rubber Products Manufacturing
- Satellite Telecommunications
- School and Employee Bus Services
- Seafood Product Manufacturing
- Securities and Commodity Exchanges
- Security Guards and Patrol Services
- Security Systems Services
- Security and Investigations
- Semiconductor Manufacturing
- Semiconductors
- Services for Renewable Energy
- Services for the Elderly and Disabled
- Sheet Music Publishing
- Shipbuilding
- Shuttles and Special Needs Transportation Services
- Sightseeing Transportation
- Soap and Cleaning Product Manufacturing
- Social Networking Platforms
- Software Development
- Solar Electric Power Generation
- Sound Recording
- Space Research and Technology
- Specialty Trade Contractors
- Spectator Sports
- Sporting Goods
- Sporting Goods Manufacturing
- Sports Teams and Clubs
- Sports and Recreation Instruction
- Spring and Wire Product Manufacturing
- Staffing and Recruiting
- Steam and Air-Conditioning Supply
- Strategic Management Services
- Subdivision of Land
- Sugar and Confectionery Product Manufacturing
- Surveying and Mapping Services
- Taxi and Limousine Services
- Technical and Vocational Training
- Technology, Information and Internet
- Technology, Information and Media
- Telecommunications
- Telecommunications Carriers
- Telephone Call Centers
- Temporary Help Services
- Textile Manufacturing
- Theater Companies
- Think Tanks
- Tobacco
- Tobacco Manufacturing
- Translation and Localization
- Transportation Equipment Manufacturing
- Transportation Programs
- Transportation, Logistics, Supply Chain and Storage
- Transportation/Trucking/Railroad
- Travel Arrangements
- Truck Transportation
- Trusts and Estates
- Turned Products and Fastener Manufacturing
- Urban Transit Services
- Utilities
- Utilities Administration
- Utility System Construction
- Vehicle Repair and Maintenance
- Venture Capital and Private Equity Principals
- Veterinary
- Veterinary Services
- Vocational Rehabilitation Services
- Warehousing
- Warehousing and Storage
- Waste Collection
- Waste Treatment and Disposal
- Water Supply and Irrigation Systems
- Water, Waste, Steam, and Air Conditioning Services
- Wellness and Fitness Services
- Wholesale
- Wholesale Alcoholic Beverages
- Wholesale Apparel and Sewing Supplies
- Wholesale Appliances, Electrical, and Electronics
- Wholesale Building Materials
- Wholesale Chemical and Allied Products
- Wholesale Computer Equipment
- Wholesale Drugs and Sundries
- Wholesale Food and Beverage
- Wholesale Footwear
- Wholesale Furniture and Home Furnishings
- Wholesale Hardware, Plumbing, Heating Equipment
- Wholesale Import and Export
- Wholesale Luxury Goods and Jewelry
- Wholesale Machinery
- Wholesale Metals and Minerals
- Wholesale Motor Vehicles and Parts
- Wholesale Paper Products
- Wholesale Petroleum and Petroleum Products
- Wholesale Raw Farm Products
- Wholesale Recyclable Materials
- Wind Electric Power Generation
- Wine and Spirits
- Wineries
- Wireless Services
- Wood Product Manufacturing
- Writing and Editing
- Zoos and Botanical Gardens
