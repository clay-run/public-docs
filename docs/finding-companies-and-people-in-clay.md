---
title: "Guide: Finding companies and people in Clay"
description: Best practices to Clay's company and people search features, including valid LinkedIn URL formats for the company identifier and troubleshooting common errors.
last_synced: 2026-04-26T01:39:59.452Z
---

# Guide: Finding companies and people in Clay

Best practices to Clay's company and people search features.

Clay's `Find Companies` and `Find People` sources give you instant access to billions of company and people profiles — all in one place. Here are the best practices we recommend to streamline your searches and surface the strongest results.

> **Note:** Find People at These Companies is currently in **Beta** — a Beta badge is shown on the panel header in the product UI.

## Company search

### Anchor on description keywords

Industry categories map to the categories companies self-select on LinkedIn — which can be too broad for most use cases. **Description keywords** let you narrow by what a company actually does, not just how it's categorized. Use them heavily as your primary filter, and layer industry categories on top only when needed.

### Use AI filters to avoid paying for data you won't use

A common TAM sourcing mistake is pulling a large list and then running enrichments afterward to qualify it — which means paying credits for companies you'll ultimately discard. **AI filters** (sub-industries, revenue streams, business types, and other derived attributes) let you filter out noise before any rows are returned, so you only pay for companies you actually want.

**Note:** Technographics filtering is also available directly in company search and costs 3 credits per company returned — cheaper in most cases than running a technographic enrichment after the fact, and more direct since you only pay for companies that already match your tech criteria. Technographics data is also available when sending company rows to Audiences; the same credit cost applies.

### Filter by location with structured fields

The **Location** filter in company search supports structured sub-filters — **Country**, **City**, **State or province**, **Region**, and **Postal code** — each with include and exclude modes. These fields match against geocoded, normalized location data, so you get accurate results rather than relying on free-text string matching.

Enable **Headquarters only** to restrict results to companies whose *primary* office is in the specified location. Without it, any matching office — branch, satellite, or headquarters — qualifies a company for inclusion.

For the full filter spec and a list of the structured location fields returned in each result's cell details, see [Find Companies](find-companies.md).

### Understand how filters combine

Company search uses AND logic across filter types and OR logic within a single filter:

-   **Across filters** — every filter you apply must match. If you set industry + company size + revenue, a company must meet all three criteria.
-   **Within a filter** — any value can match. If you select two industries, a company matching either one is returned.

If you need results that meet _either_ of two different filter combinations, set up two separate searches.

## People search

### Choose your starting point

**If you have a company list**, you have two options depending on how you want to store the results:

-   **Find People at These Companies** — sends the matched contacts to an **Audiences draft segment** (one contact per match, linked back to the company). **To access:** In your company table, click **Tools** (top right) → **Import** tab → **Find People at These Companies**. The setup panel includes full filters for job title, seniority, location, experience, and more — set your criteria, preview the results, then click **Continue** to send the contacts to an Audiences draft. To cap results to a specific number per company (for example, 5 contacts per company), use the **Number of people per company** field in the setup panel before clicking Continue. On large company lists, the in-table **Find People at These Companies** enrichment action gives you the most predictable per-company control, since it processes each company row individually.
-   **Find Contacts at Company** (add as a column in your company table) — stores contacts as a list within each company row. Best when you want contacts to stay in your company table, or when you're adding companies one at a time and don't want a single search to re-run across all rows. Use **Send Table Data** afterward to push individual contacts to another table if needed.

    **Note:** Formula columns you add to your company table (for example, a "Contact Title" or "Contact Profile URL" column) extract data for **one contact per row** — they reference a single indexed position in the list, such as the first person found. To get every found contact as its own row — each with their own name, title, and profile URL — use **Send Table Data** with **Send row for each item in a list**. The quickest way is to click a populated result cell and select **Take action on list → Write each item to new row in other table**. See [Send table data](send-table-data.md) for full setup details.

If you don't have a company list, use **People search as a source** — a standalone search by title or other criteria that returns a new table.

**If you're receiving data row-by-row via webhook** — for example, one row per incoming job opening — and need to find people automatically for each row, include a company identifier (company name, domain, or company profile URL) in each webhook payload. With a company identifier in the row, add **Find Contacts at Company** as an enrichment column in your webhook table. This action runs independently per row, finds contacts at that specific company filtered by job title, and stores results in the cell. To route those contacts into individual rows, add a **Send Table Data** column (using **Send row for each item in a list**) to push each contact to a separate people table where you can apply enrichments and AI scoring.

**Note:** The standalone **Find People source** does not run per row — it imports results at creation time and is not retriggered by new incoming webhook rows. For automated per-row people searches triggered by incoming data, use **Find Contacts at Company** (enrichment column) instead.

### Enriching your results

**Find People at These Companies** returns basic profile data for each contact: name, title, current company, LinkedIn URL, and location. **Work emails and phone numbers are not included** — add them as separate enrichments after your people table is created:

**Work email:** In your people table, click `Add enrichment` and select `Work Email`. This pre-built waterfall searches multiple email providers in sequence and requires the person's name and company domain. For full setup details, see [Work Email waterfall](work-email-waterfall.md).

**Mobile phone:** In your people table, click `Add enrichment`, search for `Phone number`, and select the waterfall option under **Waterfalls**. The phone waterfall cascades through multiple providers — providers that return no result are skipped at no credit cost. It requires the person's LinkedIn URL, which is included in the people table from the search. For provider recommendations by region, see [[Data test] Mobile phone providers by region](data-test-methodology-mobile-phone-region.md).

### Build job title lists instead of relying on the function dropdown

The **Job functions** and **Seniority** dropdowns can be too broad or too exclusionary. Instead, paste a comma-separated keyword list directly into the **Job title keywords** field. Use Claude or ChatGPT to generate an exhaustive list of title variations — for example, every way someone might write "VP of Sales" — and paste it in as a single string.

Always pair this with a **Job title keywords to exclude** list to filter out common false positives before they reach your table.

### Choose the right title match mode

