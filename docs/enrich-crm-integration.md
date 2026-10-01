---
title: Enrich CRM integration
description: Enrich contacts and companies with firmographics, funding, tech stack, traffic, and more.
last_synced: 2026-09-29T15:00:00.000Z
---

# Enrich CRM integration

Enrich contacts and companies with firmographics, funding, tech stack, traffic, and more.

Enrich CRM is a multi-signal enrichment provider with broad worldwide coverage, including deep data for French companies via official SIRENE registry data. The integration covers company firmographics, funding history, technology stack, website traffic, contact enrichment, email finding, and reverse email lookup — all from a single provider account.

## Enriching data with Enrich CRM

1.  While in a Clay table, click `Add enrichment` and search for `Enrich CRM`.
2.  Under `Integrations`, select one of the Enrich CRM options.
3.  In the modal, you will be asked to `Select Enrich CRM account`.
    -   You can run these actions on Clay's shared Enrich CRM account, or bring your own key.
    -   To bring your own, click `+ Add account` and enter your Enrich CRM API key.

### `Action` Enrich company firmographics

Returns full company firmographic data — industry, size, HQ, locations, social followers, about, and slogan — from a domain or company professional profile URL/ID.

**Inputs**

One of the following is required: company domain or company professional profile URL/ID.

| Input | Required | Description |
|-------|----------|-------------|
| **Company domain** | Conditional | Company domain, like clay.com. |
| **Company professional URL** | Conditional | Company professional profile URL. |
| **Company professional ID** | Conditional | Numeric company professional ID. |
| **Company Sales Navigator URL** | Optional | Company Sales Navigator URL. |
| **Company Sales Navigator ID** | Optional | Numeric company Sales Navigator ID. |

### `Action` Enrich company latest funding

Returns company financial data: funding rounds, investors, latest valuation, IPO/acquisition history, and employee count.

**Inputs:** Same company identifiers as Enrich company firmographics.

### `Action` Enrich website tech stack

Given a domain, returns detected technologies across 20+ categories (advertising, analytics, CMS, frameworks, payments, web servers, eCommerce, and more).

**Inputs**

| Input | Required | Description |
|-------|----------|-------------|
| **Company domain** | Required | Company domain, like clay.com. |

### `Action` Enrich monthly website traffic

Given a domain, returns monthly website traffic stats: visits, bounce rate, avg time on site, country/global/category rank, top keywords, competitors, and traffic sources.

**Inputs**

| Input | Required | Description |
|-------|----------|-------------|
| **Company domain** | Required | Company domain, like clay.com. |

### `Action` Get homepage content

Given a domain, returns the text content of the homepage. Useful as input for AI-based personalization or company summarization columns.

**Inputs**

| Input | Required | Description |
|-------|----------|-------------|
| **Company domain** | Required | Company domain, like clay.com. |

### `Action` Enrich contact

Enriches a contact record using any combination of professional profile URL, Sales Navigator URL/ID, email, name, or company info. Returns up to 200 data points including job history, skills, education, social profiles, and current role details.

**Inputs**

One of the following is required: professional profile URL, email, or name with company info.

| Input | Required | Description |
|-------|----------|-------------|
| **Professional profile URL** | Conditional | Person's professional profile URL. |
| **Sales Navigator URL** | Conditional | Person's Sales Navigator URL. |
| **Sales Navigator ID** | Conditional | Numeric Sales Navigator ID. |
| **Email** | Conditional | Person's email address. |
| **First name** | Conditional | Person's first name. Use with last name and company info. |
| **Last name** | Conditional | Person's last name. |
| **Company domain** | Optional | Company domain for name-based matching. |
| **Company name** | Optional | Company name for name-based matching. |

### `Action` Find work email

Finds a professional email address given a person's name plus their company name or domain.

**Inputs**

| Input | Required | Description |
|-------|----------|-------------|
| **First name** | Required | Person's first name. |
| **Last name** | Required | Person's last name. |
| **Company domain** | Conditional | Company domain. Required if company name isn't provided. |
| **Company name** | Conditional | Company name. Required if company domain isn't provided. |

### `Action` Reverse email lookup

Given an email address — business or personal, with worldwide coverage — returns the matching professional profile with full contact enrichment data.

**Inputs**

| Input | Required | Description |
|-------|----------|-------------|
| **Email** | Required | The email address to look up. |

### `Action` Find French SIREN number

Given a French company's domain, name, or professional profile URL/ID, returns its French SIREN registry number.

**Inputs:** Domain, company name, professional URL, or professional ID (at least one required).

### `Action` Enrich company with French SIRENE

Given a SIREN or SIRET number (or domain/professional profile URL), returns full French government registry data: revenue, employees, financials over multiple years, legal status, establishment details, and geolocation.

**Inputs**

| Input | Required | Description |
|-------|----------|-------------|
| **SIREN number** | Conditional | 9-digit SIREN number. |
| **SIRET number** | Conditional | 14-digit SIRET number. |
| **Company domain** | Conditional | Company domain. |
| **Professional profile URL** | Conditional | Company professional profile URL. |
