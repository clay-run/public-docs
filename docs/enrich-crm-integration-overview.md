---
title: Enrich CRM integration
description: How to use Enrich CRM in Clay to enrich contacts and companies with work email verification, firmographics, funding history, website traffic, tech stack, and French business registry data.
last_synced: 2026-09-24T19:36:22.703Z
---

# Enrich CRM integration

Use Enrich CRM in Clay to enrich people and companies, find and verify work emails, and add website traffic, technology, funding, and French business registry data to your tables.

Enrich CRM is a data provider that covers both people and companies, from contact profiles and work emails through to firmographics, funding history, website traffic, detected technologies, and the French national business register. With this integration, you can run ten enrichments against the rows already in your Clay tables, each one taking whichever identifier you happen to have — a domain, a company name, an email address, or a professional profile URL.

## Enriching data with Enrich CRM

1.  While in a Clay table, click `Add enrichment` and search for `Enrich CRM`.
2.  Under `Integrations`, select one of the Enrich CRM actions.
3.  In the modal, you will be asked to `Select Enrich CRM account`.
    -   If you have your own Enrich CRM account, click `+ Add account` and enter your `Enrich CRM API Key`. Otherwise, use the Clay provided key.

**Note:** `Enrich contact` and `Reverse email lookup` search Enrich CRM's underlying sources while the action runs, so a row can take anywhere from a few seconds to around two minutes — rows with no match take the longest, because the search runs all the way to the end before giving up. Clay keeps checking for the result in the background, so you don't need to stay on the table.

### `Action` Enrich contact

Builds a full profile for a person from whichever identifier you already have.

**Inputs**

Required — under `Person identifiers`, at least one of:

-   **Person's professional URL:** The person's professional profile URL.
-   **Person's Sales Navigator URL:** The person's Sales Navigator profile URL.
-   **Person's Sales Navigator ID:** The person's numerical Sales Navigator profile ID.
-   **Person's email address:** The person's professional or personal email address.
-   **Person's full name:** The person's full name.
-   **Person's first name** and **Person's last name:** Use these two together when you don't have a full name.

Optional — under `Company information`. None of these are needed on their own, but each one helps Enrich CRM pick the right person when you're matching on a name:

-   **Company domain:** The domain of the person's company, like `clay.com`.
-   **Company name:** The name of the person's company.
-   **Company professional URL:** The company's professional profile URL.
-   **Company Sales Navigator URL:** The company's Sales Navigator URL.
-   **Company professional ID:** The numerical company profile ID.
-   **Company Sales Navigator ID:** The numerical company Sales Navigator ID.

**Outputs**

-   **Identity:**
    -   Full name, First name, Last name
    -   Headline, Profile summary, Profile photo
    -   Professional profile URL, Professional profile ID, Sales Navigator URL
    -   Personal website, Social profile URL, Followers
    -   Confidence score, Enrich CRM's own score for how sure it is of the match
-   **Current role:**
    -   Role, Seniority
    -   Current company name, Current company website
    -   Current companies, with the full detail Enrich CRM holds on each one
-   **Work history:**
    -   Past companies, Previous company name
    -   Years of experience
-   **Background:**
    -   Skills, Languages, Certifications
    -   Education, broken out into Universities, Diplomas, Fields of study, and Year of last diploma
-   **Location:** Location, City, Country

### `Action` Reverse email lookup

Finds the person behind an email address, business or personal, with worldwide coverage.

**Inputs**

Required:

-   **Person's email address:** The address you want a profile for.

Optional, and each one helps Enrich CRM confirm it has the right person:

-   **Person's full name:** The person's full name.
-   **Person's first name:** The person's first name.
-   **Person's last name:** The person's last name.

**Outputs**

This action returns the same profile fields as `Enrich contact` — identity, current role, work history, background, and location.

### `Action` Find work email

Finds a professional email address from a person's name plus their company, and reports how deliverable it looks.

**Inputs**

Required — under `Person identifiers`, either:

-   **Person's full name:** The person's full name.
-   **Person's first name** and **Person's last name:** Use these two together when you don't have a full name.

Required — under `Company identifiers`, at least one of:

-   **Company domain:** The domain of the person's company, like `clay.com`.
-   **Company name:** The name of the person's company.

**Outputs**

-   **Work email:** The address Enrich CRM found (e.g., `sylvain@enrich-crm.com`).
-   **Email status:** Enrich CRM's verdict on that address (e.g., `Valid`).
-   **Email domain:** The domain the address sits on.
-   **MX record found:** Whether the domain is set up to receive mail at all.
-   **MX record:** The mail server the domain points at (e.g., `aspmx.l.google.com`).
-   **SMTP check passed:** Whether the mail server accepted the address when Enrich CRM tested it.
-   **SMTP provider:** Who hosts the mailbox (e.g., `google`).
-   **Catch-all domain:** Whether the domain accepts mail at any address. A catch-all domain makes a single verification less conclusive, so treat those addresses with more care.
-   **Alternate email:** A second address for the same person, when Enrich CRM has one.
-   **Most probable emails:** The addresses most likely to reach this person, in order.
-   **Email patterns:** The address formats in use at the company (e.g., `{first}@{domain}`), which you can apply to other people there.
-   **Deliverability flags:** Anything that affected the check (e.g., `greylisted`).
-   **Explanation:** A short note on how the result was reached (e.g., `Mailbox verified via SMTP.`).

