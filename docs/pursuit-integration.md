---
title: Pursuit integration
description: Use the Pursuit integration to build lists of U.S. public sector accounts, verify government contacts, and surface signals from public documents.
last_synced: 2026-09-28T16:43:58.533Z
---

# Pursuit integration

Build lists of U.S. public sector accounts, confirm government contacts, and track public sector signals with the Pursuit integration in Clay.

Pursuit is a data provider for the U.S. public sector, covering government organizations like municipalities, counties, school districts, universities, and special districts. With this integration, you can build a table of public sector accounts, check whether a government contact is still in their role, and surface signals from public documents such as board meeting minutes.

## **Creating a table with Pursuit**

1.  In a workbook, click `+ Add` at the bottom.
2.  Search for `Pursuit` and select one of the two Pursuit sources, both listed under `Find`.
3.  In the modal, you will be asked to `Select Pursuit account`.
    -   If you have your own Pursuit account, click `+ Add account` and enter your Pursuit API key. Otherwise, use the Clay-provided key.

### `Source` Search Pursuit's universe of US government entities

Build a table of U.S. public sector accounts that match the filters you set, with government identifiers, websites, and coordinates for every match.

**Inputs**

Set at least one filter under `Filters`. Filters are combined, so an account has to match all of them.

-   **Account types:** The kinds of public sector organization to return, across 34 categories — municipalities, counties, school districts, fire departments, law enforcement agencies, libraries, universities, tribal governments, and utility, water, transportation, and other special districts among them. Leave empty to include every account type.
-   **States or territories:** The U.S. states or territories an account has to be located in. All 50 states are available, along with the District of Columbia, Puerto Rico, Guam, American Samoa, the Northern Mariana Islands, and the U.S. Virgin Islands.
-   **Name includes any of:** One or more terms an account name has to match, such as `water` or `school`. Terms are matched as whole words rather than as substrings.
-   **Website contains:** Text an account's website has to contain, such as `k12.ca.us`. Wildcards aren't supported.
-   **Minimum population:** The lowest 2022 population estimate to include.
-   **Maximum population:** The highest 2022 population estimate to include.
-   **Maximum results:** How many accounts to return, from 1 to 50,000. Defaults to 1,000.

**Outputs**

-   **Pursuit ID:** Pursuit's identifier for the account, which you can pass to the enrichment actions below.
-   **Pursuit parent ID:** The Pursuit identifier of the account's parent organization, where it has one.
-   **Display name:** The account's name as Pursuit displays it.
-   **Full name:** The account's full name.
-   **Account type:** The kind of public sector organization, such as `Municipality`.
-   **State abbreviation:** The two-letter state or territory code.
-   **URL:** The account's website.
-   **Population estimate (2022):** The population Pursuit estimates the account serves.
-   **Summary level:** The Census summary level codes that classify the account.
-   **Latitude:** The account's latitude.
-   **Longitude:** The account's longitude.
-   Government identifiers, which let you join Pursuit accounts to other public datasets:
    -   **LSADC:** The Census area description code.
    -   **State FIPS:** The federal code for the account's state.
    -   **Place FIPS:** The federal code for the account's place.
    -   **County FIPS:** The federal code for the account's county.
    -   **LEA ID:** The education agency identifier.
    -   **NCES ID:** The National Center for Education Statistics identifier.
    -   **IPEDS ID:** The postsecondary education identifier.
    -   **ORI ID:** The originating agency identifier.
    -   **USASpending PA ID:** The account's identifier in federal spending data.
-   **Total matching accounts:** How many accounts match your filters in total, which can be higher than the number returned.

### `Source` Find public sector signals with Pursuit

Search Pursuit's accounts for recent public documents that match your criteria, and get back one row per signal with a summary and a link to its source.

**Inputs**

Required:

-   **Profile description:** What you sell, in plain language: what your product does, who buys it, and the problem it solves. Pursuit matches signals against this, and two to four sentences works best.
-   **Signal criteria:** Each buying moment you want to hear about, written as a condition a document either meets or doesn't. Enter it under `Description`, set a `Priority` from 1 to 5, and click `Add new criteria` for each additional one. When an account matches more than one criterion, priority decides which signal surfaces first.

Optional:

