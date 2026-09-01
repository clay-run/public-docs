---
title: Waterfalls
description: Maximize your data coverage with waterfalls.
last_synced: 2026-04-27T18:09:26.920Z
---

# Waterfalls

Maximize your data coverage with waterfalls.

Waterfalls allow you to utilize multiple data providers in a predetermined sequence, so you don't duplicate tasks or spend extra credits.

## Using pre-built waterfalls

To run a pre-built waterfall:

1.  Click **Tools** in the top right corner of your table, select the **Enrich** tab, and search for the data point you want to run a waterfall for (e.g. `Phone number`). Under **Waterfalls**, select the waterfall you want to run.
2.  Configure your `Waterfall sequence`. You can reorder, add. or delete your waterfall data providers.
    -   To skip a step in the waterfall, click the toggle switch next to a specific provider.
3.  Enter the required data inputs, such as email addresses or social profile URLs, to set up the enrichment waterfall.
4.  In the **Waterfall output** dropdown, select which sub-field to display in the waterfall's merged column (for example, `people > 0 > title`). You can only pick one field at a time — but all individual provider columns are still added to your table with their full data regardless of which field you select. You can access any field from a provider column by clicking into a row or referencing it in a formula.
5.  Optionally, choose to output the name of the successful provider and hide the provider columns for a cleaner table view.
6.  Configure Run settings, including enabling auto-update or setting conditions for when the waterfall should run.

## Editing an existing waterfall

To add, remove, or reorder providers in a waterfall you've already saved:

1.  Click the waterfall tab — the labeled bar spanning your waterfall's provider columns — to open the waterfall menu, then select **Edit group**.
2.  In the waterfall editor, click the **Full configuration** tab if it is not already selected.
3.  In the **Waterfall sequence** section, you can:
    -   Click **Add provider** to add a new data provider.
    -   Drag providers up or down to reorder them.
    -   Click the delete icon next to a provider to remove it.
4.  Click **Save**.

### Preserving existing data when reorganizing providers

When you reorder, add, or remove providers in a waterfall, Clay marks existing rows as out-of-date. With table-level auto-run enabled (the default), those rows can be automatically re-run — which may overwrite data you want to keep.

To reorganize a waterfall without overwriting existing results:

1.  In the save dialog, choose **Save and don't run**. This saves your updated configuration without immediately re-running any rows.
2.  Add an **Only run if** condition to the waterfall column — for example, `[Output column] is empty` — so the waterfall skips rows that already have a result. This protects existing data even if rows are later re-queued.

**To apply the updated waterfall to new or empty rows only:**

1.  Filter your table view to show only the target rows — for example, by filtering where the waterfall output column is empty.
2.  Right-click the waterfall column header and choose **Run column** → **Run [N] empty or out-of-date rows**. Clay runs the waterfall only on rows visible in the filtered view.

## Creating a waterfall

Use this when you want to chain multiple enrichment providers for the same data point — for example, enriching company details from Clearbit, then Apollo, then PDL in sequence, stopping as soon as one returns a result.

1.  While in a table, click **Add column** (at the far right of the table).
2.  Select **Waterfall** and click the ✏️ icon next to the title to rename it.
3.  Set the **Data Type** to match what you want the waterfall to output — for example, **Text** for a company name or description, **URL** for a website, or **Number** for revenue or headcount.
4.  In the **Waterfall sequence** section, click **Add provider** to add enrichment providers as steps. You can add as many as you need and reorder them by dragging.
5.  Click **Save**.

## Creating a waterfall template

Waterfall templates allow you to save and reuse your waterfall configuration, making it easier to standardize and replicate successful workflows.

1.  While creating a waterfall, select `Save as template`.
2.  Give your template a name, description, and category.
3.  Select `Save template`.

**Note:** Waterfall templates cannot be edited, only created and deleted.

## Building a provider cascade with run conditions

Use this pattern when you want to chain enrichment steps where each provider tries a **different approach** — for example, attempting a targeted contact database first, falling back to a broader enrichment tool, and falling back again to a people search — rather than multiple providers all returning the **same data point** (which is what the built-in waterfall column handles).

Common examples:
- Cognism lookup → Apollo Enrich Person → Find People at Company
- A region-specific data source for priority contacts → a general enrichment provider as fallback