### `Action` Enrich company firmographics

Returns a company's core profile: what it does, how big it is, and where it operates.

**Inputs**

Required — under `Company identifiers`, at least one of:

-   **Company domain:** The company's domain, like `clay.com`.
-   **Company name:** The company's name.
-   **Company professional URL:** The company's professional profile URL. Of the six identifiers, this one matches the most reliably.
-   **Company Sales Navigator URL:** The company's Sales Navigator URL.
-   **Company professional ID:** The numerical company profile ID.
-   **Company Sales Navigator ID:** The numerical company Sales Navigator ID.

**Outputs**

-   **Identity:**
    -   Company name, Company website, Company logo
    -   Company professional URL, Company professional ID, Crunchbase URL
    -   Slogan, About us
-   **Classification:** Industry, HubSpot industry, Specialties, Company type
-   **Size and age:**
    -   Company size, as a headcount range (e.g., `2-10`)
    -   Employee count, Social followers, Founded
-   **Location:**
    -   Headquarters location, city, state, country, postal code, and phone number
    -   Country code
    -   Number of locations
    -   Locations, with Street, City, State, Postal code, Description, and Is headquarters for each site

### `Action` Enrich company latest funding

Returns a company's funding history and financial position.

**Inputs**

Required — under `Company identifiers`, at least one of:

-   **Company domain:** The company's domain, like `clay.com`.
-   **Company name:** The company's name.
-   **Company professional URL:** The company's professional profile URL.
-   **Company Sales Navigator URL:** The company's Sales Navigator URL.
-   **Company professional ID:** The numerical company profile ID.
-   **Company Sales Navigator ID:** The numerical company Sales Navigator ID.

**Outputs**

-   **Company basics:**
    -   Company name, Description, Company website, Company domain
    -   Founded on, Operating status, Employee count range
    -   Headquarters location, Contact email, Crunchbase URL
    -   Categories, Founders
-   **Funding:**
    -   Total funding in USD, Number of funding rounds
    -   Last funding type, Latest funding date, Last funding amount in USD
    -   Number of investors, Investors
-   **Public markets and acquisitions:**
    -   IPO status, Stock symbol, Stock exchange, Went public on, IPO valuation
    -   Acquisition status, Number of acquisitions
-   **Revenue metrics:** Enrich CRM's revenue estimate for the company (e.g., `Estimated revenue $1B+`).

### `Action` Enrich monthly website traffic

Returns a month of traffic data for a website, along with where the visitors came from.

**Inputs**

Required — under `Website identifiers`, at least one of:

-   **Company domain:** The domain of the website to look up, like `clay.com`.
-   **Company professional URL:** The company's professional profile URL.
-   **Company Sales Navigator URL:** The company's Sales Navigator URL.
-   **Company professional ID:** The numerical company profile ID.
-   **Company Sales Navigator ID:** The numerical company Sales Navigator ID.

**Outputs**

-   **Engagement:**
    -   Monthly visits, Bounce rate, Pages per visit, Average time on site
    -   Month and Year, so you know which period the figures cover
-   **Trend:** Estimated monthly visits, a Month-and-Visits pair for each month in the series.
-   **Ranking:** Global rank, Country rank, Country code, Category rank, Category
-   **Traffic sources**, as a share for each channel: Direct, Referrals, Search organic, Search paid, Social organic, Social paid, Mail, Display ads, Generative AI, Affiliate
-   **Keywords:** Top keywords, each with Keyword, Search volume, Estimated value, and Cost per click.
-   **Site details:** Website title, Website description, Snapshot date

### `Action` Enrich website tech stack

Scans a website and returns the technologies running on it.

**Inputs**

Required:

-   **Company domain:** The domain of the website to scan for technologies, like `clay.com`.

**Outputs**

-   **Technologies detected on website:** Every technology found, as a list.
-   **Technologies found:** The same technologies as one comma-separated string (e.g., `Global Site Tag, CloudFront, HubSpot CMS, DMARC, AWS Route 53`), which is the easier one to read in a cell or feed into a formula.
-   **Number of technologies detected on website:** How many were found.
-   **Technologies by category:** The same technologies grouped by Category, so you can filter on a category that matters to you, like `Analytics and Tracking`.
-   **Snapshot date:** When the scan data is from.

### `Action` Get homepage content

Returns the text of a company's homepage.

**Inputs**

