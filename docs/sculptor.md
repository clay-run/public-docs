---
title: Sculptor
description: Your go-to-market co-pilot
last_synced: 2026-04-26T01:40:38.269Z
---

# Sculptor

Your go-to-market co-pilot

Sculptor is Clay's **go-to-market co-pilot**. It helps teams turn high-level ideas into production-ready workflows. You can bring a challenge into the chat box and, working alongside Sculptor, deploy it as a live Clay workflow in minutes.

For example, you could:

-   **Build a market analysis workflow:** Identify businesses in your target area and evaluate their readiness.
-   **Automate contact finding:** Collect information from Google Maps, then prioritize prospects and generate outreach messages.
-   **Create personalized messages:** Analyze competitor websites and craft customized outreach content.

## Using Sculptor

1.  **Launch Sculptor.** You can do this in two ways:
    -   From the **homepage** of [app.clay.com](http://app.clay.com/) using the large open text box.
    -   From **within any table** using the `Chat with Sculptor` button.
2.  **State your problem clearly.** Enter the type of table you want Sculptor to create (e.g., "I want to source a total addressable market (TAM) for franchisors in Canada").
    -   Adding details such as geography, industry, or company size helps Sculptor generate better results.
3.  **Iterate and review.** Sculptor will propose a workflow with integrations, enrichments, and conditions.
    -   You can reply directly in the chat to adjust or refine the table instantly.
4.  **Add enrichments.** Click `Continue` to include any recommended enrichments Sculptor suggests for your table.
5.  **Finalize your table.** Your table is created automatically. You can exit the chat at any time, and return later by clicking `Chat with Sculptor` to make further updates. To browse and resume any of your previous Sculptor conversations, click the **chat history** button (clock icon) in the Sculptor panel.

## Chat history

Sculptor saves your conversation history so you can view and continue previous sessions. Click the **chat history** button (clock icon) in the Sculptor panel to browse past conversations.

History is scoped to the surface you're currently working in:

-   **Table Sculptor** — only shows conversations from the table you are currently viewing.
-   **Workflow Builder** — only shows conversations from the workflow you are currently viewing.
-   **Claygent Builder** — only shows conversations for the Claygent you are currently viewing.
-   **Search / Onboarding** — only shows conversations from search and onboarding sessions.

Sculptor conversations cannot be deleted or cleared — there is no control to remove individual conversations or clear the history list in bulk. They are retained so you can return to any previous session at any time.

## Best practices

-   **Go step by step.** Sculptor does best when handling a problem one element at at ime.
-   **Provide context.** Sculptor performs best when you include details, examples, and framing.
-   **Check your work.** All results are inspectable—review and validate before scaling.
-   **Use Sculptor as a strategist.** Treat it like a partner to help shorten your learning curve, navigate complex systems faster, and accelerate iteration.

## Sandbox mode

When Sculptor builds new columns for your table, it automatically puts the table into [sandbox mode](https://www.clay.com/university/guide/sandbox-mode) first. This gives you a chance to review and validate the new columns before they go live—reducing unintended credit burn and giving you more control over changes.

> **Important:** To save Sculptor's proposed columns to your live table, use the **Review changes** button — do _not_ click **Exit Sandbox**. Clicking **Exit Sandbox** will discard all of Sculptor's proposed changes without publishing them.

Once Sculptor adds columns and sandbox mode is active:

1. Review the proposed columns in sandbox mode using a small set of test rows. The **All data** tab shows a **View-only** indicator while sandbox is active — this is expected and means your production table is protected while you test.
2. Click `Review changes` — visible in the tab bar above your table, to the right of the "Test data" / "All data" switcher — to see a summary of all structural column updates.
3. When ready, click `Publish and run` to apply the changes to your full table, or `Publish and don't Run` to sync the configuration without immediately running all rows.

For more on how sandbox mode works, see [Sandbox mode](https://www.clay.com/university/guide/sandbox-mode).

## Analyst mode

Analyst mode lets you query any Clay table using natural language to uncover trends and insights. Ask questions in plain English, and Sculptor will analyze your entire table to identify patterns, outliers, and strategic insights you can export as reports.

### How to use analyst mode

1.  **Open Sculptor.** From within any table, click `Chat with Sculptor` → `Analyze`.
2.  **Ask analytical questions.** For example:
    -   "What are the common characteristics of my highest-value customers?"
    -   "Which market segments have the most opportunity?"
    -   "What were the top reasons for closed-lost deals last quarter?"
    -   "What's my data enrichment match rate by provider?"
3.  Review the analysis. Sculptor will query your table and present insights with visualizations and explanations.
4.  Export your findings to Notion or as a PDF.

## Use cases and examples

The following table covers common Sculptor use cases and key notes for each.

| Use case | Notes and caveats |
| --- | --- |
| List building | Sculptor's primary use case. It can handle most of the setup for you—start from the homepage input to create a CPJ search, enrich the list in a table, then move from a company table to a people table. Sculptor can also help draft outreach emails to those prospects. |
| Data enrichment | Once your table is set up, Sculptor excels at recommending the right enrichments and generating Claygent prompts tailored to your workflow. |
| Building co-pilot | A great first pass before turning to GTME, EGS, or Support. Sculptor can troubleshoot errors, analyze patterns in your data, and even conduct research directly within your table. |

| Team / Function | Challenge | Potential Sculptor Solution |
| --- | --- | --- |
| Enterprise Sales Enablement | Source my TAM for Canadian franchisors and launch outbound. | Identify multi-location businesses, rank by growth, and flag high-intent accounts. |
| Marketing Operations | Generate personalized outreach using competitor data. | Analyze competitors and auto-generate tailored messaging. |
| Revenue Operations | Find stakeholders in target cities within our ICP. | Rank local companies, surface decision-makers, and draft outreach. |

## Sculptor limitations

While Sculptor is powerful, there are a few things to keep in mind:

-   **Weekly conversation limits apply** — Each workspace is limited to **20 in-table Sculptor conversations per week** and **50 homepage conversations per week**, on a rolling 7-day window. A "conversation" is an entire chat thread — every back-and-forth message within a single session counts as one conversation. If you hit the limit, you'll see a message like "You've reached the maximum number of conversations this week for your workspace." Contact support to have your workspace limit increased.
-   **Daily limits apply when testing actions and code via Claude** — When using Sculptor through the [Clay connector in Claude](https://university.clay.com/docs/using-clay-in-claude), you can test-run Clay actions directly up to **25 times per day** per user, and test-run code snippets up to **10 times per day** per user. Limits reset after 24 hours. If you hit a limit, you'll see a message like "You can only test-run Clay actions directly 25 times a day — add the action to a workflow node or table column and run it there instead." Production workflow runs are not affected by these limits.
-   **Supported sources are limited** — Sculptor can only generate sources using companies, people, jobs, Google Maps, CSV imports, or web search. If you want to use a different source, you'll need to manually create it before using Sculptor.
-   **No direct CRM integration (yet)** — Connections must be set up manually for now.
-   **Cross-table operations are limited** — Advanced linking and workflows are still in development.
-   **No export option** — Export functionality hasn't been integrated yet.
-   **Column modifications use sandbox mode** — Sculptor adds new columns to existing tables via [sandbox mode](#sandbox-mode) rather than writing directly to your live table. You'll need to review and publish those changes using the **Review changes** button.
-   **Sculptor can edit AI columns and formula columns, but not action/enrichment or basic columns.** If you ask Sculptor to update an existing AI column or formula column, it can edit it in place. However, action/enrichment columns (including Claygent action columns) and basic columns cannot be edited after creation — in those cases, Sculptor creates a new column with the requested changes instead. The new column appears to the right of your current columns — **scroll right** in your table to find it as a pending suggestion. To update an action/enrichment or basic column directly, click into that column and edit it yourself.
-   **Feature gaps** — Signals tables aren't currently supported.
-   **Data boundaries apply** — Only processes data you provide or data from supported sources and enrichments.

## Troubleshooting

### Suggested column card doesn't appear

When Sculptor proposes a new column but the suggestion card isn't visible, it typically means Sculptor described the action without fully completing it. Sculptor has built-in detection for this situation — the most reliable fix is to **ask Sculptor where the suggestion is** (for example: _"Where is the column you just suggested?"_ or _"I don't see the suggestion card"_). Sculptor will detect that the suggestion is missing and automatically attempt to complete it.

If that doesn't resolve it, a few additional things to try:

-   **Give the column a unique name.** Ask Sculptor to name the column something slightly different (for example, adding `-v2`) to force it to create the column fresh rather than getting stuck on the previous attempt.
-   **Start a new Sculptor conversation.** If the current chat isn't making progress, start a fresh conversation and restate your goal. You can launch a new Sculptor session from the homepage at [app.clay.com](http://app.clay.com/).

### Sculptor is slow to respond or times out

Sculptor includes your table's schema and field configuration with every message it sends. As your conversation grows, all prior messages are included in each new request — so longer threads mean slower responses. If you're experiencing delays or frequent timeouts:

-   **Start a fresh Sculptor conversation.** This is the most reliable fix. Long chat threads accumulate history that adds to processing time. Starting over from the homepage or a new `Chat with Sculptor` session clears the accumulated context.
-   **Keep prompts shorter and more focused.** Ask for one thing at a time rather than large multi-step requests — this reduces processing time and tends to produce more accurate results.
-   **Try a different browser or incognito mode.** This rules out local caching or browser extension issues.

If Sculptor is consistently slow regardless of conversation length, this is a known performance area the team is actively improving.

### "You've reached the maximum number of conversations this week"

This error means your workspace has hit its weekly Sculptor conversation limit. Workspaces are limited to **20 in-table conversations per week** (launched from within a table) and **50 homepage conversations per week** (launched from the [app.clay.com](http://app.clay.com/) homepage), on a rolling 7-day window.

A "conversation" is a full chat thread — multiple back-and-forth messages within one session count as a single conversation. The limit resets automatically after 7 days.

If you hit the limit and need it increased, contact support.

### I asked Sculptor to update an existing column but can't find the changes

Sculptor can edit existing AI columns and formula columns in place. However, if you asked it to update an action/enrichment column (including Claygent action columns) or a basic column, those column types can't be edited after creation — Sculptor creates a new column with the requested changes instead.

To find Sculptor's proposed column:

-   **Scroll right** in your table. The new column is added to the right of your existing columns as a pending suggestion.
-   Click **Review changes** in the tab bar above your table to see a summary of all proposed columns.

To update an action/enrichment or basic column directly without creating a new one, click into that column's header and edit it yourself.

### Sculptor keeps entering sandbox mode when I add a column

This is expected behavior — Sculptor uses sandbox mode whenever it adds new columns to an existing table, rather than writing directly to your live table. This gives you a chance to review proposed changes before they go live.

To apply the proposed column to your table:
1. **Do not click Exit Sandbox** — this discards all of Sculptor's proposed changes without publishing them.
2. Click **Review changes** (visible in the tab bar above your table, to the right of the "Test data" / "All data" switcher) to see a summary of the column updates.
3. Click **Publish and run** or **Publish and don't run** to apply the changes to your full table.

If you'd prefer to add a column directly without going through sandbox, use the **Add enrichment** or **+** button in your table toolbar instead.

### My search only shows 50 rows

When you use Sculptor to set up a Find People, Find Companies, or Find Jobs search, you may see 50 rows in three different situations — each with a different cause and fix.

**In the Sculptor search panel (before clicking Continue):** The search results preview is limited to 50 rows. This is a preview only — it does not cap how many records are imported. When you click **Continue**, Sculptor sends your full search query to the table and imports the complete result set. The button shows the total count (for example, *"2,400 results will be imported"*) so you can confirm the full number before proceeding.

**In your table after the search runs (with the Sandbox Mode badge visible):** If your table is in [Sandbox Mode](https://www.clay.com/university/guide/sandbox-mode) — shown by the **Sandbox Mode** badge in the toolbar — it is capped at a maximum of 50 rows. This is expected behavior and not a search error. Your full results exist in the production table.

To access all your results from sandbox:

-   **To check the full row count without publishing:** Click the **All data** tab in the tab bar above your table. The production table is read-only while sandbox is active, but you can see the total number of rows there.
-   **To run your workflow on all rows:** Click **Review changes** → **Publish and run**. This publishes your Sculptor-built columns to the production table and runs them across all matching rows.

**In your table after publishing (no Sandbox Mode badge visible):** When a search is set up and published, Clay immediately adds the first 50 matching rows to the table as a fast preview, then runs a background export to bring in the full result set. If the background export takes too long to finish — for example, because your search uses a large keyword list or filters across several fields at once — it can time out before completing, leaving the table with only those initial 50 rows.

To fix this, simplify your search so the query can complete in time:

-   **Search one field instead of several.** Applying keyword filters to both the bio/about section and every job description simultaneously increases query time — pick whichever field is most likely to surface relevant results.
-   **Trim your keyword list.** Reduce to your 6–8 most distinctive terms rather than an exhaustive list of 20 or more.
-   **Split into multiple searches.** If you need broad coverage — for example, a long list of schools or companies — break it into two or more searches with smaller filter sets and merge the results in a single table.

## FAQs

### **When should I use Sculptor instead of building manually?**

Sculptor can be helpful throughout the building process, and you can freely turn it on and off as you make progress. Sculptor excels at generating lists via natural language and building new enrichments from scratch. Note that you can always edit or extend workflows manually while working with Sculptor.

### When should I _not_ use Sculptor?

-   **When you're building on a feature that's not yet supported, such as Signals or Clay Sequencer.**
-   **When you need a complete workflow immediately.** Sculptor isn't designed to create entire workflows with a single request (it doesn't create "one-shot workflows"). Instead, it works as your partner throughout the building process. While Sculptor excels as an ideation partner, it's best at accelerating your existing work rather than replacing it.

### **What Clay surfaces does Sculptor support?**

**✅ Full Support**

-   **AI Columns** — Read, recommend, configure, preview ("Use AI" columns only; Claygent and Image Generation columns do not support preview)
-   **Formulas** — Read, recommend, configure (no preview)

**🟡 Partial Support (Read / Recommend only)**

-   **Enrichments** — Read & recommend (configuration coming soon)
-   **Waterfalls** — Read, recommend, and configure when building new tables; cannot edit existing waterfall configurations after creation.
-   **Credits Estimation** — Tracks spend
-   **CRM / Webhook Sources** — Read only
-   **Signals** — Read only

**🔜 Limited or Coming Soon**

-   **Sources (CPJ, Google Maps, CSV)** — Config reading only; full support coming soon
-   **Run Conditions** — Read and configure on new columns; when Sculptor sets a run condition automatically, review it in column settings before running at scale to ensure it matches your data.
-   **Message Drafting** — Not yet supported
-   **Filters & Sorting** — Not yet supported

### How can I use Sculptor to replicate an existing workflow's logic in a new workflow?

Open the existing workflow and click the Sculptor button to open the chat panel. Ask Sculptor to describe the workflow — for example: *"Explain step by step everything this workflow does."* Sculptor reads the full workflow graph and returns a description of each node, its configuration, and how the nodes connect.

Copy that description, open Sculptor on the new workflow, and paste it in as your build instructions. Sculptor will use the description as a blueprint to recreate the logic in the new workflow.

You can also use the Clay CLI to extract a workflow description without opening the Sculptor chat panel directly — ask the CLI to describe your workflow and use the output as build instructions in the same way.

### What table sources does Sculptor connect with?

Sculptor works with these sources:

-   **Find Companies**
-   **Find People**
-   **Find Jobs**
-   **Google** **Maps**
-   **CSV Import**
-   **Web Search**

### How do I make a custom field available to a downstream Upsert in a workflow?

**For Claygent nodes**, the output fields available to downstream steps are defined in the Claygent Builder — not from within the workflow itself. To expose a new output field (for example, an Updated Date), open the Claygent in the Claygent Builder, add the field to its output schema there, and save. The field will then appear as a mappable option in downstream steps automatically.

**For Run Code (Python) nodes**, output fields are inferred from what the code returns. After updating the code to return a new field, click **Update outputs from code** in the node's sidebar to refresh the schema — the field won't appear in downstream mapping until you do.

To generate a custom field that doesn't come from an existing upstream node — for example, a current timestamp to use as an Updated Date — add a **Run Code (Python)** node immediately before your Upsert step and return the value explicitly:

```python
def handler(context):
    from datetime import datetime, timezone
    return {"updated_date": datetime.now(timezone.utc).isoformat()}
```

Fields returned by a code node are available at the top level in downstream steps. Map `$.updated_date` (not `$.result.updated_date`) in your Upsert.
