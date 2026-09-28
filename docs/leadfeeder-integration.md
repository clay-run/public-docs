---
title: Leadfeeder integration
description: How to use the Leadfeeder integration in Clay to search for companies from its European business database, enrich company and contact records, and find people at specific companies.
last_synced: 2026-09-28T16:43:58.591Z
---

# Leadfeeder integration

Use Leadfeeder in Clay to build company lists from its European business database, then enrich those companies and find the right people at them.

Leadfeeder is a website-visitor identification and business data provider with especially deep coverage of companies and contacts across Europe, the Middle East, and Africa. With this integration, you can pull a filtered list of companies into a new Clay table, enrich companies you already have with registry and financial details, and find the contacts you need at a specific company.

## **Creating a table with Leadfeeder**

1.  In a workbook, click `+ Add` at the bottom.
2.  Search for `Leadfeeder` and select `Find companies with Leadfeeder` from the results.

**Note:** `Find companies with Leadfeeder` needs at least one filter before it will run — a search term, a location, an industry, an employee or revenue band, an ICP ID, or one of the data-availability toggles. A preview run returns the first 10 companies no matter how many you have asked for, so you can check that your filters are pointed at the right market before pulling the full list.

### `Source` Find companies with Leadfeeder

Searches Leadfeeder's company database and adds each matching company to your table as a row.

**Inputs**

Multiple values inside one filter are combined with OR, and the location filters combine into every pairing of the values you set — two cities and two countries search all four city-and-country combinations:

-   **Search terms:** Company names, alternative names, trade names, or domains. Multiple values are combined with OR.
-   **Countries:** Countries in which companies are located.
-   **Street addresses:** Full street addresses, for example `Durlacher Allee 73`.
-   **Postal codes:** Postal codes for company locations, for example `76131`.
-   **Cities:** Cities in which companies are located, for example `Karlsruhe`.
-   **Region codes:** Regional codes for company locations — NUTS codes in Europe, and ISO 3166-2 codes with an underscore in place of the hyphen everywhere else.
-   **Industries:** Leadfeeder industries. Multiple industries are combined with OR.
-   **Employee ranges:** Company size bands, from `1–10` up to `10,000+`.
-   **Minimum revenue (EUR)** and **Maximum revenue (EUR)**: The revenue floor and ceiling for the companies you want, in euros.
-   **ICP IDs:** Leadfeeder ideal customer profile IDs.
-   **Filter do not contact companies:** When enabled, returns only companies marked do not contact in Leadfeeder. Left off, results include every company regardless of that status.
-   Each of these toggles keeps only companies where Leadfeeder holds that kind of data:
    -   **Has phone number**
    -   **Has email address**
    -   **Has social profiles**
    -   **Has revenue data**
    -   **Has earnings data**
    -   **Has net worth data**
    -   **Has IP data**
-   **Result limit:** The maximum number of companies to add to the table. Defaults to 1,000 and accepts anything from 1 to 50,000.

**Outputs**

-   **Leadfeeder ID:** Leadfeeder's identifier for the company. This is what `Enrich company` and `Find people at company` take as their input.
-   **Company name:** The company's registered name.
-   **Company URL:** The company's website.
-   **Logo URL:** A link to the company's logo.
-   **City**, **Country**, and **Country code:** Where the company is located.
-   **Industries:** Each industry Leadfeeder assigns the company, with its name and code.
-   **Employee range:** The company's size band.
-   **Revenue:** The company's revenue, with its currency, year, value in that currency, value in euros, and whether the figure is estimated.
-   **Company role:** Leadfeeder's role classification for the company, for example `group`.
-   **Registration status:** The company's status in the commercial register, for example `active`.
-   **Do not contact:** Whether the company is marked do not contact in Leadfeeder.
-   **Has contacts:** Whether Leadfeeder holds contacts for the company, which makes it a useful condition for deciding which rows to send to `Find people at company`.
-   **Leadfeeder group company ID:** The Leadfeeder ID of the group the company belongs to, when it belongs to one.

## **Enriching data with Leadfeeder**