Required — under `Website identifiers`, at least one of:

-   **Company domain:** The domain of the website to look up, like `clay.com`.
-   **Company professional URL:** The company's professional profile URL.
-   **Company Sales Navigator URL:** The company's Sales Navigator URL.
-   **Company professional ID:** The numerical company profile ID.
-   **Company Sales Navigator ID:** The numerical company Sales Navigator ID.

**Outputs**

-   **Homepage content:** The text on the company's homepage. It's a useful starting point for Claygent, Clay's AI research agent, or for an AI formula that needs to read how a company describes itself.

### `Action` Find French SIREN number

Looks up a French company's SIREN number — the nine-digit number the French government assigns to every registered business — from the identifiers you already hold.

**Inputs**

Required — under `Company identifiers`, at least one of:

-   **Company domain:** The company's domain, like `clay.com`.
-   **Company name:** The company's name.
-   **Company professional URL:** The company's professional profile URL.
-   **Company Sales Navigator URL:** The company's Sales Navigator URL.
-   **Company professional ID:** The numerical company profile ID.
-   **Company Sales Navigator ID:** The numerical company Sales Navigator ID.

**Outputs**

-   **SIREN:** The company's SIREN number (e.g., `932510217`).
-   **Company name:** The registered name Enrich CRM matched.

### `Action` Enrich company with French SIRENE

Returns a French company's entry in SIRENE, the French government's register of businesses and their establishments.

**Inputs**

Required — under `French registry identifiers`, at least one of:

-   **SIREN:** The French SIREN registry number, which identifies the legal entity (e.g., `932510217`).
-   **SIRET:** The French SIRET number, which identifies one specific site of that entity — a head office, a branch, a factory (e.g., `93251021700015`).
-   **Company domain:** The company's domain, like `clay.com`.
-   **Company professional URL:** The company's professional profile URL.
-   **Company Sales Navigator URL:** The company's Sales Navigator URL.
-   **Company professional ID:** The numerical company profile ID.
-   **Company Sales Navigator ID:** The numerical company Sales Navigator ID.

**Outputs**

-   **Registry identifiers:**
    -   SIREN, SIRET, VAT number
    -   NAF code (e.g., `70.22Z`) and NAF label, the French classification of what the business does
    -   Activity domain, a broader description of the same thing
-   **Company details:**
    -   Company name, Legal name
    -   Legal form (e.g., `SAS, société par actions simplifiée`)
    -   Company category, the French size bracket the business falls into (e.g., `PME` for a small or mid-sized business)
    -   Administrative status, Company ceased, Created on, Headcount
-   **Financials:** Financials, with the figures filed for each year, and Representatives, the people registered as running the business.
-   **Address:** Address, Postal code, City, Department, Region, Latitude, Longitude

### Run settings

-   **Auto-update:** Useful when rows keep arriving, so new people and companies are enriched as they land instead of waiting for you to re-run the column.
-   **Only run if:** The enrichment will only run if conditions are met. ([Learn more about conditional formulas here!](https://www.clay.com/university/lesson/ai-formulas-conditional-runs-clay-101))

## FAQs

### How fresh is the data each action returns?

Four actions run a fresh search every time: `Enrich contact`, `Reverse email lookup`, `Find work email`, and `Get homepage content`.

The other six reuse a recent result when you run the same input again, rather than fetching it a second time:

-   Up to 30 days for `Enrich company firmographics`, `Find French SIREN number`, and `Enrich company with French SIRENE`.
-   Until the end of the calendar month for `Enrich company latest funding`, `Enrich monthly website traffic`, and `Enrich website tech stack`.

### Am I charged for rows that come back empty?

No. When an action finishes without finding anything, Clay refunds the credits for that row, and the cell shows a short message like `❌ Contact not found` or `❌ Technologies not found` so those rows are easy to spot and re-run later.

### Why did `Enrich website tech stack` come back empty for a site that loads fine?

When there's no recent result to reuse, Enrich CRM scans the site live to detect its technologies — and a scan that can't reach the site is returned as no data rather than as an error.

Clay treats that as the final answer for the row, because the usual cause is a domain that's dead or unreachable rather than a site that was briefly slow. Check the value in your input column before you re-run, since a re-run against the same unreachable domain comes back the same way.

### What happens if my own Enrich CRM account runs low on credits?

When you connect your API key, Clay checks the credit balance on your Enrich CRM account and reports it back to you. You'll get a warning if you're down to 100 credits or fewer, and a clearer one if you've run out.

Rows that run against an empty account come back with an out-of-credits message, so top up in Enrich CRM and re-run the column. If you'd rather not manage a separate balance, use the Clay provided key instead.

### Which identifier should I map for the company actions?

Map more than one where you have them. Each company action accepts several alternatives and only needs one, so a column mapped to both `Company domain` and `Company professional URL` still has something to work with on rows where one of the two is blank.
