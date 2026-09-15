---
title: Clay Agent Plugin (API & CLI)
description: Use Clay's CLI and Public API to run searches, call enrichment functions, and build Workflows programmatically from coding agents, terminals, and backend systems.
last_synced: 2026-09-15T18:32:57.405Z
---

# Clay Agent Plugin (API & CLI)

Install the Clay Agent Plugin, sign in from any environment, and see what the API and CLI can do on your plan.

Clay's plugin lets you use Clay programmatically — from coding agents, terminals, and backend systems — without working in the UI. With the API and CLI, you can run searches over Clay's GTM dataset, call Clay enrichment functions, and build Workflows, all using Clay's existing integrations and data infrastructure.

**Note:** The plugin installs Clay's skills and the Clay CLI into your coding agent. It doesn't include an MCP server, so installing the plugin doesn't give your agent the MCP for Reps toolset — that connection is set up separately.

## Getting started

### Install the plugin

Tell any coding agent to set the plugin up for you — Claude Code, Codex, Cursor, or anything else. Copy this prompt:

`Set up the Clay plugin by following the steps in <https://github.com/clay-run/agent-plugins`\>

Your agent will install the plugin, set up the `clay` command, and sign you in.

### Setup guide

### Signing in without a browser

The `clay login` command signs you in by opening a browser on the machine you're working on. That isn't possible everywhere — on a remote server, inside a container, or in an automated pipeline, there's no browser for it to open.

In those cases, run `clay login --device` instead. It prints a link and a short code, and you approve the sign-in from a browser on any other device — your laptop or phone works fine.

1.  Run `clay login --device`. The CLI prints a verification link with your code pre-filled, prints the code on its own, and then waits for approval.
2.  Open the link in a browser on any device, and sign in to Clay if you aren't already.
    -   If you enter the verification URL without the code, Clay shows `Connect a device` — type the code from your terminal into the `Code` field and click `Continue`.
3.  On `Connect Clay CLI`, check that the code on screen matches the one in your terminal, choose a workspace under `Which workspace should Clay CLI connect to?`, and click `Authorize`. To reject the request, click `Deny`.
4.  The browser confirms `Device connected` and the CLI finishes signing in on its own — there is nothing to paste back into your terminal.

**Note:** The code expires 10 minutes after the CLI prints it, and it can only be approved once. If it expires before you approve it, or you deny the request, run the command again to get a new code.

For the full CLI quickstart, Public API setup, code examples, and guides for Searches, Routines, and Workflows, see [**developers.clay.com**](https://developers.clay.com/).

## What you can do

The plugin has two primary features:

-   **CLI** — Build GTM workflows in natural language from coding agents (including Claude Code, Codex, and Cursor).
-   **Public API** — Access data from Clay or 200+ vendors in the data marketplace. Trigger functions, Claygents, or workflows.

Both paths consume the same credits and actions as equivalent in-product work. There is no additional cost to use the plugin.

The plugin also gives you access to:

-   [**Audiences**](https://university.clay.com/docs/audiences) — Read and segment the workspace's own people, companies, and deals. See **Audiences for agents and the CLI**.
-   [**Searches**](https://university.clay.com/docs/search) — Find companies and people using structured filters over Clay's GTM dataset. Learn more about Searches in [this video walkthrough](https://www.loom.com/share/6a125988c8b14b89aded2e75b8265d5c).
-   [**Functions**](https://university.clay.com/docs/functions) — Run [**managed functions**](https://university.clay.com/docs/managed-functions) and custom functions. Learn more about functions in [this video walkthrough](https://www.loom.com/share/7050c0b62b0648a984d6438112d02985).
-   [**Workflows**](https://university.clay.com/docs/workflows) — Enrichment, research, scoring, routing, and other repeatable GTM logic.
-   **Tables** — Read structured data from known Clay tables.
-   [**Sequencer**](https://university.clay.com/docs/getting-started-with-sequencer) — Build and edit campaign sequences, run variant tests, and read analytics from the CLI. Launching, pausing, and resuming a campaign stay in the Clay app.

**Note:** The CLI and API are currently supported on Mac and Linux. Windows isn't supported yet.

## Plan availability and limits

The developer platform is available across all Clay plans, including free and trial plans. Legacy plans also have access.

Search result limits vary by plan:

| Plan | Search results per request | Total search results |
| --- | --- | --- |
| Free | 50 | 100/mo |
| Trial | 50 | 10k per 14 days |
| Flex | 500 | 50k/yr |
| Other paid self-serve plans | 500 | 1M/yr |
| Enterprise | 500 | 10M/yr |

## FAQs

### Does using the API or CLI cost extra credits?

No. API and CLI calls consume the same credits and actions as the equivalent work done in-product. There is no additional cost because work is triggered via the developer platform instead of the UI.

### What's the difference between the plugin and the Public API?

The plugin gives agent environments (Claude Code, Codex, Cursor) Clay's skills and the Clay CLI — the fastest path for agent-first and interactive coding workflows. The Public API is better suited for background jobs and your own apps, where you want to call Clay directly instead of installing anything.

The Public API uses its own key rather than your CLI sign-in. Create one with the `clay api-keys create` command — the key is shown only once, so store it somewhere safe.

### What's the difference between MCP for Reps and the CLI/API?

They're separate surfaces, not two halves of one product. The plugin installs Clay's skills and the Clay CLI into your coding agent, and the CLI is what you or your agent run in a shell for one-off runs, scripting, and inspecting data. It authenticates with the session created by `clay login`, so there's no separate key to configure.

MCP for Reps is a different connection, set up separately by an admin for sellers working in chat apps and coding agents. It comes with its own Functions and per-rep credit budgets. See [**MCP in Clay**](https://university.clay.com/docs/mcp-settings) for how that access is configured.

### Can I build or write to Clay tables via CLI or API?

No. The CLI builds logic via Workflows, not tables. `Tables` in the Public API is read-only — you can query and read rows, but not create tables, add fields, or write records.

Basic row reads work on any plan. Structured queries — joins, ranges, and paging past 100 rows — need API table sync, an Enterprise feature. There are no current plans to support table building from the API or CLI.

### Can I build Workflows with the API or CLI?

Yes, Workflows are available from the CLI and plugin in `Beta`. For production use, Clay-managed functions and custom functions are the more stable option.

### Are credit budgets available via the developer platform?

Credit budgets aren't available on the developer platform yet. You can see run-level credit and action consumption from the `Runs` view in Workflows. Credit budget support is on the roadmap.

### Who can approve a device sign-in?

Whoever opens the verification link. They need to be signed in to Clay in that browser and have editor access to at least one workspace, since the sign-in is tied to the workspace they pick, not to the machine running the command. If they don't have editor access anywhere, the page shows `Editor access required` instead of the authorization screen.
