---
title: Work Email waterfall
source_url: https://university.clay.com/docs/work-email-waterfall
description: Find and validate work emails faster — the Work Email waterfall
  cascades across multiple providers in sequence, stopping as soon as a valid
  result is found.
last_synced: 2026-04-26T01:40:55.862Z
upstream_hash: ff14ab13b199adda600aaff776334bff62196b289ff02f26626417f59c488351
---

# Work Email waterfall

Find and validate work emails faster — the Work Email waterfall cascades across multiple providers in sequence, stopping as soon as a valid result is found.

The Work Email waterfall finds and validates a person's work email address by cascading across multiple email finding providers in sequence — stopping as soon as one returns a valid result.

You only pay credits for the provider that finds a match, making it one of the most credit-efficient ways to build email coverage at scale.

## **Setting up the Work Email waterfall**

1.  In your table, click `Add enrichment` in the top right corner.
2.  Search for `Work Email`  and select it from the results.
3.  Choose between `Quick setup` and `Full configuration`
4.  Map your input columns and click `Save`.

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

### Which email pattern should I use?

The best pattern depends on the companies in your dataset. `first.last@domain.com` is the default because it's the most common format across industries. For more specific datasets, test a small sample (~10 rows) with different patterns to find what performs best before running at scale.

### Does Infer Email cost credits?

No. `Infer Email` is completely free. The validation step _does_ cost Clay credits, but it is cheaper than running the waterfall without it.

### What happens if Infer Email guesses the wrong email?

If the inferred email fails validation, the waterfall moves on to the next provider as normal. No credits are charged for the failed `Infer Email` step.

### When should I adjust the Threshold for duplicate results?

Consider setting it to `2` when you're using `Conservative` validation and noticing that multiple providers are all returning the same email that keeps failing. Left at `0`, the waterfall will continue through every provider, spending credits on a result it's already decided to reject.

### Can I use both Infer Email and a validation strategy together?

Yes — and this is the recommended setup for cost-efficient workflows. `Infer Email` handles the free first attempt; your validation strategy then controls how the rest of the waterfall evaluates results from paid providers.
