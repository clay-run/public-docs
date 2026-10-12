---
title: GovSpend integration
description: Import state and local bids and RFPs, research public sector agencies, and find government contacts using the GovSpend integration in Clay.
last_synced: 2026-09-28T16:43:58.120Z
---

# GovSpend integration

Import state and local bids and RFPs, research public sector agencies, and find government contacts with the GovSpend integration in Clay.

GovSpend is a government procurement data provider covering public sector bids, the agencies that post them, and agency contacts. With this integration, you can import bids into a table, pull the full details and documents for the ones worth pursuing, and enrich the agencies behind them with their bid history, employee counts, and contacts.

## **Creating a table with GovSpend**

1.  In a workbook, click `+ Add` at the bottom.
2.  Search for the `Find bids and RFPs` source, or select `GovSpend` under `Integrations`.
3.  In the modal, you will be asked to `Select GovSpend account`.
    -   If you have your own GovSpend account, click `+ Add account` and enter your GovSpend API key. Otherwise, use the Clay provided key.

### `Source` Find bids and RFPs

Import state and local bids and RFPs into a table, one row per bid, with enough detail to decide which ones are worth pulling documents for.

**Inputs**

Filters combine, so a bid has to match every filter you set.

Required — provide at least one of these:

-   **Keyword:** Words to match against the bid's title, description, summary, and bid number. Every word you enter has to match.
-   **Agency name:** One agency to import bids from, by name, such as `City of Dallas`.
-   **Agency ID:** GovSpend's ID for the agency. It's more precise than `Agency name` and takes priority when you set both.
-   **State:** The full name of the posting agency's state, such as `Georgia`.
-   **City:** The posting agency's city.
-   **County:** The posting agency's county.
-   **Agency type:** One of 21 kinds of agency, such as `Counties`, `K12 Districts`, `Higher Ed`, or `Public Utilities`.

Optional:

-   **Level of government:** `Federal`, `State`, or `Local`.
-   **Set-aside program:** A set-aside program the bid has to fall under, such as `Small Business` or `Veteran-Owned`.
-   **Bid status:** `Open bids`, `Due in the next 30 days`, `Due in the next 90 days`, `Closed bids`, or `Open and closed bids`. Defaults to `Open bids`. `Closed bids` import newest-posted first, and the other options import by due date, earliest first.
-   **Minimum awarded amount:** Only imports bids worth at least this amount, in U.S. dollars.
-   **Maximum awarded amount:** Only imports bids worth at most this amount, in U.S. dollars.
-   **Number of bids to import:** How many bids to import, from 1 to 10,000. Defaults to 100. Only the first 10,000 matching bids can be imported, so tighten your filters when more than that match.

**Outputs**

Each bid becomes a row with these columns:

-   **Bid title:** The bid's title.
-   **Bid ID:** GovSpend's unique ID for the bid.
-   **Bid details URL:** A link to the bid in GovSpend.
-   **Bid number:** The bid's reference number, such as `26-181`.
-   **AMSC code:** The bid's AMSC code in GovSpend.
-   **Set-aside program:** The set-aside program the bid falls under, where it has one.
-   **Due date:** The date the bid is due.
-   **Posted date:** The date the bid was posted.
-   **Record created:** When GovSpend added the bid to its records.
-   **Awarded amount:** The bid's awarded amount, in U.S. dollars.
-   **Number of documents:** How many documents are attached to the bid.
-   Details about the agency that posted the bid:
    -   **Agency ID:** GovSpend's ID for the agency.
    -   **Agency name** and **Agency name and state:** The agency's name, on its own and with its state, such as `Augusta-Richmond County, Georgia`.
    -   **Agency type:** The kind of agency, such as `Consolidated City-County`.
    -   **Level of government:** The agency's level of government, such as `Local`.
    -   **Agency city**, **Agency county**, **Agency state**, **Agency state code**, and **Agency ZIP code:** Where the agency is located.
    -   **Agency website:** The agency's website.
    -   **Fiscal year start month** and **Fiscal year end month:** The months the agency's fiscal year starts and ends, as numbers from 1 to 12.

## **Enriching data with GovSpend**

1.  While in a Clay table, click `Add enrichment` and search for `GovSpend`.
2.  Under `Integrations`, select one of the GovSpend actions.
3.  In the modal, you will be asked to `Select GovSpend account`.

**Note:** `Enrich agency's aggregated bid activity` and `Enrich employee count by criteria` take a GovSpend agency ID rather than a name. Rows from `Find bids and RFPs` already carry one in `Agency ID`; for any other list of agencies, run `Enrich agency` first and map the `Agency ID` it returns into the next action.

### `Action` Get bid document details

Get the full description, summary, and attached documents for a single bid.

**Inputs**

Required:

-   **Bid ID:** GovSpend's ID for the bid, such as a value from the `Bid ID` column that `Find bids and RFPs` creates. A bid number won't work here, since only the bid ID is unique across GovSpend.

**Outputs**

