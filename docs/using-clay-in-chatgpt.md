---
title: Using Clay in ChatGPT
source_url: https://university.clay.com/docs/using-clay-in-chatgpt
last_synced: 2026-04-26T01:40:52.599Z
upstream_hash: 0f4c6c3b41db7a5f15f28f0cf12b8e7a616a1bc3c23f44444dd1b3143e3dcd8a
---

# Using Clay in ChatGPT

Find people, enrich contacts, and draft personalized outreach — all within a regular ChatGPT conversation.

Clay in ChatGPT lets you find people, enrich contacts, and draft personalized outreach — all within a regular ChatGPT conversation. Clay pulls data from a subset of its 150+ providers and AI-powered research agents directly into ChatGPT, so you can move from research to action in seconds.

## Getting started

1.  Open ChatGPT:
    -   **If using the browser,** type `@Clay` at the start of your prompt, and describe what you need.
    -   **If using the desktop app,** type `/Clay` at the start of your prompt, and describe what you need.
2.  If you haven't already, you'll be prompted to sign into your Clay account.
3.  Clay will automatically pull the available data and present it in an interactive view.
4.  From this interactive view you can:
    -   Toggle to view the list of people as a table
    -   Add a filter (e.g., only people in the US or people who have been there for less than 6 months)
    -   Enrich the data with different data points (email address, work history summary, thought leadership)
    -   Click `View Info` next to a person's name to view more professional information or `Draft Email`
        -   **Note:** You'll need to enrich and find a person's email address before you can draft an outreach email.
5.  At any time, you can click `Open in Clay` in the top right corner to unlock even more powerful enrichment and workflow capabilities directly in your Clay table.

 Your browser does not support the video tag.

Paused

