---
title: Does Clay have an API?
description: Clay doesn't have a traditional API, but you can send data via
  webhooks, wrap Clay with Make or Zapier, use the Enterprise API for people &
  company lookups, or connect AI tools via MCP.
last_synced: 2026-04-26T01:40:52.256Z
---

# Does Clay have an API?

Clay doesn't have a traditional API, but you can send data via webhooks, wrap Clay with Make or Zapier, use the Enterprise API for people & company lookups, or connect AI tools via MCP.

It's one of the most common questions we get — and the honest answer is: not in the traditional sense. Clay isn't built like a typical SaaS tool where you send a request to an endpoint and get data back in milliseconds. Instead, Clay is an enrichment and automation platform designed around tables, workflows, and integrations.

But that doesn't mean you're stuck. Depending on what you're trying to do, there are several ways to interact with Clay programmatically and get results that feel a lot like working with an API. You can pipe data into Clay automatically via webhooks, wrap Clay's functionality using tools like Make or Zapier, connect AI tools like Claude or ChatGPT directly to your Clay workspace via MCP, or — if you have beta access enabled — access Clay's native People and Company API directly.

Below, we'll walk through each approach, when to use it, and how to get started.

**Note:** If you purchase credits from us ("Clay Credits"), you agree not to sell or transfer your Clay Credits to any other user without our prior written approval. You also agree not to re-sell any data you obtain from Clay. [Learn more in our terms of service](https://www.clay.com/terms-of-service#:~:text=4.%20User%20Responsibilities).

### 1\. **Webhooks** (Best for sending data)

Every Clay table has a unique webhook endpoint. You can send data into a table programmatically—say from a form submission, CRM, or another app—and Clay will start processing it immediately.

After enrichments run, you can use Clay's native CRM actions (such as Salesforce's Update Record) or HTTP actions to push the data back out to your system of record. This is the most API-like workflow and is ideal for automating lead flow or enrichment jobs. [Click here for more information about webhooks in Clay!](https://www.clay.com/university/guide/webhook-integration-guide)

Webhook API Workflow in Clay

**Enriching Salesforce leads in real time**

A common use of this pattern is enriching new Salesforce leads or contacts automatically as they are created, without needing to manage Salesforce updates yourself:

1.  **In Clay:** Create a table using **Monitor webhook** as the source. Copy the webhook URL.
2.  **In Salesforce:** Set up a Record-Triggered Flow (`Setup → Flows → New Flow → Record-Triggered Flow`) that fires when a Lead or Contact is created. Add an **HTTP Callout** action that sends a POST request to your Clay webhook URL, with the relevant fields (Lead ID, name, email, company, etc.) as a JSON payload.
3.  **In Clay:** Add enrichment columns to process each incoming record.
4.  **In Clay:** Add an **Update record** Salesforce action column, mapping the enriched fields back to the Salesforce Lead or Contact using the ID from the webhook payload.
5.  **Enable auto-delete** on the webhook table so processed rows are deleted automatically after enrichment completes. This prevents the table from hitting the 50,000-row submission limit and lets it handle new leads continuously.

This is a simpler setup than calling the Clay API directly from Salesforce, because Clay handles the enrichment and writes the data back to Salesforce for you — no custom integration code required.

### 2\. **Wrap Clay in a third-party tool** (Best for light API proxying)

You can use tools like Replit or Make as a wrapper around Clay. These tools receive API requests, trigger Clay to do its thing, and return results once processing is complete.

This works if you absolutely need an endpoint, but be aware: Clay's enrichment model means responses might take a minute or more, and you'll need to build logic to handle that. [Click for a little tutorial on how to do that.](https://www.linkedin.com/posts/horacio-lopez_this-is-probably-the-only-enrichment-api-activity-7224062593689169923-cYg-/)

### 3\. **People & Company Search API** (Best for natural-language lookups)

Clay offers a fast API for searching its proprietary People and Company data. You submit a free-text, natural-language query (along with a `source_type` of `people`, `companies`, or `jobs`), and Clay's AI translates it into search filters and returns matching results.

**Note:** This API is currently in beta. Access is enabled per workspace on request — contact your GTM engineer or [our team](https://www.clay.com/contact-form) to have it enabled for your workspace.

-   It's useful for lightweight lookups and lead enrichment via natural-language search.
-   It doesn't include deep enrichment like emails, phone numbers, or revenue data.
-   **It returns enriched data to the caller — it does not write to Salesforce or any other CRM automatically.** Your system is responsible for taking the response and updating the CRM record. If you want Clay to handle the Salesforce write-back for you, use the webhook workflow described above instead.

[Contact our GTM engineers for more information.](https://www.clay.com/contact-form)

**Note:** If you're using Clay as an API, **Auto-delete** helps keep things fast and lightweight. It automatically enriches incoming webhook data, sends results to your destination (like Salesforce or Google Sheets), then deletes the rows—so Clay streams data through rather than storing it. Perfect for high-volume or continuous enrichment jobs. [Learn more](https://www.clay.com/university/guide/auto-delete).

### 4\. **MCP / AI tool integration** (Best for AI assistants and agent workflows)

If you're using an AI tool like Claude or ChatGPT and want it to run Clay enrichments on your behalf, Clay supports MCP (Model Context Protocol). MCP lets AI assistants look up contacts, enrich data, and invoke custom Clay Functions — without anyone opening Clay directly.

Clay offers pre-built MCP connectors within each supported platform's app or connector directory (Claude, ChatGPT, Copilot, Gemini, Grok, Cursor). See the [MCP settings guide](https://university.clay.com/docs/mcp-settings) for the full list of supported platforms and setup instructions.

**Note:** Clay's MCP endpoint also supports Dynamic Client Registration (DCR), which lets third-party MCP clients not on the pre-built list connect to Clay's MCP server. Connections from unrecognized clients will appear as "Unknown" in OAuth. If you'd like to connect Clay through a third-party agent framework or MCP client via DCR, reach out to [Clay support](https://www.clay.com/contact-form) for the DCR setup guide.
