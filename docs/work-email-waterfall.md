---
title: Work Email waterfall
description: Find and validate work emails faster — the Work Email waterfall
  cascades across multiple providers in sequence, stopping as soon as a valid
  result is found.
last_synced: 2026-04-26T01:40:55.862Z
---

# Work Email waterfall

Find and validate work emails faster — the Work Email waterfall cascades across multiple providers in sequence, stopping as soon as a valid result is found.

The Work Email waterfall finds and validates a person's work email address by cascading across multiple email finding providers in sequence — stopping as soon as one returns a valid result.

You only pay credits for the provider that finds a match, making it one of the most credit-efficient ways to build email coverage at scale.

## **Setting up the Work Email waterfall**

1.  In your table, click `Add enrichment` in the top right corner.
2.  Search for `Work Email`  and select it from the results.
3.  Choose between `Quick setup` and `Full configuration`
4.  Map your input columns and click `Save`.

**Note:** Most providers need at minimum a **full name** and **company domain** for each row — make sure those fields are populated in your table before running. Providing a LinkedIn URL or company name as additional inputs gives more providers enough data to run.

The Work Email waterfall includes two advanced settings — `Infer Email` and `Validation` — that work together to give you more control over credit efficiency and result quality.

`Infer Email` attempts a free email guess before calling any paid provider, while `Validation` settings let you define what counts as a valid result and when the waterfall should stop searching. Both are available in `Full configuration` mode.

## Infer Email

Infer email inserts a free step at the beginning of your waterfall that constructs an email address from a person's name and company domain using a common naming pattern. If the inferred email passes validation, the waterfall stops immediately — no paid providers are called. If it fails, the waterfall continues to the next step as normal.

Because this step costs zero credits, it can meaningfully reduce per-row spend when the pattern matches correctly. In Clay's internal testing on a software-industry dataset, the default `first.last@domain.com` pattern returned a valid email roughly 31% of the time.

### Enabling Infer Email

1.  While in a table, click `Tools` → open the `Work Email` waterfall.
2.  Scroll to the bottom of the `Inputs` section and toggle on `Include infer-email enrichment as first step?`
3.  In the `Column mapping` panel that appears, configure your inputs (see below).
4.  Click `Save waterfall step`.

**Inputs**

-   `Email Pattern` (required): The naming pattern used to construct the email address. Defaults to `first.last@domain.com`.
-   `Domain` (required): The company domain to use when constructing the email (e.g. `clay.com`).
-   `Name Inputs` (at least one required, depending on the pattern selected):
    -   `First Name`.
    -   `Last Name`.
    -   `Middle Name` — only needed for the `first.[middle_initial].last@domain.com` pattern.

**Tip:** Email naming conventions vary by company and industry. Test on a small sample before running at scale to assess how well a given pattern performs for your dataset.

## Validation

The `Validation` section in `Full configuration` controls how the waterfall evaluates whether an email result is good enough to stop on. Getting this right is what ties the whole waterfall together — too strict and you'll over-spend chasing elusive emails; too loose and you'll accept results that bounce.

### Validation provider and strategy

`Validation Provider` (optional): The provider used to validate each email. When set, a validation column is added after each provider step.

`Require validation success?`: When toggled on, the waterfall only accepts an email if the validation provider explicitly confirms it as valid. When off, the waterfall may accept emails where validation was inconclusive.

`Validation strategy`: Controls your risk tolerance for what counts as a valid email. Select from:

-   `Conservative` — The safest approach, including all verified email types. Best when deliverability matters (e.g. cold outreach where bounce rates affect sender reputation).
-   `Balanced` — Moderate risk level, including catch-alls. A good middle ground when you want some coverage of catch-all domains.
-   `Aggressive` — Higher risk level, good for casting a wide net. Best when volume and coverage take priority over precision.
-   `Advanced` — Manual configuration for fine-grained control over validation behavior.

### Additional column settings

`Output name of successful provider?` (optional): When enabled, adds a column showing which provider successfully found the email.