-   **Bid title:** The bid's title.
-   **Description:** The bid's full description.
-   **Summary:** The bid's summary.
-   **Bid number:** The bid's reference number.
-   **Department:** The department listed on the bid, such as `Procurement`.
-   **Number of documents:** How many documents are attached to the bid.
-   **Documents:** The attached documents, each with its **File name**, **Content type**, **Download URL**, **File size in bytes**, and **Content ID**.
-   **Bid details URL:** A link to the bid in GovSpend.
-   **Due date**, **Posted date**, and **Awarded amount:** The bid's key dates and its value in U.S. dollars.
-   **Agency ID**, **Agency name**, **Agency name and state**, and **Agency website:** The agency that posted the bid.
-   **Bid ID:** The bid's GovSpend ID.

### `Action` Enrich agency

Look up a public sector agency by name, website, or GovSpend ID, and get its basic details, population size, and employee count.

**Inputs**

Required — provide at least one of these:

-   **Agency name:** The agency's name. Partial, informal, or abbreviated names work, such as `Broward Schools`.
-   **Agency website:** The agency's website, such as `https://willcounty.gov`. Clay searches on the distinctive part of the domain, such as `willcounty`, and uses `Agency name` instead when you provide both.
-   **Agency ID:** GovSpend's numeric ID for the agency, such as `6086`. It returns that exact agency and ignores the other inputs.

Optional:

-   **State:** The state's full name or two-letter abbreviation, such as `Florida` or `FL`. Recommended when the agency name alone is ambiguous.
-   **City:** A city to narrow the results to, such as `Hallandale Beach`.
-   **Agency type:** One of 32 kinds of agency, such as `Counties`, `K12 Districts`, `Tribal Communities`, or `Public Defender`.

**Outputs**

-   **Number of matches:** How many agencies matched your inputs. A `1` means the lookup landed on a single agency.
-   **Agencies:** Up to 10 matching agencies. Each carries:
    -   **Agency ID:** GovSpend's ID for the agency.
    -   **Name** and **Name and state:** The agency's name, on its own and with its state.
    -   **Agency type:** The kind of agency, such as `Counties`.
    -   **Level of government:** The agency's level of government, such as `Local`.
    -   **Address**, **City**, **County**, **State**, **State code**, and **ZIP code:** Where the agency is located.
    -   **Phone number** and **Website:** The agency's phone number and website.
    -   **Population** and **Population year:** The agency's population size and the year that figure comes from.
    -   **Employee count** and **Employee count year:** How many people the agency employs and the year that figure comes from.
    -   **GovSpend profile URL:** A link to the agency's profile in GovSpend.

### `Action` Enrich agency's aggregated bid activity

Count the bids a public sector agency has posted, in total and year by year.

**Inputs**

Required:

-   **Agency ID:** GovSpend's ID for the agency to analyze.

Optional:

-   **Bid status:** `All bids`, `Open bids only`, or `Closed bids only`. Defaults to `All bids`.

**Outputs**

-   **Total bids:** How many of the agency's bids match `Bid status`.
-   **Bids in the latest year:** How many bids the agency posted in its most recent year with bids, which can be the current, partial year.
-   **Average bids per year:** **Total bids** divided by **Years with bid activity**, rounded to one decimal place.
-   **Years with bid activity:** How many years appear in **Bids by year**.
-   **First year with bids** and **Latest year with bids:** The earliest and most recent years in **Bids by year**.
-   **Total bid documents:** How many documents are attached across those bids.
-   **Agency ID:** The agency the counts are for.
-   **Bids by year:** One entry per year, grouped by the year each bid was posted, with **Year**, **Number of bids**, and **Number of documents**.

### `Action` Enrich employee count by criteria

Count the contacts GovSpend has on file for an agency, broken down by occupation, job title, and state.

**Inputs**

Required:

-   **Agency ID:** GovSpend's ID for the agency to count contacts for.

Optional:

-   **Job title contains:** Only counts contacts whose job title matches these words, such as `Procurement`.
-   **Department contains:** Only counts contacts in departments matching these words, such as `Public Works`.
-   **Occupation contains:** Only counts contacts whose occupation matches these words, such as `Financial Managers`. Occupations use Standard Occupational Classification (SOC) names.

Leave the optional inputs empty to count every contact GovSpend has for the agency. When you set more than one, a contact has to match all of them.

**Outputs**

-   **Number of contacts:** How many contacts match.
-   **Average profile completeness:** The contacts' average profile completeness, GovSpend's score for how fully a contact's profile is filled in.
-   **Agency ID:** The agency the count is for.
-   **Contacts by occupation:** The 10 occupations with the most matching contacts.
-   **Contacts by job title:** The 10 job titles with the most matching contacts.
-   **Contacts by state:** Matching contacts by two-letter state code.

Each breakdown entry carries a **Value**, which is the occupation, job title, or state code, along with a **Number of contacts** and an **Average profile completeness**.

### `Action` Find people

Find contacts at a public sector agency, such as procurement officers, decision-makers, and department heads.

**Inputs**

Required — provide one of these:

-   **Agency name:** The agency to find people at. Distinctive words work best, such as `Broward School` rather than `Broward County School Board`.
-   **Agency ID:** GovSpend's ID for the agency. It's more precise than `Agency name` and takes priority when you set both.