**No Audiences intermediate step or manual kickoff is required.** Run conditions evaluate automatically as each enrichment completes, so the cascade runs end-to-end without intervention.

### Setting it up

1. **Add your first enrichment column** and set its **Run settings → Only run if** condition so it runs when its prerequisite exists — for example, `/Redeem ID is not empty` to run a Cognism redemption step only when a Cognism redeem ID is available.

2. **Add your fallback enrichment column** and set its run condition to check whether the previous step produced a result. For example, to run Apollo Enrich Person only when the first step produced no email:

   `/First Step Email is empty`

3. **Add your last-resort enrichment column** (for example, Find People at Company) and gate it on all earlier steps having returned nothing:

   `/First Step Email is empty AND /Second Step Email is empty`

4. **Add a formula column to combine results** from all providers into a single merged field. For example:

   `{{First Step Email}} || {{Second Step Email}}`

   Name this column something like `Combined Email`. This single field tells you whether any step in the cascade found a result, regardless of which provider succeeded.

5. **Gate any downstream steps** — CRM writes, Send Table Data, work email enrichment, and so on — on the combined field. For example, to run a subsequent enrichment only on rows where the full cascade returned nothing:

   `/Combined Email is empty`

   Or, to push to a CRM only after the cascade has completed and found a result:

   `/Combined Email is not empty`

When Auto-run is enabled (the default), each enrichment column fires as soon as its dependencies are ready and its run condition is met — so the cascade progresses automatically row by row without any manual intervention.

**Tip:** Rows where a run condition is not met show **"Run condition not met"** in that enrichment's cell — this is expected, not an error. It means that provider was correctly skipped because an earlier step already succeeded for that row, or the prerequisite for that step was not present. See [Conditional runs](conditional-runs.md) for more on how run conditions work.

## Running a waterfall on specific rows

To run your waterfall on a specific set of rows — for example, to test it on a small sample before running the full table — select those rows by clicking a row number and dragging (or **Shift+clicking**) to extend the selection, then right-click and choose **Run [N] rows**. This runs all enrichment and waterfall columns on only those rows.

For more manual run options, see [Run progress](run-progress.md).

## Running a specific provider vs. re-running the full waterfall

When a waterfall is in its **collapsed** view (only the merged output column is visible), clicking the run ▶ button triggers **all enabled providers** in the waterfall sequence — not just one. **Run empty or out-of-date rows** fires every enabled provider for rows that are empty, errored, or out-of-date. **Force run all rows** (available from the column header dropdown) re-runs every enabled provider on every row and overwrites all previously found results.

**To run only a specific provider** — for example, after adding a new provider to extend coverage on rows that didn't get a result yet:

1.  Click the **«»** arrow on the waterfall column header to expand the waterfall and reveal each provider's individual sub-column.
2.  Right-click that provider's sub-column header and choose **Run column** → **Run [N] empty or out-of-date rows**.

Running an individual sub-column triggers only that provider. Other providers and their existing results are not affected.

**Note:** Editing the waterfall configuration — such as adding a new provider or changing provider toggles — can mark existing rows as out-of-date. Running the collapsed output on out-of-date rows re-runs all currently enabled providers for those rows, which may produce different results if your provider selection has changed since the last run.

## Avoiding unintended credit usage

By default, auto-run is **on** for every table — waterfall columns (such as a work email waterfall) fire automatically on every new row as it arrives. If rows are added to your table before your waterfall setup is finalized, all steps in the waterfall trigger immediately and consume credits.

**Best practice while building or testing:** Turn off table-level auto-run before adding rows. This prevents the waterfall from firing until your configuration is ready. See [Auto-run](auto-run.md) for how to enable and disable auto-run at the table level and per column.

**To prevent a waterfall from re-running on rows that already have a result**, add an **"Only run if"** condition to the waterfall column — for example, `Email is empty`. Clay skips the waterfall for any row where the output field is already populated, preventing duplicate enrichment and unnecessary credit spend.

For more ways to control credit usage, see [Ways to save Clay credits](clay-credit-conservation.md).

## How waterfall validation works

Email waterfalls include a validation step after each provider to confirm whether the email found is valid. However, validators are designed to skip if the same email address has already been returned and found invalid by an earlier step in the sequence.