1.  While in a Clay table, click `Add enrichment` and search for `Leadfeeder`.
2.  Under `Integrations`, select one of the Leadfeeder actions.

### `Action` Enrich company

Returns Leadfeeder's full record for a company, matched either from a Leadfeeder company ID or from details you already have in your table.

**Inputs**

Required:

-   **Company identifier:** Whether to match on `Leadfeeder ID` or on `Company details (domain, name, registration or VAT ID)`. The fields underneath change with your choice.

With `Leadfeeder ID` selected:

-   **Leadfeeder company ID:** The Leadfeeder ID of the company to enrich.

With `Company details (domain, name, registration or VAT ID)` selected, at least one of:

-   **Company domain:** The company's domain.
-   **Company name:** The company's name.
-   **VAT ID:** The company's VAT ID, also called its tax ID.
-   **Registration ID:** The company's registration number from the commercial register.

Optional, with `Company details` selected:

-   **Country:** Narrows the match to legal entities in that country, which helps when a company has entities in several. It can't be used on its own. Set one country for the column, or use the gear button to switch the field to `Text with tokens` and map a country in per row.

**Outputs**

-   **Leadfeeder ID:** Leadfeeder's identifier for the matched company.
-   **Match score:** How closely the record matched the details you supplied. Returned when you match on company details.
-   **Type:** The Leadfeeder record type.
-   **Attributes:** The company record itself, including:
    -   **Name**, **Url**, **Alternative Urls**, **Logo Url**, and **App Url:** The company's name and website, any other domains it uses, its logo, and a link to its page in Leadfeeder.
    -   **Address:** Street number, street name, full street address, postal code, city, region, region code, country, country code, and coordinates.
    -   **Employee Count** and **Employee Range:** The company's headcount and size band.
    -   **Revenue:** The company's revenue, with its currency, year, value in that currency, value in euros, and whether the figure is estimated.
    -   **Earnings** and **Net Worth:** Whether Leadfeeder's earnings and net worth figures for the company are estimated.
    -   **Industries:** The company's industries under Leadfeeder's own classification and under the European NACE and German WZ classifications, each with a code and a name.
    -   **Keywords** and **Orientation:** Descriptive keywords for the company and its market orientation, for example `B2B`.
    -   **Register:** The company's commercial-register ID, register location, and registration status.
    -   **Role:** Leadfeeder's role classification for the company, for example `group`.
    -   **Social Media Profiles:** The company's social media profiles, including Facebook, Instagram, YouTube, and others.
    -   **Meta:** Whether the company is marked do not contact, how many contacts Leadfeeder holds for it, and whether its ID has been updated.
    -   **Previous Ids:** Earlier Leadfeeder IDs for the company.
    -   **Custom Fields:** Custom field values Leadfeeder returns for the company.
    -   **Web Engagement** and **Intent:** The web engagement and intent data Leadfeeder holds for the company.
-   **Relationships:** The **Group Company** record, when the company belongs to a group.

### `Action` Enrich contact

Returns the full Leadfeeder record for a single contact — the first match Leadfeeder returns for the identifiers and filters you provide.

**Inputs**

Under `Contact identifier`, at least one of:

-   **Contact name:** The contact name to search for. Supports formula mode.
-   **Email addresses:** Up to 10 email addresses for the contact. Multiple values are combined with OR.
-   **Phone numbers:** Phone numbers for the contact, in international format starting with a `+` and the country code. Multiple values are combined with OR.

Under `Additional filters`, all optional:

-   **Company filter: Leadfeeder company ID:** Limits the search to contacts at one Leadfeeder company.
-   **Positions:** Up to 10 position phrases, such as `CEO` or `Chief Executive Officer`. Multiple values are combined with OR.
-   **Departments:** The departments contacts work in — 19 options, including `Management`, `Sales`, `Engineering`, `Marketing`, `Legal and compliance`, and `Quality management`.
-   **Hierarchy levels:** `Employees`, `Middle management`, or `Top management`.
-   **Affiliation:** How the contact relates to the company — `Employee`, `Group employee`, or `Related`.
-   **Buyer persona IDs:** Leadfeeder buyer persona IDs. Multiple IDs are combined with OR.
-   **Company cities** and **Company countries:** The cities and countries where contacts' companies are located.
-   **Has phone number**, **Has email address**, and **Has social profiles:** Each of these keeps only contacts where Leadfeeder holds that detail.

