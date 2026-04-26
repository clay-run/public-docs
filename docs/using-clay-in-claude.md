---
title: Using Clay in Claude
source_url: https://university.clay.com/docs/using-clay-in-claude
description: Find people, enrich contacts, and draft personalized outreach—all
  within a Claude conversation
last_synced: 2026-04-26T01:40:52.929Z
upstream_hash: 2041fecf55afc3051d85f4a4eef2228ca1ccc8085feed22c5ed3c3d72e2c9afc
---

# Using Clay in Claude

Find people, enrich contacts, and draft personalized outreach—all within a Claude conversation

The Clay connector in Claude lets you find people, enrich contacts, and draft personalized outreach—all within a conversation. Clay pulls data from over 150 providers and AI-powered research agents directly into Claude, so you can move from research to action in seconds.

## Getting started

1.  Go to the [Claude Connectors page](https://claude.com/connectors/clay) to connect Clay to your account. _Note: If you're on a Claude Enterprise plan, an admin must add the Clay connector before you can use it._
    -   If you have an existing Clay account, you'll connect immediately. If you're new to Clay, an account will be created for you during setup.
    -   You'll receive 500 free Clay credits when you connect for the first time.
2.  In any Claude conversation, ask Claude to find people or companies—the Clay connector will activate automatically.
3.  Ask Claude to find people, research accounts, or enrich contacts using natural language. For example:
    -   "Find VP- and Director-level RevOps leaders at \[Company\] who started in the last 9 months."
    -   "What are \[Company\]'s top go-to-market priorities this year?"
4.  Clay will pull the available data and present it in an interactive view where you can:
    -   View results as a table
    -   Add filters (e.g., only people in the US or people who have been there for less than 6 months)
    -   Enrich contacts with additional data points (email address, work history summary, thought leadership)
    -   Draft personalized emails based on the research
5.  At any time, you can open your results directly in Clay at [app.clay.com](http://app.clay.com) to access more powerful enrichment and workflow capabilities.

## Use cases for Clay in Claude

### Find and enrich people at target accounts

Once you've researched an account, Clay helps you find the right people to reach out to. Search by job title, seniority, location, or other criteria, and Clay will enrich each contact with verified emails, phone numbers, work history, and professional profiles.

**Note:** Clay finds verified contact information including email addresses and phone numbers. You can also ask Clay to pull in additional context like work history, recent achievements, thought leadership, and open roles on their team.

**Example prompts:**

-   `Find VP- and Director-level RevOps leaders at [Company] who started in the last 9 months.`
-   `Find the contact information for [Company]'s Head of Partnerships.`
-   `Who are the engineering leaders at [Company] and what are their emails?`

### Research any account

Use Clay to gather deep intelligence on target companies—tech stack, funding, hiring trends, website traffic, and more. Clay pulls from multiple data sources to give you a complete picture of any account.

**Example prompts:**

-   `What are [Company]'s top go-to-market priorities this year? Any recent executive changes or expansion signals?`
-   `Show me recent public posts from sales or product leaders at [Company] that mention automation or AI adoption.`
-   `What new markets has [Company] expanded into recently? How has headcount changed over the last year? What tools power their partner GTM motion?`

### Draft personalized outbound

After gathering context on companies and contacts, use Clay to draft personalized emails. Clay uses the research and enrichment data you've collected to create relevant, context-driven outreach that resonates with your prospects.

**Note:** Clay uses the research and enrichment data you’ve collected to create relevant, context-driven outreach. Email copy goes beyond surface-level personalization by pulling in concrete details like product initiatives, hiring focus, public commentary, and leadership changes.

**Example prompts:**

-   `Write an email referencing [Company]'s recent product launches and their VP of Engineering's comments on developer productivity, under 130 words.`
-   `Draft a personalized email to [Company]'s Head of Partnerships about their partnership priorities and key themes from their recent public posts.`
-   `Create outreach for finance leaders at [Company] mentioning their recent executive changes and expansion signals.`

## Best practices

To get the best results when using Clay in Claude:

-   Include the company domain (e.g., "[rippling.com](http://rippling.com)"), not just the company name
-   Limit your search to one company at a time for more accurate results
-   Be specific with criteria: job titles, locations, seniority, keywords
-   If you aren't sure what job title you're looking for, try asking "who manages X at company"
-   Avoid broad queries or general web searches

## Running functions

If your ops team has built Clay Functions, you can invoke them directly from Claude with a single prompt. Functions are pre-built enrichment workflows — like ICP scoring, outbound sequence generation, or account research waterfalls — that your ops team configures once in Clay and enables for your entire team.

To see which functions are available to you, ask:

-   `What functions do you have?`
-   `What workflows has RevOps built for me?`

To run a function, reference it by name:

-   `Run Clay outbound generator for sarah@acme.com`

Claude will find the matching function, run it, and return the results directly in your conversation. Functions also appear as suggested options in the standard Clay widget for easier discovery.

## MCP settings for your team

Workspace admins can set credit limits and monitor rep usage from `Settings → MCP users`. For a full walkthrough of the admin controls, see [MCP settings](https://university.clay.com/docs/mcp-settings).

## FAQ

**What data sources does Clay use in Claude?**

Clay in Claude pulls from a subset of its 150+ third-party data providers to provide comprehensive coverage across contact data, company intelligence, and web research. If you want to enable additional enrichments, add a function for them and enable it for MCP.

**What if I need data that isn't available?**

If you need additional data points or more advanced workflows, access the full Clay platform at [app.clay.com](http://app.clay.com) with your same account to unlock more powerful enrichment and workflow capabilities.

**Can I search for companies?**

Company search is not currently supported. However, you can research companies by asking Clay questions about target accounts—tech stack, funding, hiring trends, leadership changes, and more. Clay surfaces information that's otherwise hard to find: org charts, job changes, funding history, social context, and tech stack signals.

**How many credits do I get?**

All users receive 500 credits when connecting to Clay in Claude for the first time. If you reach your limit, you can continue searching for people without enrichments, or upgrade to a paid plan for full functionality.

**Can the app be used for free?**

All users receive 500 credits to test this feature. When you reach the credit limit, you can:

-   Continue running people searches in Claude for free, but without enrichments like email.
-   Continue building in your trial account directly in Clay, with full functionality and 2,000 more credits.
-   Upgrade to a paid plan.

**Do I need a paid Claude plan?**

No.

**Will this use credits from my account?**

All users receive 500 bonus credits to test the app. After that, credits will be drawn from your paid plan.

**How does pricing work?**

Credit pricing matches standard Clay plans. Claude serves as an alternative interface for using your Clay credits. You'll receive 500 free credits when you connect Clay to Claude (whether you're signing up for the first time or connecting an existing account). After that, credits will be drawn from your Clay plan as you use enrichments and data sources.

**Do I need to invoke Clay manually, or will Claude know to use it?**

Claude will automatically activate Clay based on context when you ask about finding people, researching accounts, or enriching contacts. You don't need to explicitly mention Clay in your prompt—just describe what you need.

**Can I ask which Functions are available to me?**

Yes. Ask _"What functions do you have?"_ or _"What workflows has RevOps built for me?"_ and Claude will list any Functions your ops team has enabled for your account.

**Does Clay work with Claude Code?**

Yes. Once you connect Clay via Claude’s connector system at `claude.com/connectors/clay`, it will also work in Claude Code.

**When I run an action in Claude, does it count as a Clay action?**

Yes. Everything runs on a Clay table behind the scenes, so actions taken through Claude count as Clay actions and draw from your credit balance accordingly.

**If I send outreach from Claude, does it go through Sequencer or my personal email?**

It depends on how the function is set up. By default, Claude does not have access to your Sequencer. However, you can create a function that uploads someone to Sequencer and make that available for MCP. If the function includes Sequencer, it routes through Sequencer. Otherwise, you can direct Claude to send via Gmail or another connected email provider.

**Does using Clay in Claude create a Clay table?**

If you click `Open in Clay`, a table is created in your Clay workspace. For one-off operations — like finding a single contact's email — a table is not created by default.

**How does my admin control my credit limit?**

Your workspace admin can set a default credit limit for all reps, or a per-user override, from `Settings → MCP users`. If you hit your limit, further enrichments will be blocked until the monthly reset on the 1st of each month at midnight UTC. Contact your admin to have your limit adjusted.