(function () { const video = document.getElementById("clayVideo"); const playBtn = document.getElementById("playBtn"); const pauseBtn = document.getElementById("pauseBtn"); const statusText = document.getElementById("statusText"); playBtn.addEventListener("click", async () => { try { await video.play(); } catch (e) { // Autoplay restrictions can block play until a user gesture. console.warn("Play blocked:", e); } }); pauseBtn.addEventListener("click", () => video.pause()); video.addEventListener("play", () => (statusText.textContent = "Playing")); video.addEventListener("pause", () => (statusText.textContent = "Paused")); video.addEventListener("ended", () => (statusText.textContent = "Ended")); })();

##   
Use cases for Clay in ChatGPT

### Find and enrich people at target accounts

Once you've researched an account, Clay can help you find the right people to reach out to. Search by job title, seniority, location, or other criteria, and Clay will enrich each contact with verified emails, phone numbers, work history, and professional profile.

**Example prompts:**

-   `@Clay find VP-level finance leaders at [Company] who joined in the last 6 months.`
-   `@Clay Find Product execs who joined [Company] in the last 6 months.`
-   `@Clay Who are the engineering leaders at [Company] and what are their emails?`

**Note:** Search is only available for people. Company search is not currently supported.

### Research any account

Use Clay to gather deep intelligence on target companies—tech stack, funding, hiring trends, website traffic, and more. Clay pulls from multiple data sources to give you a complete picture of any account.

**Example prompts:**

-   `@Clay show me [Company]'s hiring trends, tech stack, and new product announcements.`
-   `@Clay review [Company]'s latest 10-K and summarize its priorities, leadership changes, and headcount trends.`
-   `@Clay What's the headcount growth, website traffic, and tech stack of [Company]?`

### Draft personalized outbound

After gathering context on companies and contacts, use Clay to draft personalized emails. Clay uses all the research and enrichment data you've collected to create relevant, context-driven outreach that resonates with your prospects.

**Note:** Email copy is automatically filled with information based on the business context of the Clay workspace you authenticated with. This ensures your message aligns with your company's positioning and value proposition. To change this, click ⚙️ in the top right and edit directly in Clay.

**Example prompts:**

-   `@Clay Draft an email to [Company]'s CPO referencing their AI spend and tech stack.`
-   `@Clay Write a personalized email to these contacts about how we can help with their recent product launch.`
-   `@Clay Create outreach for these finance leaders mentioning their company's recent funding round.`

## Best practices

To get the best results when using Clay in ChatGPT:

-   Include the company domain (e.g., "rippling.com"), not just the company name
-   Limit your search to one company at a time for more accurate results
-   Be specific with criteria: job titles, locations, seniority, keywords
-   If you aren't sure what job title you're looking for, try asking "who manages X at company"
-   Use declarative language and keep prompts direct
-   Avoid broad queries or general web searches

## Running functions

If your ops team has built Clay functions, you can invoke them directly from ChatGPT with a single prompt. Functions are pre-built enrichment workflows — like ICP scoring, outbound sequence generation, or account research waterfalls — that your ops team configures once in Clay and enables for your entire team.

To see which functions are available to you:

-   `@Clay What functions do you have?`

To run a function, reference it by name in your prompt:

-   `@Clay Run Clay outbound generator for sarah@acme.com`

Clay will find the matching function, run it, and return the results directly in your chat. Functions also appear as suggested options in the standard Clay widget for easier discovery.

## MCP settings for your team

Workspace admins can set credit limits and monitor rep usage from `Settings → MCP users`. For a full walkthrough of the admin controls, see [MCP settings](https://university.clay.com/docs/mcp-settings).

## FAQ

**What data sources does Clay use in ChatGPT?**

Clay in ChatGPT pulls from a subset of its 150+ third-party data providers to give you comprehensive coverage across contact data, company intelligence, and web research. If you want to enable additional enrichments, add a function for them and enable it for MCP.

**What if I need data that isn't available?**

If you need additional data points or more advanced workflows, access the full Clay platform at [app.clay.com](http://app.clay.com) with your same account. Move your existing table from ChatGPT by clicking `Open in Clay`.

**Can I search for companies?**

Company search is not currently supported. However, you can research companies by asking Clay questions about target accounts—tech stack, funding, hiring trends, leadership changes, and more. Clay surfaces information that's otherwise hard to find: org charts, job changes, funding history, social context, and tech stack signals.

**How many credits do I get?**

New users receive 500 credits to test Clay in ChatGPT. If you reach your limit, you can continue searching for people without enrichments, or upgrade to a paid plan for full functionality.

**Can the app be used for free?**

All users receive 500 credits to test this feature. When you reach the maximum number of credits within the ChatGPT interface, you can:

-   Continue running people searches in ChatGPT for free, but without enrichments like email.
-   Continue building in your trial account directly in Clay, with full functionality and 2,000 more credits.
-   Upgrade to a paid plan.

**Do I need a paid ChatGPT plan?**

No, you only need to be logged in to ChatGPT.

**Will this use credits from my account?**

All users receive 500 bonus credits to test the app. After that, credits will be drawn from your paid plan.

**How does pricing work?**

Credit pricing matches standard Clay plans. ChatGPT serves as an alternative interface for using your Clay credits. Because this experience is designed for researching and enriching contacts one at a time (rather than processing bulk data), each ChatGPT interaction typically uses 20–100 credits depending on the enrichments you request.

**Do I need to invoke Clay manually, or will ChatGPT know to use it?**

In ChatGPT, type `@Clay` (browser) or `/Clay` (desktop app) at the start of your prompt to invoke Clay. Once connected, Clay activates and pulls the relevant data immediately.

**Can I ask which functions are available to me?**

Yes. Type `@Clay What functions do you have?` and Clay will list any functions your ops team has enabled for your account.

**When I run an action in ChatGPT, does it count as a Clay action?**

Yes. Everything runs on a Clay table behind the scenes, so actions taken through ChatGPT count as Clay actions and draw from your credit balance accordingly.

**If I send outreach from ChatGPT, does it go through Sequencer or my personal email?**

By default, ChatGPT does not have access to your Sequencer. However, you can create a function that uploads someone to Sequencer and make that available for MCP. If the function includes Sequencer, it routes through Sequencer. Otherwise, you can direct the assistant to send via Gmail or another connected email provider.

**Does using Clay in ChatGPT create a Clay table?**

If you click `Open in Clay`, a table is created in your Clay workspace. For one-off operations — like finding a single contact's email — a table is not created by default.

**How does my admin control my credit limit?**

Your workspace admin can set a default credit limit for all reps, or a per-user override, from `Settings → MCP users`. If you hit your limit, further enrichments will be blocked until the monthly reset on the 1st of each month at midnight UTC. Contact your admin to have your limit adjusted.
