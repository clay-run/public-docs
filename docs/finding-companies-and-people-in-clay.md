---
title: "Guide: Finding companies and people in Clay"
source_url: https://university.clay.com/docs/finding-companies-and-people-in-clay
description: Best practices to Clay's company and people search features, including valid LinkedIn URL formats for the company identifier and troubleshooting common errors.
last_synced: 2026-04-26T01:39:59.452Z
---

# Guide: Finding companies and people in Clay

Best practices to Clay's company and people search features.

Clay's `Find Companies` and `Find People` sources give you instant access to billions of company and people profiles — all in one place. Here are the best practices we recommend to streamline your searches and surface the strongest results.

## Company search

### Anchor on description keywords

Industry categories map to the categories companies self-select on LinkedIn — which can be too broad for most use cases. **Description keywords** let you narrow by what a company actually does, not just how it's categorized. Use them heavily as your primary filter, and layer industry categories on top only when needed.

### Use AI filters to avoid paying for data you won't use

A common TAM sourcing mistake is pulling a large list and then running enrichments afterward to qualify it — which means paying credits for companies you'll ultimately discard. **AI filters** (sub-industries, revenue streams, business types, and other derived attributes) let you filter out noise before any rows are returned, so you only pay for companies you actually want.

**Note:** Technographics filtering is also available directly in company search and costs 3 credits per company returned — cheaper in most cases than running a technographic enrichment after the fact, and more direct since you only pay for companies that already match your tech criteria. Technographics data is also available when sending company rows to Audiences; the same credit cost applies.

### Understand how filters combine

Company search uses AND logic across filter types and OR logic within a single filter:

-   **Across filters** — every filter you apply must match. If you set industry + company size + revenue, a company must meet all three criteria.
-   **Within a filter** — any value can match. If you select two industries, a company matching either one is returned.

If you need results that meet _either_ of two different filter combinations, set up two separate searches.

## People search

### Choose your starting point

**If you have a company list**, you have two options depending on how you want to store the results:

-   **Find People at These Companies** (Tools → Find People at These Companies) — creates a separate people table with one row per contact, linked back to the company. Best when you want to run enrichments on each contact individually (work email, phone, etc.) or need to rank/filter contacts before saving.
-   **Find Contacts at Company** (add as a column in your company table) — stores contacts as a list within each company row. Best when you want contacts to stay in your company table, or when you're adding companies one at a time and don't want a single search to re-run across all rows. Use **Send Table Data** afterward to push individual contacts to another table if needed.

If you don't have a company list, use **People search as a source** — a standalone search by title or other criteria that returns a new table.

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

**Find People at These Companies — as an enrichment action (saves to existing table):**

-   Returns 10 people per row by default, with full profile data.
-   `Reduce data for more results` mode returns up to 500 people per row, but only name and LinkedIn URL — you'll need to run `Enrich Person` afterward to get full profiles.
-   Best when you need to rank contacts first or run a more targeted search per company.

**Find Contacts at Company — as a column enrichment (list stored in cell):**

-   Add as a column directly in your company table. Each row independently runs a people search and stores the matching contacts as a list within the cell.
-   Unlike Find People at These Companies, results are not written as rows to a separate people table — they stay in your company table as cell data. Use **Send Table Data** to push individual contacts to another table if needed.
-   Returns **10 contacts per row by default**, with full profile data.
-   `Reduce data for more results` mode returns up to **500 contacts per row**, but only name and LinkedIn URL — run `Enrich Person` on each row afterward to get full profiles.
-   Processes each company row independently — adding a new company row does not re-trigger the enrichment on other rows.
-   Costs **0.5 credits per row** on current pricing plans (1 credit per row on legacy plans).
-   Best when you want contacts to stay associated with their parent company row, or when you're processing companies incrementally and only want to find contacts for specific rows.

### Use dynamic location filtering with in-table actions

When you run `Find People at These Companies` as an in-table action (rather than launching a separate people search), you can dynamically filter by location by referencing a location column from your company table. This lets you customize the location filter per company without running multiple separate searches.

For example, if you have a "Headquarters Location" column in your company table, you can reference that column in the location filter when setting up the in-table action. Each company will then be searched using its specific location, rather than applying a single static location filter across all companies.

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

### Excluding records during enrichment

