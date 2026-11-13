---
title: Clay formatters overview
description: Normalize and format your Clay table data using Clay's built-in tools.
last_synced: 2026-04-26T01:39:44.557Z
---

# Clay formatters overview

Normalize and format your Clay table data using Clay's built-in tools.

### Clay Formatters Overview

Clay Formatters allow you to format and normalize your cell data. Most tools on this page run at no credit cost — the Normalize First and Last Names action costs 1 credit per run.

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

### `Action` Normalize First and Last Names

Normalize first and last names by stripping unwanted characters and suffixes. Use this after running enrichments like Enrich Person, which return raw name data from data providers without any normalization applied.

**Note:** This action costs 1 credit per run.

To normalize:

**Step 1:** Input the first name and/or last name you want to normalize. You can provide one or both — each field is normalized independently.

**Step 2:** Configure run settings.

By default, new rows within your Clay table will automatically run this enrichment. Learn more about auto-update in [this brief guide](https://docs.clay.com/en/articles/9642165-auto-update-and-auto-dedupe-table).

To run enrichment only under specific conditions, use formulas that trigger the column when the formula is true. Learn more about AI formulas in [this Clay University lesson](https://www.clay.com/university/lesson/ai-formulas-conditional-runs-clay-101).

**Step 3:** Run your enrichment to normalize the names.

**What gets normalized:**

- **First name** — Takes the first word of the input, capitalizes the first character, and lowercases the rest. For example, `JANE SMITH` → `Jane`.
- **Last name** — Strips everything after the first comma, removes registered trademark symbols (®), standalone credential abbreviations (for example, `PHD`, `MBA`, `MD`), and parenthetical labels (for example, `(Founder)`), then applies title case. For example, `MCDONALD, PHD (Founder)®` → `Mcdonald`.

The action outputs a **Normalized First Name** and a **Normalized Last Name** field.

### How do I split a full name into first and last name before writing to Salesforce or another CRM?

The Normalize First and Last Names action cleans up names that are already in separate first name and last name inputs — it doesn't split a single full name into parts. It also keeps only the first word of the first name, so a double first name such as `Mary Ann` becomes `Mary`. The last name keeps every word, so a surname with particles such as `van den Heuvel` stays whole (`Van Den Heuvel`).

Splitting a full name by spaces — for example, a formula that takes the first word as the first name and the last word as the last name — breaks on double first names and on surnames with particles: `Lisa van den Heuvel` would be written as first name `Lisa` and last name `Heuvel`. To prepare full names for Salesforce (or any CRM that needs separate first and last name fields), use a Use AI column to parse the full name into separate output fields before the CRM write:

1.  Click `Add column` and select `Use AI`. If you're building a function, add the Use AI column inside the function, before the Salesforce **Create record**, **Update record**, or **Create or update record** column.
2.  Write a prompt that tells the model to split the full name into first name, last name, and (if present) middle name and suffix. Tell it explicitly to keep double first names together (for example, `Mary Ann`) and to keep the complete surname, including particles such as `van`, `van den`, `de`, or `von`. Also ask it to flag any name it isn't sure how to split. Insert your full name column into the prompt by typing `/` and selecting the column.
3.  Set **Output format** to **Fields** and add one field for each part — for example, `first_name`, `last_name`, an optional `middle_name`, an optional `suffix`, and a review flag such as `needs_review`.
4.  Run the Use AI column on a sample of edge cases (double first names, surnames with particles, names with suffixes) and check the results before turning on the Salesforce write.
5.  In the Salesforce action, map the `first_name` and `last_name` fields (not the original full name column) to the **First Name** and **Last Name** fields of your Lead or Contact.
6.  On the Salesforce column, check **Add run condition** ("Only run if this formula resolves to true") with a formula that only passes rows where `needs_review` isn't set, so names the AI flagged are reviewed by a person instead of being written to Salesforce automatically.

See [Use AI](use-ai-integration-overview.md) for more on prompts and output fields, and [Salesforce integration](salesforce-integration-overview.md) for the Salesforce actions.

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

**Get a domain from a website URL:** To turn a full website URL into just its domain — for example, a website URL returned by a Claygent or Use AI column, such as `https://www.cdicurbs.com/` → `cdicurbs.com` — add a **Normalize a Domain** column, map it to the website column, and select the **Isolate the domain** normalization type.

**Note — Normalize a Domain doesn't visit the website:** The Normalize a Domain action only cleans up the text of the URL (for example, removing the `https://`, the `www.`, and anything after the domain). It doesn't open or check the website, so a normalized domain such as `example.com` may not load in your browser even when it's the correct domain — some companies' websites only load on the www. version (`www.example.com`). To check whether a website is live, use the [Check if URL is Valid](url-validator-integration-overview.md) action with **Try variants** turned on, which also tries the www. version of the URL.

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