-   **Is similar to** _(recommended default)_ — fuzzy match that finds synonyms and variations. "Chief executive officer" also returns "CEO." May occasionally return irrelevant titles; filter those out with a formula (free) or AI.
-   **Contains** — returns titles that contain your full keyword phrase as a substring. "Chief executive officer" will not match "chief financial officer."
-   **Is exactly** — matches only the precise titles you enter. Use when precision is critical.

### Use LinkedIn URLs, not domains, as company identifiers

When running a people search against a company list, provide a **company or school LinkedIn URL** rather than a domain wherever possible. Clay resolves domains by running them through a company lookup, which can occasionally surface the wrong company — especially for subsidiaries. LinkedIn URLs map directly to the intended profile.

The company identifier field accepts these LinkedIn URL formats:

-   **Company page**: `https://www.linkedin.com/company/<slug>` (e.g., `https://www.linkedin.com/company/clay-run`)
-   **School page**: `https://www.linkedin.com/school/<slug>` (e.g., `https://www.linkedin.com/school/westlake-christian-academy`)

**Important:** Person profile URLs (`https://www.linkedin.com/in/<name>`) are not valid as company identifiers. Passing a person LinkedIn URL produces a confusing "Invalid companies provided" error even though the URL is real and correctly formatted — the field only accepts company or school page URLs, not individual profiles. See the [troubleshooting section](#getting-invalid-companies-provided-error-despite-having-a-valid-linkedin-url) below if you hit this error.

### Run conditional people searches with table views

Company and people search sources don't have run conditions the way enrichment actions do. If you only want to find people at companies that meet specific criteria (e.g., only public companies), the workaround is to **create a filtered view** of your company table first, then run **Find People at These Companies** from that view. The source will only pull from the rows visible in the view.

### Disable auto-run on the people table when running Find People selectively

When Find People is configured as an enrichment action between a company table and a people table, **both tables have independent auto-run settings**. Turning off auto-run in the company table controls whether Find People fires when company rows are added or edited — but it has **no effect** on the people table's own auto-run setting.

If the people table's auto-run is still on, adding new people rows (for example, by manually triggering Find People for a subset of companies) will automatically fire all enrichments in the people table on those new rows. This can trigger runs across all companies in the table — not just the ones you selected — consuming far more credits than expected.

**To prevent this when running Find People on specific companies only:**

1.  Open your **people table** (not the company table).
2.  Click the table name to access table settings.
3.  Under **Run Settings**, toggle **Auto-run** to **OFF**.

With auto-run disabled in both tables, you control exactly which companies trigger people searches and which enrichments run in the people table.

### Source vs. enrichment — when to use each

Clay gives you three ways to get contacts from a company list. Here's how they differ:

**Find People at These Companies — as a source (returns a new table):**

-   Returns all results in a separate people table with one row per contact.
-   When re-run, searches across all companies in the linked table — including any newly added ones. New people are appended and deduplicated against rows already in the table.
-   Subject to a per-source cumulative limit that varies by billing plan — once that limit is hit, the source stops returning new records even if new companies are added. See [the troubleshooting section](#your-source-has-exceeded-your-plans-limit-error-on-find-companies-or-find-people) for details.
-   Best when you don't need to rank or further filter contacts before saving them.
-   **Update People Table column:** When this source is created from a company table, Clay automatically adds an **Update People Table** column to the company table. That column is the link between the two tables — when it runs, it triggers a full re-run of the Find People search across all companies currently in the table, including any newly added ones. It does not run incrementally for only new rows; it re-runs the full search. With **Enable Automatic People Search Updates** toggled on, the column fires automatically when new company rows enter the table; turn it off to trigger refreshes manually.

**Find People at These Companies — as an enrichment action (saves to existing table):**

-   Returns 10 people per row by default, with full profile data.
-   `Reduce data for more results` mode returns up to 500 people per row, but only name, job title, and professional profile URL — you'll need to run `Enrich Person` afterward to get full profiles.
-   Best when you need to rank contacts first or run a more targeted search per company.

**Find Contacts at Company — as a column enrichment (list stored in cell):**

-   Add as a column directly in your company table. Each row independently runs a people search and stores the matching contacts as a list within the cell.
-   Unlike Find People at These Companies, results are not written as rows to a separate people table — they stay in your company table as cell data. To turn each contact into its own row in another table, use **Send Table Data** with **Send row for each item in a list**. Quickest setup: click a populated result cell, hover over the **People** section in the cell details panel, and click **Take action on list** → **Write each item to new row in other table**. Note that this method sends up to 20 contacts per run — see [Send table data](send-table-data.md) for full details.
-   Returns **10 contacts per row by default**, with full profile data.
-   `Reduce data for more results` mode returns up to **500 contacts per row**, but only name, job title, and professional profile URL — run `Enrich Person` on each row afterward to get full profiles.
-   Processes each company row independently — adding a new company row does not re-trigger the enrichment on other rows.
-   Costs **0.5 credits per row** on current pricing plans (1 credit per row on legacy plans).
-   Best when you want contacts to stay associated with their parent company row, or when you're processing companies incrementally and only want to find contacts for specific rows.

### Check headcounts before running a full people search

Use **Find Employee Headcount by Criteria** as an enrichment column in your company table to get a contact count matching your criteria before committing to a full people search. It takes the same filters as people search — job title keywords, seniority levels, location, and more — but returns only a `Role Count` number per company row rather than pulling full profiles. Add it as a column in your company table and pass a company profile URL or domain as the company identifier. Once the counts are populated, filter your table for companies above (or below) your threshold before running `Find Contacts at Company` or `Find People at These Companies` — this avoids spending credits on companies with too few matching contacts.

### Use dynamic location filtering with in-table actions

When you run `Find People at These Companies` as an in-table action (rather than launching a separate people search), you can dynamically filter by location by referencing a location column from your company table. This lets you customize the location filter per company without running multiple separate searches.

For example, if you have a "Headquarters Location" column in your company table, you can reference that column in the location filter when setting up the in-table action. Each company will then be searched using its specific location, rather than applying a single static location filter across all companies.

**Note:** Location filtering accepts named regions, countries, and cities — distance-based filtering (for example, "within 35 miles of a location") is not available in Find People or Find Contacts at Company.

### Target ICP contacts first with a senior fallback

When your goal is to reach your ideal customer profile (ICP) at each company — but fall back to the most senior people available if no ICP match is found — run two separate `Find Contacts at Company` enrichment columns in your company table, then use AI to select the best contacts before routing them to a people table.

**High-level flow:**

`Company table → ICP people search → Senior fallback search → AI selects best N → Send to people table → Enrich with email and phone`

**Steps:**

1. **ICP search column** — Add `Find Contacts at Company` as an enrichment column in your company table. Filter **Job title keywords** to your ICP titles (for example, "Head of Ecommerce" or "VP of Marketing"). This column runs for every company row.
2. **Senior fallback column** — Add a second `Find Contacts at Company` column filtered to high **Seniority** levels (C-level, VP, Director). In **Run settings → Only run if**, add a condition so this column only fires when the ICP search returned no contacts — for example, `{{ICP search column}} is empty`. See [Conditional runs](conditional-runs.md).
3. **AI selection column** — Add a `Use AI` column. Reference both result lists (ICP column and fallback column) and prompt the AI to return the best N candidates, prioritising ICP title match and then seniority. For example: *"Review these candidates and return the best 10 contacts, prioritising ICP title match, then seniority level."*
4. **Send to people table** — In the company table, click a populated AI-result cell, then **Take action on list → Write each item to new row in other table** to push selected contacts into a dedicated people table. See [Send table data](send-table-data.md).
5. **Enrich in the people table** — Add **Work Email waterfall** and **Phone waterfall** enrichments to the people table. See [Enriching your results](#enriching-your-results).

**To carry company attributes (employee count, industry, size) into the people table:** Add a `Lookup single row in other table` column in the people table, matching on company domain. This retrieves company enrichment data that does not flow through the automatic Company Table Data link — see [Company Table Data doesn't include company enrichment data](#company-table-data-doesnt-include-company-enrichment-data) for details.

### Verify current employment before using results

People search data reflects snapshot data, which can lag behind real-time LinkedIn changes. After running `Enrich Person`, use this formula to confirm the person is still employed at the expected company:

`{{Enrich person}}?.current_experience?.some(e => (e?.company_domain || "").toLowerCase() === ({{Company Domain}} || "").toLowerCase()) || false   `

This runs as a formula (no credit cost) and returns `true` if a matching current experience is found.

**Note:** This check requires running Enrich Person first. In most workflows you'll be running Enrich Person anyway — the formula adds no additional cost on top of that.

**One Enrich Person call returns the full experience history.** You do not need multiple Enrich Person columns to check multiple experience items. A single call returns the complete experience array, and `current_experience` is a pre-filtered list of every currently-active role. If a contact holds multiple simultaneous positions — for example, a CEO who is also a board member or investor at other companies — every active role appears in `current_experience`, and `.some()` checks across all of them automatically.

**Matching by company name instead of domain.** If you have a company name from a CRM (such as HubSpot) but not a domain, use this formula variant to return a "Yes" / "No" former-employee flag:

`{{Enrich person}}?.current_experience?.some(e => (e?.company || "").toLowerCase().includes(({{Company Name}} || "").toLowerCase())) ? "No" : "Yes"`

This returns `"No"` if any currently-active role's company name includes your CRM company name, and `"Yes"` (former employee) otherwise. You can also pass the full experience array and your company name into a **Use AI** column with a prompt like: *"Given this experience array, return only 'Yes' or 'No'. Return 'No' if any role marked as currently active matches the company name. Otherwise return 'Yes'."*

### Identify the primary role when a contact holds multiple concurrent positions

When someone lists multiple active jobs on LinkedIn — for example, a CEO who is also an Advisor at several companies — Enrich Person surfaces the **top-listed** LinkedIn position as the default `current_job_title` and `current_company`. That may not be the person's primary full-time role.

Clay does not automatically detect which concurrent role is the "main" job. To identify the actual primary role, use a **Use AI** column:

1.  Run `Enrich Person` to pull the full experience data.
2.  Add a **Use AI** column (in **Content creation, manipulation** mode).
3.  Reference `{{Enrich person}}?.current_experience` in the prompt and ask the AI to pick the primary role. For example: *"Given the following work experience, identify this person's primary current job. Deprioritize roles like Advisor, Board Member, or Consultant in favor of full-time positions."*
4.  To get the job title and company in **separate table columns** rather than a single paragraph, define two output fields in the AI column:
    -   `primary_title` (Text) — the person's primary job title
    -   `primary_company` (Text) — the company for that role

Using the **Generate tab** (describe what you want in plain English) is the fastest way to configure this — Clay will set up the prompt and output fields automatically.

### Calculate how long a contact has been in their current role

To find out how long people on an existing list have been in their current positions, run **Enrich person** and combine the returned start date with a **Use AI** column:

1.  In your people table, click **Add enrichment**, search for **Enrich person**, and add the enrichment. Map the **Professional URL** input to your LinkedIn URL column.
2.  Add a **Use AI** column. Reference the current position's start date with `{{Enrich person}}?.current_experience?.[0]?.start_date` and use a prompt like: *"How long ago was [start date] from today? Return as a decimal number of years, rounded to one decimal place."*

The enrichment returns a `start_date` for each active role. The AI column converts that date into a tenure figure you can sort, filter, or use in downstream formulas.

**Note:** If you want to filter contacts at the search stage rather than enriching afterward, use the **Months in current role** filter in **Find People** — it returns only people whose current role duration falls within a range you set. See [Find People in Clay](find-people-overview.md) for details.

### Find people who previously worked at a specific company

The **Companies** filter targets people who **currently** work at the companies you specify. Enabling the main **Include past experiences** toggle alongside a Companies filter extends that filter to past roles too — returning both current and former employees of those companies, which is not useful if you want alumni who are now elsewhere.

To find current employees at your target companies who **also previously worked at a specific company** (for example, Airtable alumni now working at competitor companies), use **Find People at These Companies** as an action column with the dedicated **Exp. Description Incl. Past Experiences** toggle:

1.  From your companies table, add **Find People at These Companies** as an action column.
2.  Under **Experience**, add the former employer's name (e.g., `Airtable`) as an **Experience description keyword**.
3.  Enable the **Exp. Description Incl. Past Experiences** toggle. This applies the keyword match against past experience descriptions specifically, while the Companies filter continues targeting only current employees at your target companies.
4.  Leave the main **Include past experiences** toggle OFF — turning it on would also extend the Companies filter to past roles, pulling in people who formerly worked at your target companies rather than people who are currently there.

This returns people who currently work at your target companies and have the former employer's name in their past experience descriptions.

**Precision caveat:** Keyword matching checks anywhere the name appears in experience descriptions, so it can pick up adjacent mentions — for example, someone who managed an Airtable integration at a vendor but never worked there directly. For higher precision, run `Enrich Person` after pulling results and verify the former employer appears in the structured past experience array.

## Excluding companies and people

You can exclude up to **150,000 companies or people** from any company or people search by adding up to **three exclusion sources**. Each exclusion source can be one of:

-   A Clay table
-   A comma-separated list of URLs (e.g., LinkedIn profile or company page URLs)
-   A CSV file

**Identifiers to use:**

-   For companies: domain or LinkedIn URL
-   For people: LinkedIn URL

This is the current way to suppress your existing CRM or list against new searches. In the future, Audiences will allow you to exclude an entire synced CRM instance (e.g., all of Salesforce) in one step.

**Plan availability:** The exclusion option in source settings is available on Launch plan and above. It is not available on Free or Starter plans.

### Exclusions apply to future source runs — not existing rows

Exclusion sources filter companies from **new imports only** — they do not remove or hide rows that are already in your table. If you add an exclusion list to the source settings of an existing, populated table, the rows that are already there are not affected.

To retroactively hide rows that match your exclusion list without re-running the source (and without losing your enrichment data), use a lookup column combined with a view filter:

1.  **Add a lookup column** — In your table, add a **Lookup single row in other table** action. Set `Table to search` to your exclusion table (e.g., a customers table) and match on **domain** for companies or **LinkedIn URL** for people.
2.  **Filter your view** — Add a view filter that shows only rows where the lookup returned no match (the lookup column is empty). Your enrichment data stays intact and the matched rows are hidden from the view without being deleted.
3.  **Keep the exclusion in source settings** — This prevents future source runs from re-importing those same companies.

This is the approach to use when you've already run enrichments and don't want to re-run the entire source just to apply exclusions retroactively.

### Excluding records during enrichment

The exclusion options above remove matched records before they enter your table. If records are already in your table and you want to skip enrichment on contacts that match a suppression list — such as existing customers, competitors, or a broker list — use **Lookup Rows combined with a run condition**:

1.  Import your suppression list as a Clay table (or use an existing one in your workspace).
2.  In your enrichment table, add a **Lookup single row in other table** action. Set `Table to search` to your suppression table and match on a stable identifier — LinkedIn URL for people, or domain for companies.
3.  On each enrichment you want to gate, open **Run settings → Only run if** and add a condition such as `{{Suppression Lookup}} is empty`. The enrichment will only run for records not found in your suppression list.

This pattern is especially useful when your suppression list changes over time (update the lookup table and the condition reflects the new list automatically), when you're pulling contacts from multiple sources and want a single suppression layer, or when you need to exclude records discovered after the initial search.

### Excluding people at specific companies (e.g., current customers)

The **Exclude People** filter in a Find People source only removes specific individuals by their professional profile URL — it does not accept a list of companies. To filter out everyone who works at your current customers, competitors, or other off-limits organizations, use one of two approaches.

**Option 1 — Start with Find Companies and exclude customer companies upfront**

If you haven't built your people table yet (or are willing to re-run the source from scratch), the cleanest approach is a two-step workflow:

1.  Create a **Find Companies** table with your target criteria.
2.  In the source configuration, expand **Exclude companies** and add your customers table, a CSV of customer domains, or a comma-separated list of domains.
3.  From the resulting company table, click **Tools** → **Find People at These Companies**. People at excluded companies will not appear in the people table.

**Option 2 — Filter an existing people table by the company the person works at**

If you already have a populated Find People table and want to suppress contacts from customer companies without re-running the source:

1.  Make sure your customers exist in a Clay table with at least a company domain column.
2.  In your people table, add a **Lookup single row in other table** column. Set `Table to search` to your customers table, `Target column` to the customer domain column, and `Row value` to the person's current company domain.
3.  Add a **view filter** showing only rows where the lookup returned no match (the lookup column is empty). Contacts at customer companies are hidden from view without being deleted — your enrichment data is preserved.

## Limitations

**Geographic coverage**

**United States:** Highest data quality and coverage.

**International (EMEA/APAC):**

-   Expect 15–25% lower coverage than US
-   Phone numbers especially may have limited availability
-   Europe/DACH regions may require adjusted expectations

**Company segments with lower data quality**

-   SMB businesses (especially those with limited social profiles)
-   Agencies
-   Companies with minimal online presence

**For local businesses with little online professional presence** — such as small service businesses in a specific city or area — use the **Find local businesses using Google Maps** source instead of Find Companies. After importing, add the **Work Email waterfall** enrichment to find contact emails. See [Work Email waterfall](work-email-waterfall.md) for setup details. To qualify the imported list further — for example, filtering out businesses below a revenue threshold or employee count minimum — add revenue and employee count enrichment columns after importing (Google Maps results don't include these data points natively), then apply table filters to show only rows that meet your criteria.

## Troubleshooting

### Find People returns fewer results than expected

Clay uses stored snapshot data rather than live LinkedIn search, so results will never be a perfect mirror of what LinkedIn shows on a company's people page. Common causes:

-   **Private or restricted profiles** — Clay can only surface profiles that are accessible in the stored dataset. Profiles set to private on LinkedIn are excluded.
-   **Domain-to-company mapping issues** — when you provide a domain instead of a LinkedIn URL, Clay resolves it through a company lookup that can occasionally return the wrong entity, especially for subsidiaries, rebranded companies, or companies with stale LinkedIn slugs. Switch to the **LinkedIn company URL** as your input to bypass this lookup entirely.
-   **Filters set too narrowly** — title, location, or seniority filters that are too specific can exclude real matches. Try broadening one filter at a time to diagnose where results drop off.

If profiles still appear to be missing after switching to LinkedIn URLs, use **Claygent** to find the missing profiles via Google search, then pass those LinkedIn URLs directly into `Enrich Person`. This uses a live-scraping fallback that isn't constrained by the stored dataset.

### Re-running Find Companies shows far fewer results than my original run

This is expected behavior. The Find Companies source deduplicates new results against rows already in your table — re-running returns only the net-new companies not yet present in the table.

**Example:** If your table already has 29,000 companies from a previous import, re-running with the same filters returns only the companies genuinely new since the last run — for example, 32 new companies. The existing 29,000 remain in your table; they are not replaced or removed.

Deduplication is based on each company's unique profile ID, not your filter configuration. A company already in the table is skipped on re-run regardless of whether your filters changed.

**To re-import the full result set** (for example, when testing): delete the existing rows from your table first, then re-run the source. Once the rows are cleared, the search re-imports all matching companies from scratch.

### Re-running Find People returns 0 new results

This is expected behavior. The Find People source deduplicates results against rows already in the table — re-running the same source on a table that already contains those contacts returns 0 new records. There is no setting to disable this: deduplication is always on for the Find People source.

**To get the same contacts back** (for example, when testing your table setup): delete the existing rows from your People table first, then re-run the source. Once the rows are cleared, the search will import the same contacts as before.

**Note:** Deduplication is based on each person's unique profile ID, not your search filters. If the data source returns genuinely new profiles matching your criteria that aren't already in the table, those will still come through on re-run. Only contacts already in the table are filtered out.

### The preview count drops dramatically when editing an existing Find People source

When you open and edit an existing Find People source — for example, to update your filters or add an exclusion list — the preview reflects only *net new* records: people who match your current search criteria and are not already in your table. Clay automatically excludes contacts already imported in previous runs, so the preview count can look far lower than the total universe of matching people.

**Example:** If your table already contains 18,000 imported contacts and you edit the source to add an exclusion list, the preview may show only a handful of results — not because the exclusion list is over-filtering, but because nearly all contacts matching your criteria are already in your table.

**To verify the full count of matching contacts** (for example, to check that your exclusion list is working correctly): create a new Find People search with the same filters and exclusion list. Since the new search starts fresh, the preview shows the complete matching universe — the total matching contacts minus your exclusion list.

### Preview count is much higher than the number of rows actually imported

The **preview count** shown before you run a search reflects the total number of matching people across all companies — it does not account for the **Limit per company** setting. Once you run the search, the per-company cap is applied and the actual row count will be substantially lower.

When searching across a large company table with **Limit per company** enabled, results may only cover a portion of your companies rather than all of them. The search prioritizes returning the full per-company allotment for companies it processes first; if that fills the search's capacity before all companies are reached, the remaining companies return zero results for that run.

To improve coverage across all your companies:

-   **Remove the per-company limit** and use the global **Limit results** setting instead to cap the total.
-   **Reduce your company list size** so that all companies can be processed within a single search run.
-   **Switch to the enrichment action** (Find People at These Companies in-table) rather than the source — it processes each company row individually and returns results per company regardless of list size.

### Find People is returning people from the wrong company

When Clay resolves a domain to a company, it expands the search to include all company records associated with that domain — parent companies, subsidiaries, acquired entities, and other organizations that share URL elements with the target. This means a search for contacts at a specific company can also return contacts who work at related but distinct entities. This is expected behavior: the contacts are real employees at real companies; they just work at an associated organization rather than the exact one you targeted.

**Reduce future spillover:** Switch to the company's **LinkedIn URL** as the input instead of a domain. LinkedIn URLs map directly to the intended company profile and bypass the domain-expansion lookup. See [Use LinkedIn URLs, not domains, as company identifiers](#use-linkedin-urls-not-domains-as-company-identifiers) above.

**Flag contacts from unrelated companies in your existing results:** Add a formula column that compares the contact's company domain against the source organization's domain using only the core domain name — strip the protocol (`http`/`https`), `www`, and TLD suffixes (`.com`, `.co`, `.pt`, etc.) from both before comparing. Rows where the stripped values don't match are contacts from a related but distinct entity. Set this column as a **run condition** on downstream enrichments to gate processing to matched contacts only.

### "Company Table Data" shows "Missing Input" in the people table

After running Find People from a company list, some rows in the resulting people table may show **Missing Input** in the **Company Table Data** column. This happens when a person's current employer uses a different domain than the company you searched — for example, searching on `broadcom.com` returns someone whose current employer resolves to `vmware.com`. Because the domains don't match, Clay can't link that person back to the original company row, leaving the company record ID blank.

This mismatch most commonly occurs with subsidiaries, acquired companies, and organizations that operate under multiple domains.

**To fix this:**

-   **Switch to LinkedIn company URLs as your company identifier** (recommended). When you provide a LinkedIn company URL instead of a domain, Clay uses the LinkedIn company slug for matching — which handles subsidiary and acquisition relationships more reliably. See [Use LinkedIn URLs, not domains, as company identifiers](#use-linkedin-urls-not-domains-as-company-identifiers).
-   **Add a Lookup Rows fallback.** In your people table, add a **Lookup single row in other table** column. Set `Table to search` to your original companies table and match on `domain`. For rows where the person's current company domain is populated, this retrieves company fields directly — even when the automatic Company Table Data link is missing. See [Lookup Rows](lookup-rows.md).

### Enrichment columns show "Missing input" for company rows

If enrichment columns — such as **Enrich Company**, **Find Contacts at Company**, or third-party company enrichments — show **"Missing input"** for some rows, those rows are missing the required identifiers. Most company enrichments require at least one of: a domain, a company name, or a company profile URL.

**Common causes:**

-   **Null or empty domain values** — Rows imported without a domain, or where a domain lookup returned no result, cannot be processed by enrichments that require a domain input.
-   **Invalid domain format** — Domains with extra characters, trailing paths, or protocols (e.g., `https://example.com/about`) may not be accepted by enrichments that expect a bare domain (e.g., `example.com`).
-   **Wrong input column mapped** — If the enrichment column's input is mapped to a column that is empty for some rows, those rows show "Missing input."

**To fix:**

1.  **Check the column's input mapping.** Click the column header → **Edit column** and confirm the input fields point to the correct columns in your table — typically the domain or company name column.
2.  **Identify and fill rows with missing values.** Add a view filter showing only rows where the domain column is empty, then populate the missing domains or other required identifiers.
3.  **Re-run the enrichment.** Right-click the column header → **Run column** → **Run empty or out-of-date rows** once inputs are populated.

**If a recent column configuration change caused the error**, use [Table Version History](table-versions.md) to revert to a working setup: click **History** (bottom-right of the table) → **All configuration versions**, then restore a version from before the change. Restoring a version reverts column configurations without affecting your row data.

### Company Table Data doesn't include company enrichment data

The **Company Table Data** column retrieves basic field types from the linked company row — text, long text, number, boolean, date, email, URL, image, JSON, and formula columns. **Enrichment columns (action-type columns such as Clearbit Company, Apollo, Enrich Company, or any other Clay integration enrichment) are not included** in what Company Table Data returns.

If you enriched your company table and want that data accessible in your people table, use **Lookup single row in other table** instead:

1.  In your people table, add a **Lookup single row in other table** column.
2.  Set `Table to search` to your company table.
3.  Set `Target column` to the company domain column in the company table.
4.  Set `Row value` to the person's company domain column.
5.  Run the lookup.

Lookup Rows returns the full company row including enrichment column outputs. To promote a specific enrichment value into a dedicated column, click into a populated cell and select a field → **Create column for it**. See [Lookup Rows](lookup-rows.md) for setup details.

**Alternatively**, extract specific enrichment values into **formula columns** in your company table first (for example, a column with formula `{{Clearbit Enrichment}}?.revenue`). Formula columns are included in Company Table Data, so those extracted values will flow through to the people table when Company Table Data runs.

### A new column I added to my company table isn't showing in Company Table Data

When you add a new column to your company table after the people table was already created, the **Company Table Data** column in the people table doesn't automatically pick up that new column. The column fetches a fresh snapshot of each linked company row every time it runs — so the new column's data only appears after the next run.

**To pull in newly added company table columns:**

1.  In your people table, right-click the **Company Table Data** column header.
2.  Select **Run column → Force run all [N] rows**.

This re-runs Company Table Data for every row and retrieves the current state of the linked company row, including any columns added since the last run.

**Note:** Only the following field types are returned — text, long text, number, boolean, date, email, URL, image, JSON, and formula columns. Enrichment action columns (Clearbit, Apollo, Enrich Company, etc.) are never included in Company Table Data regardless of re-running — see [Company Table Data doesn't include company enrichment data](#company-table-data-doesnt-include-company-enrichment-data) for how to access enrichment data in your people table.

### "Company Table Data" shows "Unable to fetch fields for company table"

If rows in your **Company Table Data** column fail with the error **"Unable to fetch fields for company table."**, the Table ID in the column configuration contains a leading `/` that prevents Clay from resolving the referenced table.

In Clay input fields, typing `/` opens the column picker so you can reference a value from another column in the row. If a leading `/` appears before a table ID (for example, `/t_0abc123` instead of `t_0abc123`), Clay treats the entry as a column reference rather than a static table ID. Because no column with that name exists, the lookup can't find the table and the error fires for every row.

**To fix this:**

1.  Right-click the **Company Table Data** column header → **Edit column**.
2.  In the configuration panel, locate the **Table ID** field.
3.  Remove the leading `/` so the field contains only the bare table ID (e.g., `t_0abc123...`).
4.  Save and re-run the affected rows.

### Getting "Invalid companies provided" error despite having a valid LinkedIn URL

If you see the error **"Invalid companies provided: please make sure you are using LinkedIn URLs or Company Domains"** but your column already contains LinkedIn URLs, check the URL format. This error occurs when the LinkedIn URL is a **person profile URL** (`linkedin.com/in/<name>`) rather than a company or school page URL — even though the URL itself is valid LinkedIn syntax, the action only accepts company-type identifiers.

Valid inputs for the company identifier field:

-   **Company page URL**: `https://www.linkedin.com/company/<slug>`
-   **School page URL**: `https://www.linkedin.com/school/<slug>`
-   **Company domain**: e.g., `example.com`
-   **Sales Navigator company URL or company ID`

To fix this, replace the person profile URLs in your column with the corresponding company LinkedIn URLs. You can use the **Find Company** or **Enrich Company** enrichments to retrieve a company URL from a company name or domain, then pass that URL into **Find Contacts at Company**.

### Getting "Invalid input: Invalid person identifier" from Enrich person

If cells in your **Enrich person** column show this error, the value in the **Professional URL** field cannot be parsed as a valid LinkedIn profile URL, Sales Navigator URL, or LinkedIn user ID.

**Valid inputs for the Professional URL field:**

-   LinkedIn profile URL: `https://www.linkedin.com/in/<slug>` (e.g., `https://www.linkedin.com/in/satya-nadella`)
-   Sales Navigator profile URL: `https://www.linkedin.com/sales/people/<id>`
-   LinkedIn numeric user ID (e.g., `12345678`)

**Common cause — wrong column mapped to Professional URL:**

This most often happens when a column containing emails, names, company names, or other non-LinkedIn data is accidentally mapped to the **Professional URL** field in the column mapping panel. Open the **Enrich person** column, expand the column mapping, and confirm that the Professional URL field is either left empty or points to a column that contains actual LinkedIn URLs.

**If you only have email addresses:** Leave the **Professional URL** field empty and map only the **Email** field. The action accepts either input. Email-only lookups do not produce this error — if no matching profile exists for the email, the cell shows **"No profile found"** rather than an error.

After correcting the mapping, right-click the column header → **Run column** → **Run [N] empty or out-of-date rows** to re-run the affected cells.

### "Your source has exceeded your plan's limit" error on Find Companies or Find People

If you see **"Your source has exceeded your plan's limit of [N], so future runs will not add new records. Consider creating a new source or moving onto a higher tier plan"**, the source has reached a per-source cumulative record limit enforced by your billing plan.

**The limit is cumulative across all runs of the same source** — not per search. Each time the source imports records, the count accumulates. Once the limit is hit, the source stops adding new records regardless of how many times you re-run it.

**This limit is a row count, not a Data Credits limit.** The number shown (e.g., 100) refers to how many records the source can import in total — not how many Data Credits you have available. Your Data Credits balance is tracked separately and is used for enrichments such as finding emails or company data. Even after a source hits its row limit, your remaining Data Credits are still available for enrichments on rows already in your table.

The limit varies by plan tier and is shown in the error message itself (for example, 100 on free workspaces, 25,000 on Explorer-tier plans, 50,000 on Pro plans and above).

**To continue importing beyond the limit:**

-   **Create a new source.** Add a new Find Companies or Find People source with the same (or adjusted) filters. The new source starts with a fresh record count. Use the **Exclude companies** or **Exclude people** filter to avoid re-importing records already in your table.
-   **Upgrade your plan** to access a higher per-source limit.

**Note:** this limit is separate from the 50,000-row table limit. A source can hit its plan-based record limit even when the table shows fewer visible rows — the source tracks every record it has ever introduced, including rows you've since deleted from the table.

## FAQs

### Why is this person showing up despite having moved companies?

Clay's company and people search relies on snapshot data that may lag behind real-time changes. To confirm current employment, run `Enrich Person` and use the formula in the **Verify current employment** section above to check whether the company matches.

### Why am I finding people with unexpected job titles?

First, check that you're filtering on **Job title keywords** (not just function or seniority). If you're using **Is similar to** mode, you may get some fuzzy matches — filter those out with a formula or AI after the fact.

### Why isn't someone I found on LinkedIn showing in Clay?

Your search filters may be too specific. Try broadening your criteria incrementally. The profile may also not yet be in the dataset.

**Tip for job title filters:** Someone with a compound title — for example, "MD, Head of Mortgages" — may not appear when you search for "Head of Mortgages." Multi-word title phrases that include stop words like "of" can produce unexpected phrase-matching results. Using a shorter, single-word keyword such as "Mortgages" avoids this and catches a wider range of title variations, including "Head of Mortgages," "MD, Head of Mortgages," and "Mortgages Director."

### Why does Find Contacts at Company return "No Profile Found"?

Two main causes:

-   **Privacy or access restrictions** — some LinkedIn profiles are not accessible in the stored dataset due to privacy settings. Profiles set to private on LinkedIn are excluded from what providers can index, so a company may show people on LinkedIn when you're logged in but return no results in Clay.
-   **Stale provider data** — Find Contacts at Company draws from a bulk-refreshed index. If a company's employees haven't been re-indexed recently, the current state of the LinkedIn company page may not yet be reflected. See [How often is company and people data updated?](#how-often-is-company-and-people-data-updated) for details on update cadences.

### How often is company and people data updated?

The answer depends on which feature you're using:

-   **Enrich Person / Enrich Company** — data is fetched close to real-time each time you run the enrichment, pulling the provider's latest available data at the moment of the run.
-   **Find People / Find Companies / Find Contacts at Company (CPJ sourcing)** — these features draw from a pre-indexed dataset that providers refresh through bulk record processing. Results can show some deviation from what you see live on LinkedIn, because the index reflects the provider's most recent batch update rather than an immediate lookup. Data freshness has improved significantly over time, so deviation is rarely a problem in practice.

Across both, high-importance profiles (frequently accessed records, decision-makers, active companies) refresh more often than long-tail profiles.

### Can I run a people search only on companies that meet certain criteria?

Company and people search sources don't support run conditions. The workaround is to create a **filtered view** of your company table (showing only the rows you want), then run **Find People at These Companies** from that view. The source will only process the companies visible in that view.

**Note:** The row limit, starting row, and "Run [N] rows" controls available for enrichment columns do **not** control which companies a Find People source processes — the source always reads from the view it was configured with at setup. Only a filtered view limits which companies are included.

### Can I process a large company list in segments without creating multiple tables?

Yes — use the **Row limit** and **Starting row** settings in the table toolbar to work through a large list in chunks. This is useful when you have a table with tens of thousands of company rows and want to run enrichment-type operations (such as **Find Contacts at Company**) on segments of the list without splitting the data across multiple tables.

Click the **rows** button in the toolbar (it shows the visible row count, for example **50,000/50,000 rows**). A popover opens with two fields:

-   **Starting row** — the row to begin from. Leave blank to start at row 1, or enter a number to skip ahead (for example, enter `10,001` to begin the second batch of 10,000).
-   **Row limit** — the maximum number of rows to include. Enter `10,000` to cap the view to rows 1–10,000.

Click **Save changes**, run your enrichment columns on that segment, then update **Starting row** to advance to the next batch and repeat until you've processed the full list.

**Important:** The row limit and starting row apply to enrichment columns (such as **Find Contacts at Company**). They do **not** control which companies a Find People *source* processes — a source always reads from the view it was configured with at setup. To limit which companies a source processes, use a filtered view instead (see [Can I run a people search only on companies that meet certain criteria?](#can-i-run-a-people-search-only-on-companies-that-meet-certain-criteria) above).

### What's the difference between the people search source and the enrichment action?

The source returns results in a new table and is subject to a per-source cumulative limit that varies by billing plan (see [the troubleshooting section](#your-source-has-exceeded-your-plans-limit-error-on-find-companies-or-find-people) if you hit that limit). The enrichment action saves results to your existing table, returns 10 people by default with full profile data, and supports a **Reduce data for more results** option that returns up to 500 people (name, job title, and professional profile URL only). Use the action when you need to rank or filter contacts before saving them, or when you need more records than a single source allows.

**When you select "Find Contacts at Company," Clay prompts you to choose how to save results:**

-   **Save results in this table** — adds Find Contacts at Company as an enrichment column in your company table. Contacts are stored as a list within each company row. This option costs credits (0.5 credits per row on current plans; 1 credit per row on legacy plans).
-   **Save results in new table** — opens the Find People search instead, which creates a new table with one row per contact. Find People draws from Clay's regularly-ingested people index and does not cost credits.

The outputs are similar. If you want contacts as individual rows without spending credits on the lookup, choose **Save results in new table** to use Find People. Choose **Save results in this table** when you need contacts stored inline with their parent company row.

### I added new companies to my company table — how do I get them through my Find People searches?

**If using Find People as a source (a separate people table):**
Re-running the source is all that's needed. It searches across all companies in the linked table — including any you just added — and appends new people while deduplicating against rows already in the table. To re-run: click the source column header in the people table and select **Run**.

**If your company table has an Update People Table column:** That column is the mechanism that triggers Find People refreshes. Despite the UI warning ("does NOT perform incremental Find People searches for new companies"), the column *does* include newly added companies in the refresh — it re-runs the entire Find People search across all companies currently in the table and appends new contacts to the people table. The warning means the refresh runs the full search rather than an isolated search for just the new rows. With **Enable Automatic People Search Updates** toggled on, the column runs automatically when new company rows are added. If you prefer to trigger it manually, turn that toggle off and run the column on demand.

If you want to add contacts from only the newly added companies without re-searching the entire list, the simple re-run above is usually sufficient: deduplication means only genuinely new contacts are added — contacts already in your people table are not duplicated regardless of how many companies were searched. You pay credits for searching all companies in the table, but only new contacts appear as new rows.

If you want to avoid searching the full company list entirely (to save credits), create a **filtered view** of your company table showing just the new rows, then set up a new **Find People at These Companies** search from that view — this creates a *separate* people table with contacts for only those companies. To reuse your existing search criteria, open the Find People source column (right-click → **Edit column**), click **Save search** at the top of the filter panel, and use that saved search when setting up the new search. See [Saved searches](saved-searches.md) for full details.

**If using Find People as an enrichment action (runs within the company table, per row):**
New company rows trigger Find People automatically when auto-run is enabled — no extra steps needed. See [Disable auto-run on the people table](#disable-auto-run-on-the-people-table-when-running-find-people-selectively) for caveats about downstream enrichment costs when new rows are added.

### Why does my downstream company table have fewer rows than my original company list?

When you run a people search across a company list and route results to a downstream company table — for example, using **Send Table Data** from a people table, de-duplicated by company domain — that destination table only contains companies where at least one person was found. Companies where the people search returned no results never generate a row in the people table, so nothing flows downstream for them.

For example: if your original company list has 3,818 companies and people were found at 2,694 of them, your downstream company table shows 2,694 rows. The remaining 1,124 companies had no contacts found — this is expected behavior, not missing data. The downstream table is a filtered view of only the companies you can reach.

To identify which companies had no people found, add a **Lookup Rows** column to your original company table (searching your people table, matched on company domain) and filter for rows where the count is zero.

### How do I get a unique list of companies from my people table?

If your people table has a **Company Table Data** column (created automatically when you run a people search from a company table), you can extract the company name into its own column and deduplicate it to get a list of unique companies:

1.  **Extract the company name:** Click a cell in the **Company Table Data** column to open the cell details panel. Hover over the **Name** field and click **Add as column**. This creates a new column in your people table containing each person's company name.
2.  **Deduplicate:** Click the header of the new company name column and select **Dedupe** from the dropdown. Review the flagged duplicates and click **Delete** to remove them, leaving only one row per unique company name.

**To work with the deduplicated list in a separate table:** Use [Send Table Data](send-table-data.md) to push the company name column to a destination table, then run **Dedupe** on that column's header in the destination table.

**Note:** Column deduplication removes entire rows from your table based on matching values — deleted rows cannot be recovered. For full rules and caveats, see [Dedupe columns](table-columns-overview.md).

### Why do "Picture URL Copy" and "Picture URL Orig" return null in Enrich Person?

This is expected behavior. Clay stopped returning professional profile picture URLs through the Enrich Person enrichment for privacy and compliance reasons. Both the **Picture URL Copy** and **Picture URL Orig** output fields are present but always return null for all customer workspaces — this is not a bug and is not plan-specific (Growth, Pro, and Enterprise plans are all affected equally).

If you need professional profile photos in your workflow, the alternative is to use a third-party scraping tool integrated with Clay via HTTP API or webhooks:

-   **Phantombuster** — uses your session cookie to access profile photos.
-   **Apify** — offers profile scrapers with authentication.

When using third-party scrapers, ensure your usage complies with the platform's Terms of Service and your organization's data privacy policies.

### How can I find a professional profile URL if I only have a name and an old email address?

Several enrichment providers can match a person's professional profile using a name and an email address — even if the email is personal or from a former employer — though match rates vary depending on how current the data is in each provider's system.

**Step 1: Combine first and last name into a full name**

Add a formula column to concatenate your first and last name columns into a single full name value (for example, `{{First Name}} + " " + {{Last Name}}`).

**Step 2: Run a professional profile enrichment using email and full name**

Add a professional profile enrichment — such as [LiveData Find Professional Profile](livedata-integration.md) or [Minerva Find professional profile](minerva-integration.md) — and map both the **Email** and **Full Name** inputs. These providers accept an email address as a matching signal and return a professional profile URL if the data is present in their systems.

Before running on your full dataset, test on 5–10 rows to gauge match rates and accuracy.

**Step 3 (optional): Improve match rates by adding company name**

If initial results are unsatisfactory, extracting the company name from the email domain can improve matching:

1.  Add the **Identify Email Type and Extract Company Domain from Email** enrichment and map your email column. This extracts the company domain from the address (for example, `jane@acme.com` → `acme.com`).
2.  Use a company enrichment (such as Apollo, ZoomInfo, or Clearbit) to look up the company name from the extracted domain.
3.  Re-run your professional profile enrichment with **Full Name**, **Email**, and **Company Name** all mapped as inputs. The additional company context can improve the match rate.
