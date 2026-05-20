---
title: Using Clay in Glean
source_url: https://university.clay.com/docs/using-clay-in-glean
description: Find people, enrich contacts, and draft personalized outreach — all
  within Glean Assistant. Currently in Open Beta for Enterprise plans.
last_synced: 2026-05-20T12:00:00.000Z
---

# Using Clay in Glean

Find people, enrich contacts, and draft personalized outreach — all within Glean Assistant.

**Note: Clay in Glean is currently in Open Beta for Enterprise plans. Contact your Clay account team to enroll.**

Clay in Glean lets you find people, enrich contacts, and draft personalized outreach — all within Glean Assistant. Clay pulls data from a subset of its 150+ providers and AI-powered research agents directly into Glean, so you can move from research to action in seconds.

## Admin setup

Clay in Glean requires two setup steps from admins before reps can use it:

1. **Glean admin:** Connect Clay to your Glean instance through Glean's admin settings. This makes Clay available as an app in Glean Assistant. There is no MCP server URL or OAuth credential from Clay to paste — the connection is configured entirely within Glean's admin panel.
2. **Clay admin:** Enable MCP access for your team from `Settings → MCP users` in Clay. You can also enable specific [Functions](https://university.clay.com/docs/functions) for Glean from the Functions settings page by toggling `Enable for MCP` _(currently in beta — contact your account team if the toggle isn't visible)_, and set per-user credit limits.

Once both steps are complete, reps can start using Clay in Glean immediately.

## Getting started

1. Open **Glean Assistant** by clicking the chat icon in Glean's left navigation, or go to [app.glean.com/chat](https://app.glean.com/chat).
    - *Note: A Glean admin must connect Clay to your Glean instance and a Clay admin must enable access for your team before you can use it. See [Admin setup](#admin-setup) above.*
2. If you haven't already, you'll be prompted to sign into your Clay account.
3. Ask a research question in natural language — Glean will invoke Clay automatically when relevant.
4. Clay will automatically pull the available data and present it in an interactive view. From this view you can:
    - Toggle to view the list of people as a table.
    - Add a filter (e.g., only people in the US or people who have been there for less than 6 months).
    - Enrich the data with different data points (email address, work history summary, thought leadership).
    - Click `View info` next to a person's name to `View on LinkedIn` or `Draft email`.
        - *Note: You'll need to enrich and find a person's email address before you can draft an outreach email.*
5. At any time, you can click `Open in Clay` in the top right corner to unlock more powerful enrichment and workflow capabilities directly in your Clay table.

## Use cases for Clay in Glean

### Research any account

Use Clay to gather deep intelligence on target companies — tech stack, funding, hiring trends, website traffic, and more. Clay pulls from multiple data sources to give you a complete picture of any account.

**Example prompts:**

- `Show me example.com's hiring trends, tech stack, and new product announcements.`
- `Review example.net's latest priorities, leadership changes, and headcount trends.`
- `What's the headcount growth, website traffic, and tech stack of example.org?`

### Find and enrich people at target accounts

Once you've researched an account, Clay can help you find the right people to reach out to. Search by job title, seniority, location, or other criteria, and Clay will enrich each contact with verified emails, phone numbers, work history, and LinkedIn profiles.

**Note:** Today, people search is supported. Company search may be added later.

**Example prompts:**

- `Find VP- and Director-level RevOps leaders at contoso.com who started in the last 9 months.`
- `Find the contact information for example.com's Head of Partnerships.`
- `Who are the engineering leaders at fabrikam.com and what are their emails?`

### Draft personalized outbound

After gathering context on companies and contacts, use Clay to draft personalized emails. Clay uses all the research and enrichment data you've collected to create relevant, context-driven outreach that resonates with your prospects.

**Note:** Email copy is automatically filled with information based on the business context of the Clay workspace you authenticated with. To change this, click `Settings` (gear icon) in the top right and edit directly in Clay.

**Example prompts:**

- `Draft an email to example.com's CPO referencing their AI spend and tech stack.`
- `Write a personalized email to these contacts about how we can help with their recent product launch.`
- `Create outreach for these finance leaders mentioning their company's recent funding round.`

### Run custom functions

If your RevOps team has built enrichment workflows in Clay and enabled them for MCP, you can trigger them directly from Glean Assistant with a single prompt.

**Example prompts:**

- `Run the Clay Outbound Generator for Keith at example.net.`
- `Use the account research function for these three companies.`

## Best practices

To get the best results when using Clay in Glean:

- Include the company domain (e.g., `contoso.com`), not just the company name.
- Limit your search to one company at a time for more accurate results.
- Be specific with criteria: job titles, locations, seniority, keywords.
- If you aren't sure what job title you're looking for, try asking `"who manages X at company"`.
- Use declarative language and keep prompts direct.
- Avoid broad queries or general web searches.

## MCP settings for your team

Workspace admins can set credit limits and monitor rep usage from `Settings → MCP users`. For a full walkthrough of the admin controls, see [MCP settings](https://university.clay.com/docs/mcp-settings).

## FAQ

**Do I need a paid Glean plan?**

Clay in Glean is currently in Open Beta and requires a Clay Enterprise plan. Contact your Clay account team to enroll.

**How do I get set up? Where do I find the MCP server URL or API key?**

Clay in Glean does not use an MCP server URL or OAuth credentials that you paste into Glean. Instead:

1. A Glean admin connects Clay to your Glean instance through Glean's admin settings.
2. A Clay admin enables MCP access from `Settings → MCP users` in Clay.
3. To expose specific workflows, a Clay admin enables them from the Functions settings page and toggles `Enable for MCP` _(currently in beta — contact your account team if the toggle isn't visible)_.

For your Clay API key (used for other Clay integrations, not for the Glean setup), go to your profile picture → `Settings` → `Your Profile` → `API Key`.

**What data sources does Clay use in Glean?**

Clay in Glean pulls from a subset of its 150+ third-party data providers to give you comprehensive coverage across contact data, company intelligence, and web research.

**What data points can Clay enrich?**

Clay can enrich your searches with the following data points:

- Email
- Claygent (including some Claygent templates)
- Revenue
- Funding
- Tech stack
- Website traffic
- Headcount growth
- Open jobs

**Can I search for companies?**

Today, people search is supported. Company search may be added later. You can still research companies by asking Clay questions about target accounts — tech stack, funding, hiring trends, leadership changes, and more.

**What if I need data that isn't available?**

If you need additional data points or more advanced workflows, access the full Clay platform at [app.clay.com](https://app.clay.com) with your same account. Click `Open in Clay` to move your existing table from Glean directly into Clay.

**How does credit usage work?**

Credits are drawn from your organization's Clay plan. Your Clay admin can set default and per-user credit limits from `Settings → MCP users`. Credit spend resets on the 1st of each month at midnight UTC.

**Will this use credits from my account?**

Credits are drawn from your organization's Clay plan. Contact your Clay admin if you have questions about your credit limit.

**How do I enrich contacts with phone numbers?**

Phone number enrichments are available on paid plans. See [pricing](https://www.clay.com/pricing).
