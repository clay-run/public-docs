---
title: Does Clay have an API?
source_url: https://university.clay.com/docs/using-clay-as-an-api
description: Clay doesn't have a traditional API, but you can send data via
  webhooks, wrap Clay with Make or Zapier, or use the Enterprise API for people
  & company lookups.
last_synced: 2026-04-26T01:40:52.256Z
---

# Does Clay have an API?

Clay doesn't have a traditional API, but you can send data via webhooks, wrap Clay with Make or Zapier, or use the Enterprise API for people & company lookups.

It's one of the most common questions we get — and the honest answer is: not in the traditional sense. Clay isn't built like a typical SaaS tool where you send a request to an endpoint and get data back in milliseconds. Instead, Clay is an enrichment and automation platform designed around tables, workflows, and integrations.

But that doesn't mean you're stuck. Depending on what you're trying to do, there are several ways to interact with Clay programmatically and get results that feel a lot like working with an API. You can pipe data into Clay automatically via webhooks, wrap Clay's functionality using tools like Make or Zapier, or — if you're on an Enterprise plan — access Clay's native People and Company API directly.

Below, we'll walk through each approach, when to use it, and how to get started.

**Note:** If you purchase credits from us ("Clay Credits"), you agree not to sell or transfer your Clay Credits to any other user without our prior written approval. You also agree not to re-sell any data you obtain from Clay. [Learn more in our terms of service](https://www.clay.com/terms-of-service#:~:text=4.%20User%20Responsibilities).

### 1\. **Webhooks** (Best for sending data)

Every Clay table has a unique webhook endpoint. You can send data into a table programmatically—say from a form submission, CRM, or another app—and Clay will start processing it immediately.

After enrichments run, you can use HTTP actions to push the data back out to your system of record. This is the most API-like workflow and is ideal for automating lead flow or enrichment jobs. [Click here for more information about webhooks in Clay!](https://www.clay.com/university/guide/webhook-integration-guide)

Webhook API Workflow in Clay

### 2\. **Wrap Clay in a third-party tool** (Best for light API proxying)

You can use tools like Replit or Make as a wrapper around Clay. These tools receive API requests, trigger Clay to do its thing, and return results once processing is complete.

This works if you absolutely need an endpoint, but be aware: Clay's enrichment model means responses might take a minute or more, and you'll need to build logic to handle that. [Click for a little tutorial on how to do that.](https://www.linkedin.com/posts/horacio-lopez_this-is-probably-the-only-enrichment-api-activity-7224062593689169923-cYg-/)

### 3\. **Enterprise-only People & Company API** (Best for basic lookups)

For Enterprise customers, Clay offers a limited but fast API for accessing its proprietary People and Company data.

**Endpoint:** `POST https://api.clay.com/v3/actions/run-enrichment`

**Auth:** Pass your Clay API key in the `Authorization` header. You can find your key under Settings → Account → Your profile → API key.

The API supports two enrichment types:

-   **Person lookup** (`enrichmentType: "enrich-person"`) — submit a known email address or LinkedIn URL to get back basic profile details.
-   **Company lookup** (`enrichmentType: "enrich-company"`) — submit a company domain to get back basic company info.

**Important:** This API is designed for point lookups on identifiers you already have — it does not support searching by keyword, job title, location, industry, or other criteria. Endpoints like `/v3/contacts/search` do not exist and will return a 404 error.

**Limitations:**

-   It doesn't include deep enrichment like emails, phone numbers, or revenue data.
-   Available to Enterprise plan customers only — requests from non-Enterprise workspaces return a 403 error.

**If you want to discover and filter people by criteria** (job title, company, location, industry): use Clay's [Find People](find-people-overview.md) source directly in the platform instead. Find People supports rich filters — job title, organizational level, company attributes, location, and more — and you can sync results to Google Sheets or any other destination via Clay's native integrations.

[Contact our GTM engineers for more information.](https://www.clay.com/contact-form)

**Note:** If you're using Clay as an API, **Auto-delete** helps keep things fast and lightweight. It automatically enriches incoming webhook data, sends results to your destination (like Salesforce or Google Sheets), then deletes the rows—so Clay streams data through rather than storing it. Perfect for high-volume or continuous enrichment jobs. [Learn more](https://www.clay.com/university/guide/auto-delete).
