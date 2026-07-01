---
title: Clay formatters overview
description: Format your Clay table data for free.
last_synced: 2026-04-26T01:39:44.557Z
---

# Clay formatters overview

Format your Clay table data for free.

### Clay Formatters Overview

Clay Formatters allow you to format your cell data without using any credits.

### `Action` Format Date/Time

Transform a given date or datetime into a given format.

To format your date/time:

**Step 1:** Input the date and format

Select the date or datetime you want to parse and the format of the value you want to convert the value to.

**(Optional) Step 2:** Specify the timezones of the original and new values.

- **Original Timezone** — The timezone your input date is stored in. If left blank, it defaults to UTC. Select a UTC offset from the dropdown (for example, UTC-6 for Central Standard Time, UTC-5 for Eastern Standard Time).
- **New Timezone** — The timezone to convert the output date to. If left blank, the output stays in the original timezone.

To convert a datetime from one timezone to another, set **Original Timezone** to the source timezone and **New Timezone** to the target timezone. For example, to convert a stored UTC timestamp to Central Standard Time, set Original Timezone to UTC and New Timezone to UTC-6.

**(Optional) Step 3:** Select the language of your locale.

**Step 4:** Configure run settings.

By default, new rows within your Clay table will automatically be formatted. Learn more about auto-update in [this brief guide](https://docs.clay.com/en/articles/9642165-auto-update-and-auto-dedupe-table).

To run enrichment only under specific conditions, use formulas that trigger the column when the formula is true. Learn more about AI formulas in [this Clay University lesson](https://www.clay.com/university/lesson/ai-formulas-conditional-runs-clay-101).

**Step 5:** Run your enrichment to format date/time.

**Tip — CRM date compatibility:** To push a date to a CRM or other system that requires a numeric timestamp, select **Unix Timestamp** from the Format dropdown in Step 1. After running the formatter, keep the output column type set to **Text** (not Date) — storing a Unix timestamp in a Date-type column can cause formatting issues because Clay's Date column type expects a date-formatted string, not a number.

### `Action` Normalize Company Name

Normalize your company names by removing terms like Inc., LLC, and other suffixes for a cleaner format.

To normalize:

**Step 1:** Input the company name you want to normalize

**(Optional) Step 2:** Enable the 'Normalize Case' option to automatically transform company names into Title Case (Ex. 'SALESFORCE' to 'Salesforce')

**Step 3:** Configure run settings.

By default, new rows within your Clay table will automatically be formatted. Learn more about auto-update in [this brief guide](https://docs.clay.com/en/articles/9642165-auto-update-and-auto-dedupe-table).

To run enrichment only under specific conditions, use formulas that trigger the column when the formula is true. Learn more about AI formulas in [this Clay University lesson](https://www.clay.com/university/lesson/ai-formulas-conditional-runs-clay-101).

**Step 4:** Run your enrichment to normalize your company name.

### `Action` Normalize a Domain

Extract and standardize a domain URL to the format you need. To add this action to your table, click **+ Add Column → Enrich Data** and search for **"Normalize a Domain."**

To normalize a domain:

**Step 1:** Input the URL you want to normalize.

**Step 2:** Select a **Normalization Type**:

- **Remove prefix** — strips the protocol and www prefix but keeps the path. For example, `https://apple.com/products` → `apple.com/products`.
- **Include www.** — adds a www. prefix. For example, `apple.com` → `www.apple.com`.
- **Include https://** — adds the https:// protocol. For example, `www.apple.com` → `https://www.apple.com`.
- **Isolate the domain** — extracts only the root domain and top-level domain (TLD), stripping all subdomains and paths. For example, `https://corporate.apple.com/products` → `apple.com`. Use this option when you want to match or deduplicate records by primary domain. This mode requires a recognized, publicly listed TLD (such as `.com`, `.org`, or `.io`) — domains with non-standard or reserved TLDs (for example, `.test` or `.local`) are not extracted and the action returns the original URL unchanged.

**Step 3:** Configure run settings.

By default, new rows within your Clay table will automatically be formatted. Learn more about auto-update in [this brief guide](https://docs.clay.com/en/articles/9642165-auto-update-and-auto-dedupe-table).

To run enrichment only under specific conditions, use formulas that trigger the column when the formula is true. Learn more about AI formulas in [this Clay University lesson](https://www.clay.com/university/lesson/ai-formulas-conditional-runs-clay-101).

**Step 4:** Run your enrichment to normalize the domain.

**Note:** This action normalizes the format of a single URL — it does not identify whether two different domains (for example, `meta.com` and `facebook.com`) belong to the same company. For that use case, use a [Claygent](claygent-builder.md) prompt that checks whether two domains resolve to the same organization.

### `Action` Normalize Phone Number

Format and normalize phone numbers to e164, international, and national formats.

To normalize:

**Step 1:** Input the phone number you want to normalize

**Step 2 (Optional):** Enter a country code to include in the formatted phone number. If no country code is provided or included in the input number, it will default to "US."

**Step 3:** Configure run settings.

By default, new rows within your Clay table will automatically be formatted. Learn more about auto-update in [this brief guide](https://docs.clay.com/en/articles/9642165-auto-update-and-auto-dedupe-table).

To run enrichment only under specific conditions, use formulas that trigger the column when the formula is true. Learn more about AI formulas in [this Clay University lesson](https://www.clay.com/university/lesson/ai-formulas-conditional-runs-clay-101).

**Step 4:** Run your enrichment to normalize your phone number.

### `Action` Remove Extra Whitespace from Text

Removes extra whitespace from input text.

To format text:

**Step 1:** Input the text you want to remove extra whitespace from

**Step 2:** Configure run settings.

By default, new rows within your Clay table will automatically be formatted. Learn more about auto-update in [this brief guide](https://docs.clay.com/en/articles/9642165-auto-update-and-auto-dedupe-table).

To run enrichment only under specific conditions, use formulas that trigger the column when the formula is true. Learn more about AI formulas in [this Clay University lesson](https://www.clay.com/university/lesson/ai-formulas-conditional-runs-clay-101).

**Step 3:** Run your enrichment to remove extra whitespace from text.

### `Action` Normalize and Deduplicate a List

Remove duplicate values from a list of items within a single cell, with automatic normalization applied before comparison.

**Note:** This enrichment operates on the contents of a single cell — for example, an array of domains or email addresses stored in one row. It does **not** compare values across rows. To remove duplicate rows from your table based on a column's values, use the [column-level Dedupe option](https://university.clay.com/docs/table-columns-overview) instead.

Normalization trims leading/trailing whitespace and converts all string values to lowercase before checking for duplicates, so `Dyson.com` and `dyson.com` are treated as the same value.

To normalize and deduplicate a list:

**Step 1:** Input the list of values you want to normalize and deduplicate. This can be an array or a comma-separated string (for example, a multi-value cell).

**(Optional) Step 2:** Enable **Remove empty values** to strip blank entries before returning the list. This setting is on by default.

**Step 3:** Configure run settings.

By default, new rows within your Clay table will automatically run this enrichment. Learn more about auto-update in [this brief guide](https://docs.clay.com/en/articles/9642165-auto-update-and-auto-dedupe-table).

To run enrichment only under specific conditions, use formulas that trigger the column when the formula is true. Learn more about AI formulas in [this Clay University lesson](https://www.clay.com/university/lesson/ai-formulas-conditional-runs-clay-101).

**Step 4:** Run your enrichment. The output includes a **Deduped List Object** (the unique values as an array) and a **Deduped String** (the unique values joined with commas).