`Hide provider columns?` (optional, on by default): Hides the intermediate per-provider columns, keeping your table clean. Disable if you want to see which provider returned each result.

`Threshold for duplicate results` (optional, default `0`): Stops the waterfall early if the same email keeps failing validation across multiple providers. Setting this to `0` disables the feature. Set to `2` or higher to stop the waterfall after the same invalid email appears that many times — preventing credits from being spent running additional providers that are likely to return the same result.

**Tip:** The `Threshold for duplicate results` setting is especially useful when paired with the `Conservative` strategy — if a catch-all email keeps failing conservative validation across providers, the threshold prevents the waterfall from continuing to spend credits on the same result.

## FAQs

### How do I find an email for a specific contact?

Make sure the contact's row has the required input data (full name and company domain at minimum). Then select the Work Email cell on that row, right-click, and choose **Run 1 cell**. The waterfall checks providers in sequence and stops as soon as one returns a valid email. For more ways to run enrichments on a subset of rows, see [Run progress](run-progress.md).

### How do I run the Work Email waterfall on a specific set of rows?

To run the waterfall on multiple contacts at once — without running the full table — you have two options:

- **Select and run specific cells:** Click the Work Email cell for the first row you want to run, then drag (or **Shift+click**) to extend the selection across additional rows in that column. Right-click the selection and choose **Run [N] cells**. The waterfall runs only on the selected rows.
- **Run all empty or out-of-date rows:** Click the ▶ button in the Work Email waterfall column header and select **Run empty or out-of-date rows**. This processes every row in the column that hasn't yet returned a result or is marked as out-of-date.

For a full reference on run options — including a row limit and starting row — see [Run progress](run-progress.md).

### What does it mean if no email is found?

If the cell shows no result, click into it to see which providers were tried and what each returned. Common reasons no email surfaces:

-   The row is missing required input data. Check that the contact's full name and company domain are populated.
-   **An upstream column that provides required inputs was skipped due to a run condition.** If a column that feeds data into your email waterfall — such as a company domain lookup, company match, or people search — is showing **"Run condition not met"**, that cell is empty. The email waterfall then sees blank inputs and shows **"Missing input"** for those rows. Open the settings for the upstream column and review its **Only run if** condition — if the condition is preventing rows it should be processing from running, adjust it so the required data gets populated first. See [Conditional runs](conditional-runs.md) for how run conditions work and how skipped cells affect downstream columns.
-   None of the providers in your waterfall have email data for this person. You can edit the waterfall sequence to add more providers.
-   The providers ran but returned results that failed validation. Try a less strict validation strategy, or check the individual provider columns (enable them in waterfall settings) to see what was returned.
-   Your workspace ran out of credits mid-waterfall. When credit limits are hit, remaining providers in the sequence don't execute — click into the cell to see how far the waterfall got before stopping. See [Actions and data credits](actions-data-credits.md) to add more credits.

### What match rate should I expect from the Work Email waterfall?

For a well-configured Work Email waterfall with good input data, a match rate of **60–75%** is typical across most B2B contact lists. Results vary based on:

-   **Input data completeness** — rows with a company domain and full name consistently get higher match rates. Missing either input significantly limits which providers can run.
-   **Your list composition** — match rates vary by industry, geography, and contact type. Some datasets skew higher; others skew lower.
-   **Number of providers** — more providers in the waterfall sequence give more opportunities to find an email.

If you're seeing rates well below 60%, see [How can I improve my email match rate?](#how-can-i-improve-my-email-match-rate) below. If you're already near 70% and have optimized your inputs and provider sequence, you may be close to the ceiling for your specific contact list — some contacts simply don't have emails findable through any commercial data provider.

### How can I improve my email match rate?

If you want to find emails for more of your contacts, here are the most effective steps to take:

1.  **Make sure Company Domain and full name are populated.** Most providers need both to run. Rows without a company domain in particular are skipped by a large portion of the waterfall. If you only have a company name, use the [Company Domain waterfall](building-a-data-waterfall.md) to find domains first.

