---
title: Using Clay in Glean
description: How to find people, enrich contacts, and draft personalized outreach using Clay within Glean Assistant.
last_synced: 2026-07-13T21:39:14.719Z
---

# Using Clay in Glean

Find people, enrich contacts, and draft personalized outreach — all within Glean Assistant.

Glean is an enterprise AI search and assistant platform for workplace knowledge. With this integration, you can find people, enrich contacts, and draft personalized outreach — all within Glean Assistant.

**Note:** A Glean admin must connect Clay to your Glean instance through Glean's MCP apps directory before you can use it. A Clay admin must also enable access for your team from Clay's [MCP settings page](https://university.clay.com/docs/mcp-settings).

## **Getting started**

1.  Open Glean Assistant by clicking the chat icon in Glean's left navigation, or go to `app.glean.com/chat`.
2.  If you haven't already, you'll be prompted to sign into your Clay account.
3.  Ask a research question in natural language — Glean will invoke Clay automatically when relevant.
4.  Clay will automatically pull the available data and present it in an interactive view. From this view you can:
    -   Toggle to view the list of people as a table
    -   Add filters (e.g., only people in the US or people who have been there for less than 6 months)
    -   Enrich contacts with additional data points (email address, work history summary, thought leadership)
    -   Click `View info` next to a person's name to `View on LinkedIn` or `Draft email`
        -   **Note:** You'll need to enrich and find a person's email address before you can draft an outreach email.
5.  Results are returned in groups of 20. Click `Load more` to see additional pages — up to 100 results total.
6.  At any time, click `Open in Clay` in the top right corner to unlock more powerful enrichment and workflow capabilities directly in your Clay table.

## **Use cases for Clay in Glean**

### **Find and enrich people at target accounts**

Once you've researched an account, Clay helps you find the right people to reach out to. Search by job title, seniority, location, or other criteria, and Clay will enrich each contact with verified emails, phone numbers, work history, and professional profiles.

**Example prompts:**

-   `Find VP-level RevOps leaders at [Company] who started in the last 9 months.`
-   `Find the contact information for [Company]'s Head of Partnerships.`
-   `Find enterprise software companies in the Midwest with 200–1,000 employees.`

### **Research any account**

Use Clay to gather deep intelligence on target companies — tech stack, funding, hiring trends, website traffic, and more. Clay pulls from multiple data sources to give you a complete picture of any account.

**Example prompts:**

-   `What are [Company]'s top go-to-market priorities this year? Any recent executive changes or expansion signals?`
-   `What new markets has [Company] expanded into recently? How has headcount changed over the last year?`
-   `What's the tech stack and hiring trend at [Company] over the last 6 months?`

### **Draft personalized outbound**

After gathering context on companies and contacts, use Clay to draft personalized emails based on the research you've collected.

**Example prompts:**

-   `Write an email referencing [Company]'s recent product launches and their VP of Engineering's comments on developer productivity, under 130 words.`
-   `Draft a personalized email to [Company]'s Head of Partnerships about their partnership priorities and key themes from their recent public posts.`
-   `Create outreach for finance leaders at [Company] mentioning their recent executive changes and expansion signals.`

## **Running functions**

If your ops team has built Clay Functions, you can invoke them directly from Glean with a single prompt. Functions are pre-built enrichment workflows — like ICP scoring, outbound sequence generation, or account research waterfalls — that your ops team configures once in Clay and enables for your entire team.

To see which functions are available to you, ask:

-   `What functions do you have?`
-   `What workflows has RevOps built for me?`

To run a function, reference it by name:

-   `Run Clay outbound generator for sarah@acme.com`

Glean will find the matching function, run it, and return the results directly in your conversation.

## **Best practices**

To get the best results when using Clay in Glean:

-   Include the company domain (e.g., `contoso.com`), not just the company name
-   Be specific with criteria: job titles, locations, seniority, keywords
-   If you aren't sure what job title you're looking for, try asking "who manages X at company"
-   Use declarative language and keep prompts direct
-   Avoid broad queries or general web searches

## **FAQ**

**What data sources does Clay use in Glean?**

Clay in Glean pulls from a subset of its 200+ third-party data providers to provide comprehensive coverage across contact data, company intelligence, and web research. If you want to enable additional enrichments, your ops team can add a Function for them and enable it for MCP.

**Can I search for companies?**

Yes — you can search for companies by criteria like location, headcount, and industry. For example: `Find enterprise software companies in the Midwest with 200–1,000 employees.` You can also research any company by asking Clay about it directly — tech stack, funding, hiring trends, leadership changes, and more.

**What if I need data that isn't available?**

If you need additional data points or more advanced workflows, access the full Clay platform at [**app.clay.com**](http://app.clay.com/) with your same account to unlock more powerful enrichment and workflow capabilities.

**How do credits work in Glean?**

Credits are consumed at the same rate as using Clay directly. Searching for people and companies is free; enriching a contact (finding an email, phone number, etc.) consumes credits. Your workspace admin controls your credit limit from `Settings → MCP users`.

**Does my Glean admin need to do anything to set this up?**

Yes — a Glean workspace admin must first connect Clay through Glean's MCP apps directory. Once connected at the Glean level, a Clay admin also needs to enable MCP access and configure which Functions are available. Individual reps don't need to configure anything beyond signing into their Clay account.
