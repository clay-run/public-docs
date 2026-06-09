---
title: Waterfalls
source_url: https://university.clay.com/docs/building-a-data-waterfall
description: Maximize your data coverage with waterfalls.
last_synced: 2026-04-27T18:09:26.920Z
---

# Waterfalls

Maximize your data coverage with waterfalls.

Waterfalls allow you to utilize multiple data providers in a predetermined sequence, so you don't duplicate tasks or spend extra credits.

## Using pre-built waterfalls

To run a pre-built waterfall:

1.  Click `Add enrichment` on the top right corner of your table and search for the data point you want to run a waterfall for (ex. Phone number). Under `Waterfalls`, select the waterfall you want to run.
2.  Configure your `Waterfall sequence`. You can reorder, add. or delete your waterfall data providers.
    -   To skip a step in the waterfall, click the toggle switch next to a specific provider.
3.  Enter the required data inputs, such as email addresses or social profile URLs, to set up the enrichment waterfall.
4.  In the **Waterfall output** dropdown, select which sub-field to display in the waterfall's merged column (for example, `people > 0 > title`). You can only pick one field at a time — but all individual provider columns are still added to your table with their full data regardless of which field you select. You can access any field from a provider column by clicking into a row or referencing it in a formula.
5.  Optionally, choose to output the name of the successful provider and hide the provider columns for a cleaner table view.
6.  Configure Run settings, including enabling auto-update or setting conditions for when the waterfall should run.

## Editing an existing waterfall

To add, remove, or reorder providers in a waterfall you've already saved:

1.  Click the waterfall column header to open the column menu.
2.  Select **Edit column**.
3.  If the waterfall shows a **Quick setup** / **Full configuration** tab selector, click **Full configuration**.
4.  In the **Waterfall sequence** section, you can:
    -   Click **Add provider** to add a new data provider.
    -   Drag providers up or down to reorder them.
    -   Click the delete icon next to a provider to remove it.
5.  Click **Save**.

## Creating a waterfall

1.  While in a table, click `Add column` (which you will find at the far right side).
2.  Select `Waterfall` and click the `🖊️` to next to the title to rename.
3.  Change the `Data Type` that you'll be working with.
4.  Add actions to the waterfall and adjust other settings.
5.  Click `Save`.

## Creating a waterfall template

Waterfall templates allow you to save and reuse your waterfall configuration, making it easier to standardize and replicate successful workflows.

1.  While creating a waterfall, select `Save as template`.
2.  Give your template a name, description, and category.
3.  Select `Save template`.

**Note:** Waterfall templates cannot be edited, only created and deleted.

## Running a waterfall on specific rows

To run your waterfall on a specific set of rows — for example, to test it on a small sample before running the full table — select those rows by clicking a row number and dragging (or **Shift+clicking**) to extend the selection, then right-click and choose **Run [N] rows**. This runs all enrichment and waterfall columns on only those rows.

For more manual run options, see [Run progress](run-progress.md).

## Avoiding unintended credit usage

By default, auto-run is **on** for every table — waterfall columns (such as a work email waterfall) fire automatically on every new row as it arrives. If rows are added to your table before your waterfall setup is finalized, all steps in the waterfall trigger immediately and consume credits.

**Best practice while building or testing:** Turn off table-level auto-run before adding rows. This prevents the waterfall from firing until your configuration is ready. See [Table management settings](table-management-settings.md) for how to enable and disable auto-run at the table level and per column.

**To prevent a waterfall from re-running on rows that already have a result**, add an **"Only run if"** condition to the waterfall column — for example, `Email is empty`. Clay skips the waterfall for any row where the output field is already populated, preventing duplicate enrichment and unnecessary credit spend.

For more ways to control credit usage, see [Ways to save Clay credits](clay-credit-conservation.md).

## How waterfall validation works

Email waterfalls include a validation step after each provider to confirm whether the email found is valid. However, validators are designed to skip if the same email address has already been returned and found invalid by an earlier step in the sequence.