2.  **Add profile URLs for your contacts.** Mapping professional profile URLs as an additional input can expand which providers are able to run on each row, increasing your overall coverage.

3.  **Check which providers are finding emails.** In the waterfall's Full Configuration, toggle off `Hide provider columns?` to reveal individual per-provider result columns. This shows you exactly which providers are returning emails for your list and where coverage drops off — useful for identifying whether adding new providers might help.

4.  **Add more providers to your waterfall.** In Full Configuration, click **Add provider**. Different providers cover different datasets, so a longer sequence gives more chances to find emails your current providers missed.

### Why do some rows show "Invalid input" with a message about a first or last name?

This error appears when the **Full Name** input contains a value that can't be separated into a distinct first name and last name. Most providers in the Work Email waterfall require at minimum a first and last name — a single-word value, a company name, or a name missing either first or last will cause those providers to return **"Invalid input"**.

**Common causes:**

-   The Full Name column contains a single word with no space (e.g., `"Smith"` instead of `"John Smith"`)
-   A company name or other non-person text is mapped to the Full Name field
-   First and last name are stored in separate columns but weren't combined before mapping

**How to fix it:** Map the **Full Name** input to a column that contains a person's complete name with both a first and last name separated by a space (e.g., `"John Smith"`).

If your table stores first and last names in **separate columns**, create a formula column that combines them:

`{{First Name}} + " " + {{Last Name}}`

Then map that formula column to the **Full Name** field in the waterfall inputs.

### Which email pattern should I use?

The best pattern depends on the companies in your dataset. `first.last@domain.com` is the default because it's the most common format across industries. For more specific datasets, test a small sample (~10 rows) with different patterns to find what performs best before running at scale.

### Does Infer Email cost credits?

No. `Infer Email` is completely free. The validation step _does_ cost Clay credits, but it is cheaper than running the waterfall without it.

### How much does the Work Email waterfall cost per email?

You only pay for the provider step that successfully finds an email — providers that run and return nothing are not charged. Total credit cost per matched email depends on which provider in the sequence finds a result first: if the first provider succeeds, you pay that provider's cost; if the waterfall tries two or three providers before finding a valid email, you pay for each attempt. Credit costs vary by provider and your plan tier. To reduce per-email spend, enable `Infer Email` — it adds a free first step that can skip paid providers entirely when the naming pattern matches.

For additional strategies — including connecting your own provider API keys (which drop the Clay credit cost for that step to 0) or using Lookup Columns to pull existing email data before the waterfall runs — see [Ways to save Clay credits](clay-credit-conservation.md).

### What happens if Infer Email guesses the wrong email?

If the inferred email fails validation, the waterfall moves on to the next provider as normal. No credits are charged for the failed `Infer Email` step.

### Why did multiple providers run in a row?

The step-by-step conditional logic that controls which provider runs next is built into the waterfall — you do not need to add a conditional formula between individual provider steps, and you cannot configure the inter-step logic directly.

Each provider in the sequence runs only when no valid email has been found yet: if the previous provider returned nothing, the next provider runs; if the previous provider returned an email that failed validation, the next provider also runs. This continues until a valid email is found (the waterfall stops) or all providers have run without returning a valid result.

