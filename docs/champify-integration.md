---
title: Champify integration
source_url: https://university.clay.com/docs/champify-integration
description: Find potential sales champions.
last_synced: 2026-04-27T18:09:33.390Z
upstream_hash: 05d65ab07fb463f350cff0ca9c184560ba64253d8405c1d927f526f7e4b57ea8
---

# Champify integration

Find potential sales champions.

Champify is a digital champion management tool for sales teams. With this integration, you can find professional profiles for people and companies to identify and engage potential sales champions within target accounts.

## Enriching data with Champify

1.  While in a Clay table, click `Add enrichment` and search for `Champify`.
2.  Under `Integrations`, select one of the Champify options.

### `Action` Find professional profile URL

Use this action to find a person's professional profile URL from their name and company information.

**Inputs**

One of the following input combinations is required:

-   **Email:** A work or personal email address (e.g., `john.doe@clay.com`).
-   **Full name + Company name:** The person's full name (e.g., `John Doe`) and the name of a current or past company (e.g., `Clay`).
-   **Full name + Company domain:** The person's full name (e.g., `John Doe`) and the company's website or domain (e.g., `clay.com`).

Optional:

-   **Job title:** The person's title at the company (e.g., `Software Engineer`).

**Outputs**

-   **Professional profile URL:** The person's LinkedIn profile URL (e.g., `https://www.linkedin.com/in/johndoe`).

### `Action` Find company professional profile

Use this action to find a company's LinkedIn profile page from their name and website domain.

**Inputs**

Required:

-   **Company name:** The company name (e.g., `Clay`).
-   **Company domain:** The company website or domain (e.g., `clay.com`).

**Outputs**

-   **Company profile URL:** The company's LinkedIn profile URL (e.g., `https://www.linkedin.com/company/clay`).
