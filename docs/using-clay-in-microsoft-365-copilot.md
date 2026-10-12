---
title: Using Clay in Microsoft 365 Copilot
description: How to find people, enrich contacts, and draft personalized outreach using the Clay agent inside Microsoft 365 Copilot.
last_synced: 2026-07-13T21:15:59.405Z
---

# Using Clay in Microsoft 365 Copilot

Find people, enrich contacts, and draft personalized outreach — all within Microsoft 365 Copilot.

Microsoft 365 Copilot is an AI assistant embedded across Microsoft's productivity suite — Teams, Outlook, Word, and more. With this integration, you can find people, enrich contacts, and draft personalized outreach without leaving the tools your team already works in.

**Note:** A Microsoft 365 admin must install the Clay agent for your organization before reps can use it. A Clay admin must also enable access for your team from Clay's [MCP settings page](https://university.clay.com/docs/mcp-settings).

## **Getting started**

**For admins:**

1.  Go to the [**Clay listing in the Microsoft Marketplace**](https://marketplace.microsoft.com/en-us/product/WA200011257) and click **Get it now**, or find Clay in the **Agent Store** inside Microsoft 365 Copilot at [**aka.ms/m365\_copilot\_app**](https://aka.ms/m365_copilot_app).
2.  Deploy the Clay agent to your organization through the [**Microsoft 365 Admin Center**](https://admin.microsoft.com/). IT controls deployment, access, and governance from there.
3.  In your Clay workspace, go to `Settings → Team` and invite reps. Then set credit limits from `Settings → MCP users`, and enable any Functions you want them to use from the `Functions` tab.

**For reps:**

1.  Open Microsoft 365 Copilot — in Teams, at [**m365.cloud.microsoft/chat**](https://m365.cloud.microsoft/chat), or in any M365 app with Microsoft 365 Copilot enabled.
2.  If you haven't already connected Clay, you'll be prompted to sign into your Clay account.
3.  Ask a research question in natural language — Microsoft 365 Copilot will invoke Clay automatically when relevant.
4.  Clay will pull the available data and present it in an interactive view where you can:
    -   Toggle between **People** and **Company** views
    -   Add filters (e.g., only people in the US or people who joined in the last 6 months)
    -   Enrich contacts with additional data points (email address, work history summary, thought leadership)
    -   Click `View info` next to a person's name for more details or `Draft email`
        -   **Note:** You'll need to enrich and find a person's email address before you can draft an outreach email.
5.  Results are returned in groups of 20. Click `View 10 more` to see additional results — up to 100 total.
6.  At any time, click `Open` in the top right of the widget to unlock more powerful enrichment and workflow capabilities directly in your Clay table.

## **Use cases for Clay in Microsoft 365 Copilot**

### **Find and enrich people at target accounts**

Once you've researched an account, Clay helps you find the right people to reach out to. Search by job title, seniority, location, or other criteria, and Clay will enrich each contact with verified emails, phone numbers, work history, and professional profiles.

**Example prompts:**

-   `Find VP-level RevOps leaders at [Company] who started in the last 9 months.`
-   `Find the contact information for [Company]'s Head of Partnerships.`
-   `Find B2B SaaS companies in New York with 200–500 employees.`

### **Research any account**

Use Clay to gather deep intelligence on target companies — tech stack, funding, hiring trends, website traffic, and more. Clay pulls from multiple data sources to give you a complete picture of any account.

**Example prompts:**

-   `Find information about the company [Company].`
-   `What are [Company]'s top go-to-market priorities this year? Any recent executive changes or expansion signals?`
-   `What's the tech stack and hiring trend at [Company] over the last 6 months?`

### **Draft personalized outbound**

After gathering context on companies and contacts, use Clay to draft personalized emails based on the research you've collected.

**Example prompts:**

-   `Write an email referencing [Company]'s recent product launches and their VP of Engineering's comments on developer productivity, under 130 words.`
-   `Draft a personalized email to [Company]'s Head of Partnerships about their partnership priorities and key themes from their recent public posts.`
-   `Create outreach for finance leaders at [Company] mentioning their recent executive changes and expansion signals.`

## **Best practices**

To get the best results when using Clay in Microsoft 365 Copilot:

-   Include the company domain (e.g., `contoso.com`), not just the company name
-   Be specific with criteria: job titles, locations, seniority, keywords
-   If you aren't sure what job title you're looking for, try asking "who manages X at company"
-   Use declarative language and keep prompts direct
-   Avoid broad queries or general web searches

## **Running functions**

If your ops team has built Clay Functions, you can invoke them directly from Microsoft 365 Copilot with a single prompt. Functions are pre-built enrichment workflows — like ICP scoring, outbound sequence generation, or account research waterfalls — that your ops team configures once in Clay and enables for your entire team.

To see which functions are available to you, ask:

-   `What functions do you have?`
-   `What workflows has RevOps built for me?`

To run a function, reference it by name:

-   `Run Clay outbound generator for sarah@acme.com`

Microsoft 365 Copilot will find the matching function, run it, and return the results directly in your conversation.

## **MCP settings for your team**

Workspace admins can set credit limits and monitor rep usage from `Settings → MCP users`. For a full walkthrough of the admin controls, see [**MCP settings**](https://university.clay.com/docs/mcp-settings).

## **FAQ**

**Does a Microsoft 365 admin need to install Clay before reps can connect?**

Yes — unlike Claude and ChatGPT where reps connect individually, Microsoft 365 Copilot requires an M365 admin to install and deploy the Clay agent for your organization first. Admins can find Clay in the [**Microsoft Marketplace**](https://marketplace.microsoft.com/en-us/product/WA200011257) or the Agent Store inside Microsoft 365 Copilot and manage deployment from the Microsoft 365 Admin Center. Once deployed, reps are prompted to sign into their Clay account on first use.

**What data sources does Clay use in Microsoft 365 Copilot?**

Clay in Microsoft 365 Copilot pulls from a subset of its 150+ third-party data providers to provide comprehensive coverage across contact data, company intelligence, and web research. If you want to enable additional enrichments, your ops team can add a Function for them and enable it for MCP.

**Can I search for companies?**

Yes — you can search for companies by criteria like location, headcount, and industry. For example: `Find B2B SaaS companies in New York with 200–500 employees.` You can also research any company by asking Clay about it directly — tech stack, funding, hiring trends, leadership changes, and more.

**What if I need data that isn't available?**

If you need additional data points or more advanced workflows, access the full Clay platform at [**app.clay.com**](https://app.clay.com/) with your same account by clicking `Open` in the top right of the Clay widget.

**How do credits work in Microsoft 365 Copilot?**

Credits are consumed at the same rate as using Clay directly — if a Function that finds an email and phone number costs 12 credits in a Clay table, it costs 12 credits when triggered from Microsoft 365 Copilot. Searching for people and companies is free; enrichments consume credits. Your workspace admin controls your credit limit from `Settings → MCP users`.