The exclusion options above remove matched records before they enter your table. If records are already in your table and you want to skip enrichment on contacts that match a suppression list — such as existing customers, competitors, or a broker list — use **Lookup Rows combined with a run condition**:

1.  Import your suppression list as a Clay table (or use an existing one in your workspace).
2.  In your enrichment table, add a **Lookup single row in other table** action. Set `Table to search` to your suppression table and match on a stable identifier — LinkedIn URL for people, or domain for companies.
3.  On each enrichment you want to gate, open **Run settings → Only run if** and add a condition such as `{{Suppression Lookup}} is empty`. The enrichment will only run for records not found in your suppression list.

This pattern is especially useful when your suppression list changes over time (update the lookup table and the condition reflects the new list automatically), when you're pulling contacts from multiple sources and want a single suppression layer, or when you need to exclude records discovered after the initial search.

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

## Troubleshooting

### Find People returns fewer results than expected

Clay uses stored snapshot data rather than live LinkedIn search, so results will never be a perfect mirror of what LinkedIn shows on a company's people page. Common causes:

-   **Private or restricted profiles** — Clay can only surface profiles that are accessible in the stored dataset. Profiles set to private on LinkedIn are excluded.
-   **Domain-to-company mapping issues** — when you provide a domain instead of a LinkedIn URL, Clay resolves it through a company lookup that can occasionally return the wrong entity, especially for subsidiaries, rebranded companies, or companies with stale LinkedIn slugs. Switch to the **LinkedIn company URL** as your input to bypass this lookup entirely.
-   **Filters set too narrowly** — title, location, or seniority filters that are too specific can exclude real matches. Try broadening one filter at a time to diagnose where results drop off.

If profiles still appear to be missing after switching to LinkedIn URLs, use **Claygent** to find the missing profiles via Google search, then pass those LinkedIn URLs directly into `Enrich Person`. This uses a live-scraping fallback that isn't constrained by the stored dataset.

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

### Getting "Invalid companies provided" error despite having a valid LinkedIn URL

If you see the error **"Invalid companies provided: please make sure you are using LinkedIn URLs or Company Domains"** but your column already contains LinkedIn URLs, check the URL format. This error occurs when the LinkedIn URL is a **person profile URL** (`linkedin.com/in/<name>`) rather than a company or school page URL — even though the URL itself is valid LinkedIn syntax, the action only accepts company-type identifiers.

Valid inputs for the company identifier field:

-   **Company page URL**: `https://www.linkedin.com/company/<slug>`
-   **School page URL**: `https://www.linkedin.com/school/<slug>`
-   **Company domain**: e.g., `example.com`
-   **Sales Navigator company URL or company ID**

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

The limit varies by plan tier and is shown in the error message itself (for example, 25,000 on Explorer-tier plans, 50,000 on Pro plans and above).

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

### What's the difference between the people search source and the enrichment action?

The source returns results in a new table and is subject to a per-source cumulative limit that varies by billing plan (see [the troubleshooting section](#your-source-has-exceeded-your-plans-limit-error-on-find-companies-or-find-people) if you hit that limit). The enrichment action saves results to your existing table, returns 10 people by default with full profile data, and supports a **Reduce data for more results** option that returns up to 500 people (name and LinkedIn URL only). Use the action when you need to rank or filter contacts before saving them, or when you need more records than a single source allows.

### I added new companies to my company table — how do I get them through my Find People searches?

**If using Find People as a source (a separate people table):**
Re-running the source is all that's needed. It searches across all companies in the linked table — including any you just added — and appends new people while deduplicating against rows already in the table. To re-run: click the source column header in the people table and select **Run**.

If you want to run on *only* the newly added companies (skipping the full company list), create a **filtered view** of your company table showing just the new rows. To reuse your existing filter criteria without rebuilding them, open the Find People source column (right-click → **Edit column**), click **Save search** at the top of the filter panel to save your current filters, then use that saved search when setting up a new **Find People at These Companies** search on the filtered view. See [Saved searches](saved-searches.md) for full details.

**If using Find People as an enrichment action (runs within the company table, per row):**
New company rows trigger Find People automatically when auto-run is enabled — no extra steps needed. See [Disable auto-run on the people table](#disable-auto-run-on-the-people-table-when-running-find-people-selectively) for caveats about downstream enrichment costs when new rows are added.