-   **Account types:** Limits the search to the selected kinds of public sector account. Leave blank to search all Pursuit accounts.
-   **Exclude account types:** Leaves the selected kinds of public sector account out of the search.
-   **States:** Limits the search to accounts in the selected states or territories.
-   **Minimum population:** Only includes accounts whose 2022 population estimate is at least this number.
-   **Maximum population:** Only includes accounts whose 2022 population estimate is at most this number.
-   **Date range:** How far back Pursuit looks for matching documents — `Past 30 days`, `Past 60 days`, `Past 90 days`, or `Past 6 months`. Defaults to `Past 30 days`.
-   **Result limit:** How many signals to return, from 1 to 1,000. Defaults to 100.

**Outputs**

-   **Signal ID:** Pursuit's identifier for the signal.
-   **Summary:** A one-line summary of what Pursuit found.
-   **Public sector account:** The account the signal belongs to.
    -   **Pursuit ID:** Pursuit's identifier for the account.
    -   **Account name:** The account's name.
    -   **State:** The account's two-letter state or territory code.
-   **Source document:** The document the signal came from.
    -   **Source link:** A link to the document in Pursuit.
    -   **Source title:** The document's title.
    -   **Source date:** The date attached to the document.
    -   **Date type:** What that date represents, such as a meeting date.
    -   **Document type:** The kind of document, such as board meeting minutes.
    -   **Source content:** The passage the signal was drawn from.

## **Enriching data with Pursuit**

1.  While in a Clay table, click `Add enrichment` and search for `Pursuit`.
2.  Under `Integrations`, select one of the Pursuit actions.
3.  In the modal, you will be asked to `Select Pursuit account`.

### `Action` Enrich a public sector account

Return firmographic and identifier data for a U.S. public sector account.

**Inputs**

Required:

-   **Company name:** The name of the public sector organization to enrich.
-   **Company state or territory:** The full name or two-letter abbreviation of the state or territory the organization is in, such as California or CA.

Optional:

-   **Company domain:** The organization's domain, which sharpens the match when you have it.

**Outputs**

-   **Match:** How Pursuit matched your row to an account.
    -   **Status:** Whether Pursuit settled on a match. Rows Pursuit can't match finish with no data.
    -   **Category:** The kind of match, such as an exact match.
    -   **Score:** Pursuit's score for the match.
    -   **Reason:** Why Pursuit returned this match.
    -   **Details:** What Pursuit compared, broken into **Match type** and **Matched fields**.
-   **Account:** The matched account's data.
    -   **Pursuit ID:** Pursuit's identifier for the account.
    -   **Pursuit parent ID:** The Pursuit identifier of the account's parent organization.
    -   **Display name:** The account's name as Pursuit displays it.
    -   **Full name:** The account's full name.
    -   **State abbreviation:** The two-letter state or territory code.
    -   **URL:** The account's website.
    -   **Population estimate (2022):** The population Pursuit estimates the account serves.
    -   **Summary level:** The Census summary level codes that classify the account.
    -   **Lat:** The account's latitude.
    -   **Long:** The account's longitude.
    -   **LSADC**, **State FIPS**, **Place FIPS**, **County FIPS**, and **LEA ID:** Government identifiers for the account.

### `Action` Enrich a public sector contact

Check a public sector contact against Pursuit data to see whether the person is still in role, has moved, or has retired, and return corrected details with a confidence score.

**Inputs**

Required:

-   **Full name:** The contact's first and last name.
-   **Pursuit account ID:** The Pursuit identifier of the account the contact works for. (Required if company name and state are not provided)
-   **Company name:** The name of the public sector organization. (Required if Pursuit account ID is not provided)
-   **Company state or territory:** The full name or two-letter abbreviation of the state or territory, such as California or CA. (Required if Pursuit account ID is not provided)

Optional:

-   **Company domain:** The organization's domain, which sharpens account matching.
-   **Job title:** The contact's current job title, which sharpens contact matching.
-   **Email address:** The contact's current email address.
-   **Phone number:** The contact's current phone number.

**Outputs**

-   **Status:** Pursuit's verdict on the contact. When Pursuit can't confirm the person, the status comes back as `unknown` and the row finishes with no data.
-   **Reason:** Why Pursuit landed on that status.
-   **Pursuit ID:** Pursuit's identifier for the account the contact was checked against.
-   **Confidence score:** How confident Pursuit is in the result.
-   **Contact:** The corrected contact details.
    -   **First name:** The contact's first name.
    -   **Last name:** The contact's last name.
    -   **Title:** The contact's job title.
    -   **Email address:** The contact's email address.
    -   **Phone number:** The contact's phone number.
    -   **Professional profile URL:** A link to the contact's professional profile.