**Outputs**

-   **ID** and **Type:** Leadfeeder's identifier for the contact and the record type.
-   **Attributes:** The contact record itself, including:
    -   **First name**, **Last name**, **Title**, and **Gender:** The contact's name and personal details.
    -   **Position:** The contact's job title, with the language code it is recorded in.
    -   **Departments** and **Hierarchy level:** Where the contact sits in the company.
    -   **Affiliation:** How the contact relates to the company.
    -   **Emails:** Each email address Leadfeeder holds, with the source it came from.
    -   **Phones:** Each phone number, with its type, for example `mobile`.
    -   **Address:** The contact's city, region, and country.
    -   **Social media profiles:** The contact's professional profile, plus any Facebook, Instagram, YouTube, Pinterest, Xing, and other social profiles.
    -   **Public sources:** Other links Leadfeeder holds for the contact, each with its type.
    -   **Custom fields:** Custom field values Leadfeeder returns for the contact.
-   **Relationships:** The **Company** record for the contact's employer, with the same attributes `Enrich company` returns.

### `Action` Find people at company

Returns people at one Leadfeeder company, with their contact details, narrowed by the filters you set.

**Inputs**

Required, under `Company`:

-   **Leadfeeder company ID:** The Leadfeeder ID of the company you want people from. Both `Find companies with Leadfeeder` and `Enrich company` return this ID.

Optional, under `Contact filters`:

-   **Positions:** Up to 10 position phrases, such as `CEO` or `Chief Executive Officer`.
-   **Departments:** The departments people work in — the same 19 options `Enrich contact` offers.
-   **Hierarchy levels:** `Employees`, `Middle management`, or `Top management`.
-   **Affiliation:** How the person relates to the company — `Employee`, `Group employee`, or `Related`.
-   **Has phone number**, **Has email address**, and **Has social profiles:** Each of these keeps only people where Leadfeeder holds that detail.
-   **Result limit:** The maximum number of people to return. Defaults to 10 and accepts anything from 1 to 500.

**Outputs**

-   **Results:** One entry per person found, each with:
    -   **Id** and **Type:** Leadfeeder's identifier for the person and the record type.
    -   **Attributes:** The person's **First Name**, **Last Name**, **Position**, **Gender**, **Departments**, **Hierarchy Level**, **Affiliation**, and **Address**, along with **Emails** (each with its source), **Phones** (each with its type), **Social Media Profiles** (the person's professional profile), and **Custom Fields**.
    -   **Relationships:** The **Company** record for the person's employer.

### Run settings

-   **Auto-update:** Useful when rows keep arriving, so new companies and people are enriched as they land instead of waiting for you to re-run the column.
-   **Only run if:** The enrichment will only run if conditions are met. ([Learn more about conditional formulas here!](https://www.clay.com/university/lesson/ai-formulas-conditional-runs-clay-101))

## **FAQs**

### Am I charged for rows where Leadfeeder finds nothing?

No. Each of these actions refunds its credits when a search finishes without a match, and the cell shows a message like `No Companies Found`, `No Company Found`, `No Contact Found`, or `No people found`, so those rows are easy to spot and re-run with different inputs.

### Why did `Enrich company` return more than one company?

When you match on company details, Leadfeeder scores every candidate it finds and Clay keeps all of the registered entities tied at the top score. A group with several legal entities under the same name can therefore come back as several records in one cell.

That matters because the action charges per company returned. To narrow it, add a `Country` to the match, or switch `Company identifier` to `Leadfeeder ID` when you already have the ID.

### Should I use `Enrich contact` or `Find people at company`?

Both return Leadfeeder contact records, so the right one depends on what your table already holds:

-   `Enrich contact` returns one contact per row. Reach for it when you know who you are looking for, or when you want to attach a Leadfeeder record to a person already in your table.
-   `Find people at company` returns up to 500 people from one company. Reach for it when you have the company and still need to work out who to talk to there.
