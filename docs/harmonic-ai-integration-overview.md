---
title: Harmonic.ai integration overview
description: Platform for discovering startups with real-time data, network
  insights, and alerts.
last_synced: 2026-04-26T01:40:06.717Z
---

# Harmonic.ai integration overview

Platform for discovering startups with real-time data, network insights, and alerts.

## Harmonic.ai Overview

The Harmonic.ai integration in Clay allows users to access in-depth company data and fundraising information, providing insights into a company's industry, location, funding history, and technology stack. This tool is essential for market research, competitor analysis, and lead enrichment within Clay workflows.

## Setting up Harmonic.ai and Clay

You can connect and utilize Harmonic.ai enrichments in two ways.

1.  **Clay-managed account**: Use Clay Credits to pay for enrichments using the credits available in your Clay account.
2.  **(Available to paid Clay users) Harmonic.ai account via API key**: Use your Harmonic.ai account credits by integrating your API key directly into Clay.

## **Available Actions with the Harmonic.ai Integration**

### `Action` **Get Fundraising Data for Company**

Use this action to retrieve detailed fundraising information for a company based on its domain or LinkedIn URL.

**Setup Inputs**

-   **Company Domain or Company LinkedIn URL**: Enter the company's domain (e.g., clay.com) or LinkedIn URL (e.g., https://www.linkedin.com/company/clay-run/) to fetch relevant fundraising data.

### `Action` **Enrich Company**

Use this action to access a company's detailed information, including technology stack, based on its domain.

**Setup Inputs**

-   **Company Domain**: Enter the domain of the company (e.g., clay.com) to enrich the company profile with comprehensive data, including technologies used.

## Troubleshooting Harmonic.ai enrichment errors

### "Company not found; scheduled for enrichment"

When Harmonic.ai hasn't yet indexed a company in its database, it returns the message: *"Company not found; scheduled for enrichment, check back in a few hours."* This is a transient status — Harmonic has queued the company for background enrichment and may return data when the row is re-run a few hours later.

Harmonic's `/enrichment_status` endpoint is not available as a Clay action, so there is no way to poll for the enrichment status or check when the data will be ready from within a Clay table or workflow.

### Harmonic enrichment error types

Harmonic enrichment errors fall into three categories:

-   **Transient — retry later**: *"Company not found; scheduled for enrichment"* — the company isn't in Harmonic's index yet. Re-running the row a few hours later may succeed.
-   **Hard failure — fix the input**: Missing or invalid domain — the enrichment cannot run without a valid company domain. Re-running won't help until the domain is corrected first.
-   **Provider error**: Other errors returned by Harmonic's API. These are less common and may resolve on retry.

### Handling "company not found" errors

The built-in retry setting runs within seconds, which is too fast for Harmonic's background enrichment process (which can take several hours). The recommended approach:

1.  **Filter out blank or invalid domains before the Harmonic step.** Use a conditional to skip rows where the company domain is missing or invalid. This prevents hard failures from blocking downstream steps.
2.  **Re-run affected rows after a few hours.** Filter your table or workflow for rows where Harmonic returned no data or a "company not found" error, then re-run them once Harmonic has had time to complete the enrichment.
