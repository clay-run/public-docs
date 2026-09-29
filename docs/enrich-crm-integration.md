---
title: Enrich CRM integration
description: Enrich contacts, find work emails, enrich company firmographics, funding, French SIRENE data, website technologies, traffic, and homepage content.
last_synced: 2026-09-29T00:00:00.000Z
---

# Enrich CRM integration

Enrich contacts, find work emails, enrich company firmographics, funding, French SIRENE data, website technologies, traffic, and homepage content.

Enrich CRM is a data enrichment provider with broad coverage for contact enrichment, company firmographics, and specialized data for French companies. With this integration you can enrich contact records, find work emails, look up company firmographics and funding history, access French government registry data, and retrieve website technology and traffic data.

## Using Enrich CRM in Clay

1.  While in a Clay table, click `Add enrichment` and search for `Enrich CRM`.
2.  Under `Integrations`, select one of the Enrich CRM actions.
3.  In the modal, you will be asked to `Select Enrich CRM account`.
    -   You can use the Clay-managed Enrich CRM account, or bring your own key.
    -   To bring your own, click `+ Add account` and enter your Enrich CRM API key.

### `Action` Enrich contact

Enriches a contact record using any combination of professional profile URL, Sales Navigator URL/ID, email, name, or company info. Returns up to 200 data points including job history, skills, education, social profiles, and current role details.

**Inputs**

Provide at least one identifier:

-   **Professional profile URL** (e.g. a LinkedIn URL)
-   **Sales Navigator URL or ID**
-   **Email**
-   **Full name** (optionally combined with company name or domain)
-   **Company name** or **Company domain**

### `Action` Reverse email lookup

Given an email address (business or personal, worldwide coverage), returns the matching professional profile with full contact enrichment data.

**Inputs**

-   **Email (Required):** The email address to look up.

### `Action` Find work email

Finds a professional email address given a person's name plus their company name or domain.

**Inputs**

-   **First name** and **Last name**, combined with **Company name** or **Company domain**.

### `Action` Enrich company firmographics

Returns full company firmographic data (industry, size, HQ, locations, social followers, about, slogan) from a domain or company professional profile URL/ID.

**Inputs**

Provide at least one of: **Company domain**, or **Company professional profile URL or ID**.

### `Action` Enrich company latest funding

Returns company financial data: funding rounds, investors, latest valuation, IPO/acquisition history, and employee count.

**Inputs**

Provide at least one of: **Company domain**, or **Company professional profile URL or ID**.

### `Action` Find French SIREN number

Given a French company's domain, name, or professional profile URL/ID, returns its French SIREN registry number.

**Inputs**

Provide at least one of: **Company domain**, **Company name**, or **Company professional profile URL or ID**.

### `Action` Enrich company with French SIRENE

Given a SIREN or SIRET number (or domain/professional profile URL), returns full French government registry data: revenue, employees, financials over multiple years, legal status, establishment details, and geolocation.

**Inputs**

Provide at least one of: **SIREN number**, **SIRET number**, **Company domain**, or **Company professional profile URL or ID**.

### `Action` Enrich website tech stack

Given a domain, returns detected technologies across 20+ categories (advertising, analytics, CMS, frameworks, payments, web servers, eCommerce, and more).

**Inputs**

-   **Company domain (Required):** The website domain to analyze.

### `Action` Enrich monthly website traffic

Given a domain, returns monthly website traffic stats: visits, bounce rate, average time on site, country/global/category rank, top keywords, competitors, and traffic sources.

**Inputs**

-   **Company domain (Required):** The website domain to analyze.

### `Action` Get homepage content

Given a domain, returns the text content of the homepage.

**Inputs**

-   **Company domain (Required):** The website domain whose homepage content to retrieve.
