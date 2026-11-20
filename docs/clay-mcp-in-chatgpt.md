---
title: Clay MCP in ChatGPT
description: Connect the Clay MCP to ChatGPT, sign in to your workspace, and see what you can build and run from a chat on your plan.
last_synced: 2026-11-19T07:40:14.942Z
---

# Clay MCP in ChatGPT

Connect the Clay MCP to ChatGPT, sign in to your workspace, and see what you can build and run from a chat on your plan.

The Clay MCP is a ChatGPT app that connects ChatGPT to your Clay workspace with your own Clay sign-in. Once it's set up, you can search Clay's GTM dataset, run your workspace's functions, and build multi-step workflows, email campaigns, and segments from a conversation, all on Clay's existing integrations and data.

It carries the same tools as the Clay CLI, the `clay` command that coding agents run, packaged for chat. If you work in Claude Code or Codex instead, see [Installing Clay Plugin (API & CLI)](https://university.clay.com/docs/clay-api-cli).

ChatGPT lists two Clay apps. This doc covers the Clay MCP, listed as `Clay`. The other, listed as `Clay for Reps`, is MCP for Reps, which sales reps use to prospect and to run the functions their ops team approves; see [Using Clay in ChatGPT](https://university.clay.com/docs/using-clay-in-chatgpt) for that one.

## Before you start

You'll need:

-   **A ChatGPT account.** If your company runs ChatGPT on a Business, Enterprise, or Edu plan, a ChatGPT admin may need to make Clay available to you first.
-   **Editor or Admin access** in the Clay workspace you'll connect.

## Setting up the Clay MCP in ChatGPT

1.  **Find Clay in ChatGPT's app directory.** In ChatGPT, open the app directory, search for Clay, and connect the app named `Clay`, not `Clay for Reps`.
2.  **Connect your workspace.** When ChatGPT sends you to Clay, sign in, choose the workspace to connect, and click `Authorize`.
3.  **Confirm it's working.** Start a new chat with Clay turned on, and ask something like "Which Clay workspace am I connected to?"

### Troubleshooting

-   **You can't find or connect Clay on a company ChatGPT plan:** a ChatGPT admin needs to make Clay available in your ChatGPT workspace.
-   **Clay shows `No workspaces available`, or your workspace isn't in the list:** you need Editor or Admin access in that workspace. Ask a workspace admin to change your role.
-   **You connected the wrong workspace:** disconnect Clay in ChatGPT's settings, then connect again and choose the right workspace.
-   **Some tools seem to be missing:** ChatGPT only sees the tools your workspace role allows. Ask a workspace admin if you need more access.

## What you can do

Ask for what you want in plain language, and ChatGPT picks the Clay tools to use. Search results, segments, campaigns, and workflows can show as interactive previews right in the chat.

### Searches

Find companies and people with structured filters over Clay's GTM dataset, refine the search as you go, and see the results as a table in the chat. From the results table, you can run your workspace's functions on the rows you found. Results count toward your plan's search limits, covered in **Plan availability and limits** below.

-   _"Find Series B SaaS companies in the US with 100–500 employees."_
-   _"Now narrow that to companies hiring for RevOps roles."_
-   _"Find the VP of Sales at each of those companies."_

### Audiences

Work with Audiences, where your workspace's own people, companies, and deals live. You can look up records, count or search the records that match a filter, and create or edit segments of people and companies.

-   _"How many companies in our Audiences are in the healthcare segment?"_
-   _"Show me the people we have at Acme Corp."_

### Functions and routines

Run Clay-managed functions and your own custom functions on a single record or in bulk. They run as routines, a function or workflow made callable from outside the Clay app, and you can save an existing function or workflow as a new routine from ChatGPT. You can start runs, check their status, and cancel them from the chat.

-   _"Which routines do we have for enriching companies?"_
-   _"Run our company-scoring routine on Stripe."_
-   _"What's the status of my last bulk run?"_

### Workflows

**Note:** Workflows is in beta. A Workspace Admin can request access from the `Beta program` section of your workspace settings by clicking `Join beta program`.

Build and edit Workflows, Clay's builder for multi-step logic that runs one record at a time, for enrichment, research, scoring, routing, and other repeatable GTM work. You can run a test, rerun failed runs, read the results step by step, set alerts, and publish a workflow when it's ready. ChatGPT can show the workflow and its recent runs in the chat.

-   _"Build a workflow that takes a company domain, finds the head of marketing, and scores fit against our ICP."_
-   _"Test it on these five domains."_
-   _"Why did yesterday's runs fail at the enrichment step?"_

### Tables

Read data from your Clay tables: list tables, look at their columns, read rows, and ask questions about a table's data, like counts and totals. Tables are read-only from ChatGPT, so to build new logic, ask for a workflow instead.

Listing tables and reading rows need a paid or trial plan. Queries that combine several tables need API table sync, available on Enterprise plans.

-   _"Show me the first 20 rows of our Inbound Leads table."_

### Sequencer

Build and edit campaign sequences in Sequencer, Clay's email outreach tool. You can check copy for spam triggers, send a test email, run variant tests, and read analytics, and ChatGPT can show the campaign in the chat after an edit. Launching, pausing, and resuming a campaign stay in the Clay app.

-   _"Draft a 3-step sequence for the VP of Sales list we just built."_
-   _"How is the Q4 outbound campaign performing?"_

### Signals

Create and manage signals, which watch your accounts and contacts for changes such as job changes, new hires, and funding news. You can also edit, pause, resume, or delete a signal.

-   _"Watch our target accounts for funding news."_

## Plan availability and limits

The Clay MCP is available on every Clay plan, including Free and Trial.

Search result limits are shared across the Clay MCP, the CLI, and Clay's Public API, and they scale with your plan:

| Plan | Results per request | Results per search | Results per period |
| --- | --- | --- | --- |
| Free | 50 | 50 | 100 per 30 days |
| Trial | 50 | 50 | 10,000 per 14 days |
| Flex | 500 | Up to your period limit | 50,000 per 30 days |
| Paid self-serve plans | 500 | Up to your period limit | 1,000,000 per 30 days |
| Legacy paid plans | 500 | Up to your period limit | 1,000,000 per year |
| Enterprise | 500 | Up to your period limit | 10,000,000 per 30 days |

**Results per request** is the most one page of search results can hold. **Results per search** is the total you can page through for one search, and **results per period** is your workspace's running total across the Clay MCP, the CLI, and the Public API together.

30-day periods roll rather than resetting on a set date: each day at midnight UTC, the oldest day of usage ages out of the window. Legacy paid plans (Starter, Explorer, and Pro) keep a yearly period that resets on January 1 UTC instead. Moving to a current paid plan or to Enterprise switches the workspace to the rolling window.

When you go over a limit, Clay tells you which limit you hit, and a period-limit message also says when usage frees up. On Free and Trial, the message links to upgrading your plan. To raise a limit on any other plan, contact Clay Support; Enterprise workspaces can reach out to their Clay account team.

### Checking your search usage

Open the `API and CLI` page in the left sidebar. The `Search usage` card shows the results your workspace has used out of its limit for the current period, including searches run from ChatGPT. A rolling 30-day period shows `Counts the last 30 days`, and a fixed period shows the date it resets.

## FAQs

### Does using the Clay MCP cost extra?

No. Work you start from ChatGPT spends the same credits and actions as the same work done in the Clay app. That spend is reported as MCP usage for the person who ran it, rather than as API and CLI usage.

### What's the difference between the Clay MCP and MCP for Reps?

They cover different use cases, so ChatGPT has a separate app for each. The Clay MCP is for builders who want to work in Clay without leaving ChatGPT. It signs you in with your own Clay account and gives you the tools your workspace role allows, so you can build workflows, query Audiences, edit campaigns, and more.

MCP for Reps is for sales reps to prospect with. Reps can find people and companies and run the functions and workflows that admins and editors have enabled for them, and an admin sets each rep's credit budget. See [MCP in Clay](https://university.clay.com/docs/mcp-settings) for how that access is configured, and [Clay MCP for Reps vs. Agent Plugin](https://university.clay.com/docs/mcp-for-reps-vs-agent-plugin) for choosing between the rep and builder surfaces.

### Can a workspace admin control who uses Clay from ChatGPT?

Yes. On the `Agent users` page, which admins open from the sidebar on the Clay homepage, the `Allowed MCP clients` section has a toggle for each AI app. Turning `ChatGPT` off blocks ChatGPT from connecting to the workspace, and anyone who tries sees `Not permitted by your workspace`.

Access also follows each person's role. Clay checks it on every request, so removing someone from the workspace or lowering their role below Editor cuts off their ChatGPT access right away. It's the same role check the CLI uses, covered in [CLI security and privacy](https://university.clay.com/docs/cli-security-privacy).