If two providers in a waterfall both return the same email address, and the first validator already confirmed it's invalid, the second validator won't run — its column will show **Run condition not met**. This is expected behavior, not an error. Re-validating an email that was already tested would waste credits without adding new information.

Because the waterfall can't predict what any given provider will return, all providers in the sequence still run normally. Only the validation step is skipped when the returned value is already known to be invalid.

Validation steps skipped with **Run condition not met** do not consume credits.

To limit the number of providers the waterfall calls when the same invalid email keeps appearing across multiple steps, use the **Threshold for duplicate results** setting in the Work Email waterfall's **Additional column settings**. Setting this to `2` or higher stops the waterfall from calling additional providers once the same email has appeared that many times consecutively. See [Work Email waterfall](work-email-waterfall.md) for full configuration details.

## Viewing per-provider results

After a waterfall runs, click the **»** arrow on the waterfall column header to expand the column group and reveal each provider's individual sub-column. Each sub-column shows that provider's result for every row:

-   A sub-column that found a result displays the value it returned.
-   A sub-column that was skipped because an earlier provider already found a result shows **Run condition not met**.
-   A sub-column that returned an error shows the error message for that row — an error does not stop the waterfall. The record automatically falls through to the next provider in the sequence. The waterfall only stops when a provider returns a valid result or all providers have been tried.
-   Click into any individual provider sub-column cell to open that provider's details panel for that specific row.

To add a dedicated column per row showing the winning provider's name, enable **Output name of successful provider?** in the waterfall's output settings.

## Expanding contacts from a people waterfall into a new table