-   **Score reasoning:** The evidence behind the score.
    -   **Summary:** A written explanation of what Pursuit could and couldn't confirm.
    -   **Is current:** Whether the contact still works for the account.
    -   **Is current in role:** Whether the contact still holds the same role.
    -   **Is retired:** Whether the contact has retired.
    -   **Has moved:** Whether the contact has moved elsewhere.
    -   **Matched title:** The title Pursuit matched the contact to.
    -   **Email verified:** Whether the email address was verified.
    -   **Email generic:** Whether the email address is a shared inbox rather than a personal one.

### `Action` Find public sector signals for an account

Find signals for one public sector account using a profile description and prioritized criteria.

**Inputs**

Required:

-   **Profile description:** What you sell, in plain language: what your product does, who buys it, and the problem it solves. Pursuit matches signals against this, and two to four sentences works best.
-   **Signal criteria:** Each buying moment you want to hear about, entered under `Description` with a `Priority` from 1 to 5. When the account matches more than one criterion, priority decides which signal surfaces first.
-   **Pursuit ID:** Pursuit's identifier for the account. (Required if account name and state are not provided)
-   **Account name:** The account's name. (Required if Pursuit ID is not provided)
-   **Account state:** The account's state or territory. (Required if Pursuit ID is not provided)

Optional:

-   **Account URL:** The account's website, which sharpens the match when you have it.
-   **Date range:** How far back Pursuit looks for matching documents — `Past 30 days`, `Past 60 days`, `Past 90 days`, or `Past 6 months`. Defaults to `Past 30 days`.
-   **Result limit:** How many signals to return, from 1 to 1,000. Defaults to 100.

**Outputs**

-   **Public sector account:** The account Pursuit searched, broken into **Pursuit ID**, **Account name**, and **State**.
-   **Signals:** Every signal Pursuit found for the account. Each one carries a **Signal ID**, a **Summary**, and a **Source document** with **Source link**, **Source title**, **Source date**, **Date type**, **Document type**, and **Source content**.

### Run settings

-   **Auto-update:** Useful when rows keep arriving in the table, so new accounts and contacts get checked without you rerunning the column.
-   **Only run if:** The enrichment will only run if conditions are met. ([Learn more about conditional formulas here!](https://www.clay.com/university/lesson/ai-formulas-conditional-runs-clay-101))

## **FAQs**

### When does a Pursuit run not use credits?

Rows where Pursuit finds nothing are refunded, so an account it can't match, a contact it can't confirm, or a signal search that comes back empty doesn't cost anything. Runs on your own Pursuit API key don't use credits either.

### Should I use the signal source or the signal action?

Start with `Find public sector signals with Pursuit` when you don't have a list yet. It searches across Pursuit's accounts and returns one row per signal, so the signals themselves become your table.

Reach for `Find public sector signals for an account` when you already have a table of accounts and want signals attached to each row. The two share the same `Profile description` and `Signal criteria` fields, so criteria you've tuned in one carry straight over to the other.

### Why is my signal search still running?

Pursuit searches documents in the background and calls Clay back when it finishes, so the cell reads `Searching for signals` until the results land. Clay waits up to two hours for that callback.

There's nothing to do in the meantime — the cell fills in on its own as soon as Pursuit responds.

### How do I skip account matching?

`Search Pursuit's universe of US government entities` and `Enrich a public sector account` both return a `Pursuit ID`. Map that column into `Pursuit account ID` on `Enrich a public sector contact`, or into `Pursuit ID` on `Find public sector signals for an account`, and Pursuit goes straight to the account instead of matching on name and state.

A Pursuit ID is 24 characters long. If the column holds a value of a different length, the action stops and tells you the ID isn't valid rather than falling back to the name.

### Can the date range come from a column?

Yes. Click the gear button on `Date range`, switch the input type from `Dropdown` to `Text with tokens`, and map a column so every row searches over its own window. Any dropdown in a Clay action offers the same toggle.

The column needs to hold the underlying value rather than the label — `past_30_days`, `past_60_days`, `past_90_days`, or `past_6_months`. Anything else stops the run with a message asking you to select a valid date range.

### What happens when Pursuit can't find the account I named?

`Find public sector signals for an account` reports that no matching Pursuit account was found and asks you to check the account name and state or supply a Pursuit ID. Adding `Account URL` gives Pursuit a second identifier to match on, which makes that less likely.

The two enrichment actions handle it more quietly: they finish with no data rather than an error, so the row stays empty and you can filter on it.