Optional:

-   **Department:** Only returns people in departments matching these words, such as `Public Works`.
-   **Job title:** Only returns people whose job title matches these words, such as `Procurement Director`.
-   **City:** The person's city.
-   **County:** The person's county.
-   **State:** The person's state, by full name, such as `Illinois`.
-   **Number of results:** How many people to return, from 1 to 50. Defaults to 25. People come back ranked by profile completeness, most complete first.

**Outputs**

-   **Number of people returned:** How many people came back.
-   **Total matching people:** How many people match in GovSpend, which can be more than the number returned.
-   **People:** The people found. Each carries:
    -   **Full name**, **First name**, **Middle name**, and **Last name**.
    -   **Job title** and **Department:** The person's role.
    -   **SOC occupation code** and **SOC occupation name:** The person's occupation, such as `11-1011` and `Chief Executives`.
    -   **Is a decision maker:** Whether GovSpend flags the person as a decision-maker.
    -   **Profile completeness:** The person's profile completeness score.
    -   **Contact ID:** GovSpend's ID for the person.
    -   **Record created** and **Record last updated:** When GovSpend added the person's record and when it last changed.
    -   **Address**, **City**, **County**, **State**, **State code**, and **ZIP code:** The address on the person's record.
    -   **Agency name on the contact record** and **Agency type on the contact record:** The agency as written on the person's own record.
    -   **Agency ID**, **Agency name**, **Agency name and state**, **Agency type**, **Level of government**, **Agency city**, **Agency county**, **Agency state**, and **Agency ZIP code:** The agency GovSpend links the person to.

**Note: `Find people` returns names, roles, and locations, not contact details.** To get a person's work email and phone numbers, pass their `Contact ID` to `Enrich person`.

### `Action` Enrich person

Look up a government contact by name or GovSpend contact ID, and get their role, department, agency, and contact details.

**Inputs**

Required — provide one of these:

-   **Person's full name:** The person's full name.
-   **Contact ID:** GovSpend's ID for the person. It returns that exact person and ignores the other inputs.

Optional, and most useful for common names:

-   **Agency name:** The agency the person works for. Distinctive words work best, such as `Broward School` rather than `Broward County School Board`.
-   **Agency ID:** GovSpend's ID for the agency. It's more precise than `Agency name` and takes priority when you set both.
-   **Job title:** The person's job title, such as `Procurement Director`.
-   **Department:** The department the person works in, such as `Public Works`.
-   **City:** The person's city.
-   **State:** The agency's state, by full name, such as `Illinois`.

**Outputs**

-   **Number of matches:** How many people match in GovSpend.
-   **People:** Up to 10 matches, most complete profile first. Each carries:
    -   **Full name**, **First name**, **Middle name**, and **Last name**.
    -   **Job title** and **Department:** The person's role.
    -   **Work email**, **Cell phone**, and **Phone:** The person's contact details.
    -   **Website:** The website on the person's record.
    -   **Address**, **City**, **County**, **State**, **State code**, and **ZIP code:** The address on the person's record.
    -   **SOC occupation code** and **SOC occupation name:** The person's occupation.
    -   **Is a decision maker:** Whether GovSpend flags the person as a decision-maker.
    -   **Profile completeness:** The person's profile completeness score.
    -   **Contact ID** and **Contact details URL:** GovSpend's ID for the person and a link to their record in GovSpend.
    -   **Record created** and **Record last updated:** When GovSpend added the record and when it last changed.
    -   **Agency ID**, **Agency name**, **Agency name and state**, **Agency type**, **Level of government**, and **Agency website:** The agency GovSpend links the person to.

### **Run settings**

-   **Auto-update:** Useful when new rows keep arriving, so each new agency or person is enriched without rerunning the column.
-   **Only run if:** The enrichment will only run if conditions are met. For example, you can run `Get bid document details` only on bids above an `Awarded amount` you choose. ([Learn more about conditional formulas here!](https://www.clay.com/university/lesson/ai-formulas-conditional-runs-clay-101))

## FAQs

### When do GovSpend runs not use data credits?

With your own GovSpend API key connected, runs use no data credits.

Rows where GovSpend finds nothing are refunded in full, so an unmatched agency, person, or bid doesn't cost anything.

### Why are some agency details empty after `Enrich agency` runs?

`Enrich agency` fills in population, employee count, address, phone number, website, county, and level of government only when your inputs match a single agency. When they match several, each result in `Agencies` carries only identifying details, such as its ID, name, type, and city.

To get the full profile, narrow the match with `State`, `City`, or `Agency type`, or run the action again with the right result's `Agency ID`.

### How is `Enrich employee count by criteria` different from `Employee count` on `Enrich agency`?

`Employee count` on `Enrich agency` is the agency's own employee count, alongside the year that figure comes from. `Enrich employee count by criteria` counts the contacts GovSpend has on file for the agency instead, and can narrow that count by job title, department, or occupation.

That makes it a quick way to check how many contacts in a given role, such as procurement, GovSpend has at an agency before you run `Find people` there.