If two providers in a waterfall both return the same email address, and the first validator already confirmed it's invalid, the second validator won't run — its column will show **Run condition not met**. This is expected behavior, not an error. Re-validating an email that was already tested would waste credits without adding new information.

Because the waterfall can't predict what any given provider will return, all providers in the sequence still run normally. Only the validation step is skipped when the returned value is already known to be invalid.

Validation steps skipped with **Run condition not met** do not consume credits — Clay automatically refunds those steps.

To limit the number of providers the waterfall calls when the same invalid email keeps appearing across multiple steps, use the **Threshold for duplicate results** setting in the Work Email waterfall's **Additional column settings**. Setting this to `2` or higher stops the waterfall from calling additional providers once the same email has appeared that many times consecutively. See [Work Email waterfall](work-email-waterfall.md) for full configuration details.

## Viewing per-provider results

After a waterfall runs, click the **»** arrow on the waterfall column header to expand the column group and reveal each provider's individual sub-column. Each sub-column shows that provider's result for every row:

-   A sub-column that found a result displays the value it returned.
-   A sub-column that was skipped because an earlier provider already found a result shows **Run condition not met**.
-   Click into any individual provider sub-column cell to open that provider's details panel for that specific row.

To add a dedicated column per row showing the winning provider's name, enable **Output name of successful provider?** in the waterfall's output settings.

## Waterfall results and data quality

Waterfall enrichments return the first result found from a provider in your sequence — there is no built-in confidence score or confidence level on the output. For enrichments like company employee count, revenue, or company description, providers return a value when they find one; there is no high/medium/low rating attached to the result.

This is different from AI columns (such as Use AI or Claygent), where you can define structured output fields — including a confidence score — as part of your column setup.

**To improve data reliability with waterfalls:**

-   **Cross-validate across providers.** Run the same enrichment from two or three providers in separate columns, then use a formula or AI column to flag rows where results are consistent across sources. Matching results across providers indicate higher data confidence.
-   **Track which provider returned the result.** When configuring your waterfall output, enable the option to output the name of the successful provider. This lets you filter or score rows based on which data source you trust most.

**Company revenue reflects total annual revenue, not ARR.** Revenue figures returned by enrichment providers such as PDL, Clearbit, Apollo, and Owler represent estimated total company revenue — not annual recurring revenue (ARR) or any subscription-specific metric. These figures are drawn from public filings, web data, and provider estimates.

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

1.  In your table, click `Add enrichment` in the top right corner.
2.  Search for `Find company domain` and select the **Company Domain** waterfall.
3.  Map the column containing company names as the input.
4.  Click `Save`.

**Input required:** Company name  
**Output:** Company domain (e.g., `clay.com`)

### Credit usage

Each provider step that runs costs 1 credit. The waterfall stops at the first provider that returns a domain, so you pay only for the steps that run before a result is found. Best case (Clearbit finds a match): 1 credit. Worst case (no provider finds a domain): 3 credits.

**Tip:** To avoid running the waterfall on rows that already have a domain, add an **Only run if** condition — for example, `Domain is empty` — in the waterfall's run settings.

### Google step: accuracy and workarounds

The Google step finds a domain by running a web search for the company name. Because it relies on search engine rankings rather than a curated database, it can return an incorrect domain when the company name appears prominently on another site — for example, a business-listing directory, a credit-check platform, or any other site that has indexed the company's profile.

This is the most common cause of unexpected results from the Company Domain waterfall: Clearbit didn't find a match, so Google fell back to a web result that ranked highly for the company name — returning that site's domain instead of the company's own website.

**To reduce incorrect results:**

-   **Skip the Google step** — In the waterfall's **Waterfall sequence** configuration, toggle off the Google provider. The waterfall then only queries Clearbit and HG Insights, which draw from structured company databases rather than live web search. You'll get fewer overall matches but higher accuracy on the ones you do find.
-   **Use Claygent instead** — For the most reliable domain finding, set up a Claygent column that searches for the company name and verifies the found URL belongs to the right company before returning a domain. Claygent uses AI credits rather than standard waterfall credits.
