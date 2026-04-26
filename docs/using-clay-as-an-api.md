---
title: Does Clay have an API?
source_url: https://university.clay.com/docs/using-clay-as-an-api
last_synced: 2026-04-26T01:40:52.256Z
upstream_hash: 68043843908de9341f1182cc6cea38cdf9c442881e24f9f4d411a1fb1c665600
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

This works if you absolutely need an endpoint, but be aware: Clay’s enrichment model means responses might take a minute or more, and you’ll need to build logic to handle that. [Click for a little tutorial on how to do that.](https://www.linkedin.com/posts/horacio-lopez_this-is-probably-the-only-enrichment-api-activity-7224062593689169923-cYg-/)

### 3\. **Enterprise-only People & Company API** (Best for basic lookups)

For Enterprise customers, Clay offers a limited but fast API for accessing its proprietary People and Company data. You can send an email or LinkedIn URL to get back basic person details, or a domain to get company info.

-   It’s useful for lightweight lookups and lead enrichment.
-   It doesn’t include deep enrichment like emails, phone numbers, or revenue data.

[Contact our GTM engineers for more information.](https://www.clay.com/contact-form)

**Note:** If you’re using Clay as an API, **Auto-delete** helps keep things fast and lightweight. It automatically enriches incoming webhook data, sends results to your destination (like Salesforce or Google Sheets), then deletes the rows—so Clay streams data through rather than storing it. Perfect for high-volume or continuous enrichment jobs. [Learn more](https://www.clay.com/university/guide/auto-delete).