When your waterfall uses contact-finding providers (such as Find Contacts at Company), each provider sub-column stores the full list of returned contacts as an array. The merged waterfall output column shows only the single field you selected during setup (for example, a contact's profile URL or name) — it does not contain the full array, so the **Take action on list** button does not appear when you click into the merged column.

To send each contact as its own row to a new table for downstream enrichment (such as Work Email or Enrich Person):

1.  Click the **»** arrow on the waterfall column header to expand the waterfall and reveal each provider's sub-columns.
2.  Click into a cell in one of the provider sub-columns (for example, a "Find Contacts at Company" sub-column).
3.  In the **Cell details** panel, click **Take action on list** → **Write each item to new row in other table**.
4.  Select the destination table.

This opens the **Send Table Data** configuration with the correct list pre-populated. See [Send table data](send-table-data.md) for full details, including the 20-item-per-row limit.

## Manually overwriting a merge column value

If a waterfall returns an incorrect value in the merge column, you can replace it manually:

1.  Double-click the cell in the merge column.
2.  Type the correct value, or delete the existing value.
3.  Press Enter to save.

A pencil icon appears in the cell to indicate the value has been manually overwritten. To prevent the waterfall from re-running and replacing your edit, add an **Only run if** condition to the waterfall column — for example, `Domain is not empty`.

## Waterfall results and data quality

Waterfall enrichments return the first result found from a provider in your sequence — there is no built-in confidence score or confidence level on the output. For enrichments like company employee count, revenue, or company description, providers return a value when they find one; there is no high/medium/low rating attached to the result.

This is different from AI columns (such as Use AI or Claygent), where you can define structured output fields — including a confidence score — as part of your column setup.

**To improve data reliability with waterfalls:**

-   **Cross-validate across providers.** Run the same enrichment from two or three providers in separate columns, then use a formula or AI column to flag rows where results are consistent across sources. Matching results across providers indicate higher data confidence.
-   **Track which provider returned the result.** When configuring your waterfall output, enable the option to output the name of the successful provider. This lets you filter or score rows based on which data source you trust most.
-   **Check that the enriched company domain matches the contact's email domain.** Enrichment providers use a best-match algorithm — they return the company they believe is the right match based on name or profile data, and do not validate that the returned company's domain matches the contact's email address. If a contact's profile is outdated (for example, a person recently changed jobs but their profile still shows their previous employer), providers may return data for the old company. See [Handling email/company domain mismatches](#handling-emailcompany-domain-mismatches) below for detection and remediation steps.

**Company revenue reflects total annual revenue, not ARR.** Revenue figures returned by enrichment providers such as PDL, Clearbit, Apollo, and Owler represent estimated total company revenue — not annual recurring revenue (ARR) or any subscription-specific metric. These figures are drawn from public filings, web data, and provider estimates.

### Handling email/company domain mismatches

When enriching a person or company, providers match on name or profile data — not on whether the returned company domain agrees with the contact's work email. A contact whose profile still shows a previous employer can come through your waterfall with the wrong company and title, and a company domain that doesn't match their email address.

**Detecting mismatches:** Add a formula or AI column that extracts the domain from the contact's work email (the portion after `@`) and compares it to the enriched company domain. A boolean "Domain Match" column makes it easy to filter and audit mismatched rows at scale.

**Preventing mismatches from reaching downstream systems:** Use the domain-match column as a run condition on downstream write steps — for example, your **Update CRM Record** or **Create CRM Record** action — so a contact is only pushed when the email domain and company domain agree. See [Conditional runs](conditional-runs.md) for how to set this up.

**Fixing contacts that are already mismatched:**

1. Filter the table to rows where the domain-match column is `false`.
2. Re-enrich the company using the email domain as the primary input instead of the company name. A validated work email domain is a more reliable signal than a profile-based best-match result.

## Trial plan and provider restrictions

Waterfall enrichments are available on all plans, including the Trial plan. However, some individual providers within a waterfall require a paid plan.

Providers that can return phone numbers — such as PDL (People Data Labs), Bytemine, and others — require the Launch plan or higher. When a waterfall template includes one or more of these providers, Trial users see the error:

> Your subscription does not allow this integration to be added.

This error can appear even when your goal is to find something other than a phone number (for example, a LinkedIn URL), because the provider is phone-number gated regardless of which output you're looking for.

**To work around this on a Trial plan:** open the waterfall's `Waterfall sequence` configuration and remove any providers that return phone numbers. The remaining providers will work normally. To use all providers without restriction, upgrade to a paid plan.

## Company Domain waterfall

The **Company Domain** waterfall finds a company's website domain from its name by cascading across three providers in sequence — stopping as soon as one returns a result.

Provider order: **Clearbit → Google → HG Insights**

### Setting up the Company Domain waterfall

1.  In your table, click **Tools** in the top right corner, then select the **Enrich** tab.
2.  Search for `Find company domain` and select the **Company Domain** waterfall.
3.  Map the column containing company names as the input.
4.  Click `Save`.

**Input required:** Company name  
**Output:** Company domain (e.g., `clay.com`)

### Credit usage

Each provider step that runs costs 1 credit. The waterfall stops at the first provider that returns a domain, so you pay only for the steps that run before a result is found. Best case (Clearbit finds a match): 1 credit. Worst case (no provider finds a domain): 3 credits.

**Tip:** To avoid running the waterfall on rows that already have a domain, add an **Only run if** condition — for example, `Domain is empty` — in the waterfall's run settings.

### Fixing "Missing input" errors in a domain-dependent waterfall

If a downstream waterfall — such as **Company Revenue** — shows **Missing input** for certain rows, and clicking a failing cell reveals a message like *"Company domain or HG company ID is blank"*, the domain column is empty for those rows. Domain-dependent waterfalls require a company domain to run; rows where the domain is blank are skipped before any external API call is made, so no credits are charged for those rows.

To resolve this without losing those rows, use this three-step pattern:

1. **Add a Company Domain waterfall column and run it conditionally.** In its run settings, add an **Only run if** condition — for example, `[Domain column] is empty` — so the Company Domain waterfall only runs on rows that are missing a domain. Rows that already have a domain are skipped.
2. **Add a formula column that merges the two domain sources.** Use the `||` operator: `{{Domain}} || {{Company Domain}}`. This returns the original domain when it is present, and the Company Domain waterfall result when it isn't. The result is a single resolved-domain column that is populated for every row where a domain could be found.
3. **Update the downstream waterfall's domain input to use the merged column.** Open the Company Revenue waterfall (or any other domain-required enrichment), change its domain input to point to the merged formula column, and save.

### Google step: accuracy and workarounds

The Google step finds a domain by running a web search for the company name. Because it relies on search engine rankings rather than a curated database, it can return an incorrect domain when the company name appears prominently on another site — for example, a business-listing directory, a credit-check platform, or any other site that has indexed the company's profile.

This is the most common cause of unexpected results from the Company Domain waterfall: Clearbit didn't find a match, so Google fell back to a web result that ranked highly for the company name — returning that site's domain instead of the company's own website.

**To reduce incorrect results:**

-   **Use the Excluded Domains field on the Google step** — In the Google provider's settings within the waterfall, expand the **Excluded Domains** optional field and enter specific domains you want to block from results (for example, `proff.no`, `tracxn.com`, `rocketreach.co`). Note: due to a known issue, this filtering may not work reliably in all cases.
-   **Skip the Google step** — In the waterfall's **Waterfall sequence** configuration, toggle off the Google provider. The waterfall then only queries Clearbit and HG Insights, which draw from structured company databases rather than live web search. You'll get fewer overall matches but higher accuracy on the ones you do find.
-   **Use Claygent instead** — For the most reliable domain finding, set up a Claygent column that searches for the company name and verifies the found URL belongs to the right company before returning a domain. Claygent uses AI credits rather than standard waterfall credits.

## Tech Stack waterfall

The **Tech Stack** waterfall finds which technologies a company has installed by cascading across four providers — stopping as soon as one returns a result.

Provider order: **SimilarWeb → Predict Leads → BuiltWith → Apollo**

### Setting up the Tech Stack waterfall

1.  In your table, click **Tools** in the top right corner, then select the **Enrich** tab.
2.  Search for `Tech stack` and select the **Tech Stack** waterfall.
3.  Map the column containing company domains as the input.
4.  Click `Save`.

**Input required:** Company domain  
**Output:** Technologies detected at the company

### Provider strengths

Each provider detects technology using different methods:

-   **SimilarWeb** — Identifies technologies installed on a domain, including installation and uninstallation dates and technology categorization. Draws from web analytics and crawl data.
-   **Predict Leads** — Sources technology data from historical job descriptions, website script tags, and DNS records. Surfaces tools that appear in hiring descriptions, including software not visible in website source code.
-   **BuiltWith** — Scans a company's public website source code to find client-side technologies: marketing pixels, JavaScript libraries, and front-end software embedded in the site.
-   **Apollo** — Returns technology data as part of its company profile enrichment. Note: the Apollo step requires your own Apollo account connected to Clay via Apollo's OAuth flow (**Settings → Connections** → connect Apollo and authorize access). If no Apollo account is connected, the waterfall cannot be saved — you'll need to either connect an Apollo account or manually toggle the Apollo step off (skipped) in the waterfall sequence before saving.

### Verifying whether a company uses a specific product

For verifying whether a company uses a particular enterprise product — including back-end platforms, CRMs, ERP systems, and service software that doesn't appear in website code — use the separate **Verify Product Usage** waterfall. This waterfall uses HG Insights, which analyzes business documents such as contracts, RFPs, and job postings to surface internally-deployed tools that front-end scanners can't detect.

To set up Verify Product Usage:

1.  In your table, click **Tools** in the top right corner, then select the **Enrich** tab.
2.  Search for `Verify Product Usage` and select the waterfall.
3.  Map your company domain column as the input and specify the product you want to verify.
4.  Click `Save`.

See [HG Insights integration](hg-insights-integration-overview.md) for more details on HG Insights' detection methodology and what types of technologies it covers best.

### Other providers for tech stack enrichment

**Sumble** is available as a standalone enrichment action (not part of a pre-built waterfall). It validates whether a company uses specific technologies you select, charging 6 credits per technology found. Use it when you need targeted confirmation of named tools rather than a broad technology scan. See [Sumble integration](sumble-integration.md).

**Claygent** supplements database-backed tech stack enrichment by searching the web for signals of technology adoption. It is most useful for open-source or infrastructure frameworks — such as LangChain or AWS Bedrock — that leave no footprint in website source code and may not appear in database provider catalogs. Add a Claygent column to your table, use the company domain as an input variable, and write a mission prompt such as: *"Does {{company_domain}} use [technology name]? Search the company's website, blog posts, GitHub repositories, case studies, and press mentions, and return yes or no with the evidence found."* See [Claygent](claygent-builder.md) for setup details.

**Note:** 6sense is not available as a waterfall provider in Clay. Store Leads enriches e-commerce site traffic data and is not part of any technographic waterfall.