**If multiple providers keep returning the same invalid email:** use the **Threshold for duplicate results** setting to stop the waterfall early when the same address appears repeatedly. Set it to `2` to stop after the same email has failed validation twice in a row. See [Additional column settings](#additional-column-settings) for details.

### When should I adjust the Threshold for duplicate results?

Consider setting it to `2` when you're using `Conservative` validation and noticing that multiple providers are all returning the same email that keeps failing. Left at `0`, the waterfall will continue through every provider, spending credits on a result it's already decided to reject.

### Why does an email appear in a provider column but not in the final output?

The most common cause is validation: when `Require validation success?` is enabled, an email only reaches the final output column if the validation provider confirms it as valid. If validation marks the email as invalid, the final output column stays blank — even though a provider did find an email. The waterfall continues running remaining providers in case a later one returns a different, valid email address.

To confirm this is what happened: in the waterfall's `Full configuration`, turn off `Hide provider columns?` and re-run. The individual validation columns will show you what each provider returned and whether the email passed or failed validation.

**If validation is rejecting emails you want to keep:**

-   Switch to a less strict `Validation strategy` — for example, `Balanced` or `Aggressive` instead of `Conservative`.
-   Remove the validation provider entirely — any email found will then flow directly to the final output column without being checked.

**A related sub-case — same email found by multiple providers:** To avoid paying for validation twice, the waterfall skips re-validation for any email address that was already found and validated (as invalid) by an earlier provider step. If Provider 3 finds the same email address that Provider 1 already returned and confirmed as invalid, the validation column for Provider 3 will show **run conditions not met** and that email will not be written to the final output column. This is expected behavior — the waterfall continues searching because a later provider might still return a different, valid email.

If you need to use an email that a later provider found despite an earlier invalid result, you can manually paste it into your output column, or create a formula column that pulls directly from the individual provider result columns.

### Why does my own email address appear in the Work Email results?

If your own email address shows up in the Work Email output column, a field containing your own email — such as an "Account Owner" column synced from a CRM — has likely been wired to one of the waterfall's input fields. The waterfall passes mapped inputs directly to providers without checking whether the value belongs to you or to a contact, so any field mapped to an email input is used as-is.

**How to fix it:** Open the waterfall settings and review which column is mapped to each input field. Remove any column that contains your own email address or account-owner information from the input mapping.

### Why does the validation step show "Click to run" instead of running automatically?

If a validation column shows **"Click to run"** on rows where an email was already found, your table is most likely in manual mode — auto-run is disabled at the table level. When table-level auto-run is off, downstream columns (including validation steps in a waterfall) do not execute automatically, even when an upstream provider successfully finds a result.

To have validation run automatically right after an email is found:

1.  Click the `⛭` icon in the top toolbar (or click the table name → **Run Settings**).
2.  Toggle **Auto-run** on.
3.  Choose **Continue without running** or **Update cells** depending on whether you want to process existing rows immediately.

Once auto-run is enabled at the table level, the waterfall will flow through to the validation step on its own as soon as an email is found.

**Note:** Table-level auto-run is the master switch — even if a column's own auto-run is enabled, it won't fire if the table-level setting is off. See [Table management settings](table-management-settings.md) for a full breakdown of how table-level and column-level auto-run interact.

### Can I use both Infer Email and a validation strategy together?

Yes — and this is the recommended setup for cost-efficient workflows. `Infer Email` handles the free first attempt; your validation strategy then controls how the rest of the waterfall evaluates results from paid providers.

### Can I run additional validators after the waterfall?

Yes. The waterfall's built-in `Validation Provider` supports one provider at a time, validating emails as the waterfall finds them. To layer additional validators in sequence — for example, running a second email verification enrichment as an extra check after the waterfall completes — add them as **separate enrichment columns** after the waterfall column rather than trying to fit them inside the waterfall itself.

**Example setup for layered validation:**

1. **Work Email waterfall** — with your primary validation provider set (e.g., LeadMagic or ZeroBounce)
2. **Second validator column** (e.g., a Debounce "Validate Email" enrichment) — set its **Only run if** condition to `/Work Email is not empty` so it only runs after the waterfall has found an email
3. **Third validator column** (optional) — set its **Only run if** to reference the second validator's output, for example to run only on emails that returned a specific status from the previous step

You can chain as many validators as needed this way. Each column's **Only run if** condition references the previous column's output, creating a sequential validation flow without requiring all validators to be part of the same waterfall step.

**Tip:** Before running at scale, test by right-clicking a single row and choosing **Run 1 cell**, or enable [sandbox mode](sandbox-mode.md) to try your full validation sequence without consuming live credits.

For a full reference on writing conditional run formulas, see [Conditional runs](conditional-runs.md).
