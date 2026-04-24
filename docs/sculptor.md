---
title: Sculptor
source_url: https://university.clay.com/docs/sculptor
---

# Sculptor

Your go-to-market co-pilot

## Overview

Sculptor is Clay's **go-to-market co-pilot**. It helps teams turn high-level ideas into production-ready workflows. You can bring a challenge into the chat box and, working alongside Sculptor, deploy it as a live Clay workflow in minutes.

For example, you could:

- **Build a market analysis workflow:** Identify businesses in your target area and evaluate their readiness.
- **Automate contact finding:** Collect information from Google Maps, then prioritize prospects and generate outreach messages.
- **Create personalized messages:** Analyze competitor websites and craft customized outreach content.

## Using Sculptor

1. **Launch Sculptor.** You can do this in two ways:
   - From the **homepage** of [app.clay.com](http://app.clay.com/) using the large open text box.
   - From **within any table** using the `Chat with Sculptor` button.
2. **State your problem clearly.** Enter the type of table you want Sculptor to create (e.g., "I want to source a TAM for franchisors in Canada").
   - Adding details such as geography, industry, or company size helps Sculptor generate better results.
3. **Iterate and review.** Sculptor will propose a workflow with integrations, enrichments, and conditions.
   - You can reply directly in the chat to adjust or refine the table instantly.
4. **Add enrichments.** Click `Continue` to include any recommended enrichments Sculptor suggests for your table.
5. **Finalize your table.** Your table is created automatically. You can exit the chat at any time, and return later by clicking `Chat with Sculptor` to make further updates.

## Best practices

- **Go step by step.** Sculptor does best when handling a problem one element at a time.
- **Provide context.** Sculptor performs best when you include details, examples, and framing.
- **Check your work.** All results are inspectable—review and validate before scaling.
- **Use Sculptor as a strategist.** Treat it like a partner to help shorten your learning curve, navigate complex systems faster, and accelerate iteration.

## Analyst mode

Analyst mode lets you query any Clay table using natural language to uncover trends and insights. Ask questions in plain English, and Sculptor will analyze your entire table to identify patterns, outliers, and strategic insights you can export as reports.

### How to use analyst mode

1. **Open Sculptor.** From within any table, click `Chat with Sculptor` → `Analyze`.
2. **Ask analytical questions.** For example:
   - "What are the common characteristics of my highest-value customers?"
   - "Which market segments have the most opportunity?"
   - "What were the top reasons for closed-lost deals last quarter?"
   - "What's my data enrichment match rate by provider?"
3. Review the analysis. Sculptor will query your table and present insights with visualizations and explanations.
4. Export your findings to Notion or as a PDF.

## Use cases and examples

| Use case | Notes and caveats |
|----------|-------------------|
| List building | Sculptor's primary use case. It can handle most of the setup for you—start from the homepage input to create a CPJ search, enrich the list in a table, then move from a company table to a people table. Sculptor can also help draft outreach emails to those prospects. |
| Data enrichment | Once your table is set up, Sculptor excels at recommending the right enrichments and generating Claygent prompts tailored to your workflow. |
| Building co-pilot | A great first pass before turning to GTME, EGS, or Support. Sculptor can troubleshoot errors, analyze patterns in your data, and even conduct research directly within your table. |

| Team / Function | Challenge | Potential Sculptor Solution |
|-----------------|-----------|-------------------------------|
| Enterprise Sales Enablement | `Source my TAM for Canadian franchisors and launch outbound.` | Identify multi-location businesses, rank by growth, and flag high-intent accounts. |
| Marketing Operations | `Generate personalized outreach using competitor data.` | Analyze competitors and auto-generate tailored messaging. |
| Revenue Operations | `Find stakeholders in target cities within our ICP.` | Rank local companies, surface decision-makers, and draft outreach. |

## Sculptor limitations

While Sculptor is powerful, there are a few things to keep in mind:

- **Supported sources are limited** — Sculptor can only generate sources using companies, people, jobs, Google Maps, CSV imports, or web search. If you want to use a different source, you'll need to manually create it before using Sculptor.
- **No direct CRM integration (yet)** — Connections must be set up manually for now.
- **Cross-table operations are limited** — Advanced linking and workflows are still in development.
- **No export option** — Export functionality hasn't been integrated yet.
- **No write capabilities yet** — You can create new tables, but can't modify existing ones.
- **Feature gaps** — Signals tables aren't currently supported.
- **Data boundaries apply** — Only processes data you provide or data from supported sources and enrichments.

## FAQs

### When should I use Sculptor instead of building manually?

Sculptor can be helpful throughout the building process, and you can freely turn it on and off as you make progress. Sculptor excels at generating lists via natural language and building new enrichments from scratch. Note that you can always edit or extend workflows manually while working with Sculptor.

### When should I not use Sculptor?

- **When you're building on a feature that's not yet supported, such as Signals or Clay Sequencer.**
- **When you need a complete workflow immediately.** Sculptor isn't designed to create entire workflows with a single request (it doesn't create "one-shot workflows"). Instead, it works as your partner throughout the building process. While Sculptor excels as an ideation partner, it's best at accelerating your existing work rather than replacing it.

### What Clay surfaces does Sculptor support?

**Full Support**

- **AI Columns** — Read, recommend, configure, edit, preview
- **Formulas** — Read, recommend, configure, edit

**Partial Support (Read / Recommend only)**

- **Enrichments** — Read & recommend (configuration coming soon)
- **Waterfalls** — Read & recommend (configuration coming soon)
- **Credits Estimation** — Tracks spend
- **CRM / Webhook Sources** — Read only
- **Signals** — Read only

**Limited or Coming Soon**

- **Sources (CPJ, Google Maps, CSV)** — Config reading only; full support coming soon
- **Run Conditions** — Very limited; more functionality on the way
- **Message Drafting** — Not yet supported
- **Filters & Sorting** — Not yet supported

### What table sources does Sculptor connect with?

Sculptor works with these sources:

- **Find Companies**
- **Find People**
- **Find Jobs**
- **Google Maps**
- **CSV Import**
- **Web Search**
