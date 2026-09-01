---
title: Clay API & CLI
description: Access Clay's data and enrichments programmatically with the Clay CLI and Public API — no UI required.
last_synced: 2026-07-09T21:58:04.283Z
---

# Clay API & CLI

Access Clay's data and enrichments programmatically with the Clay CLI and Public API — no UI required.

Clay's Agent Plugin lets you use Clay programmatically — from coding agents, terminals, and backend systems — without working in the UI. With the API and CLI, you can run searches over Clay's GTM dataset, call Clay enrichment functions, and build Workflows, all using Clay's existing integrations and data infrastructure.

**Note:** Clay's Agent Plugin is in open beta. Some capabilities — particularly Workflows — are in an earlier Alpha stage and are actively evolving.

## Getting started

### Install the Clay plugin

Copy and paste this into any coding agent (Claude Code, Codex, Cursor, etc.)

`Set up the Clay plugin by following the steps in <https://github.com/clay-run/agent-plugins>   `

Your agent will install the plugin, put `clay` on its PATH, and sign you in. The same prompt works regardless of which coding agent you use.

**Learn more:** For the full CLI quickstart, Public API setup, code examples, and guides for Searches, Routines, and Workflows, see [developers.clay.com](https://developers.clay.com/).

## What you can do

Agent Plugin has two primary features:

-   **CLI** — Build GTM workflows in natural language from coding agents (including Claude Code, Codex, and Cursor).
-   **Public API** — Access data from Clay or 200+ vendors in the data marketplace. Trigger functions, Claygents, or workflows.

Both paths consume the same credits and actions as equivalent in-product work. There is no additional cost to use the Agent Plugin.

The platform has three core primitives:

-   **Searches** — Find companies and people using structured filters over Clay's GTM dataset. **_Learn more about Searches in_** [**_this video walkthrough_**](https://www.loom.com/share/6a125988c8b14b89aded2e75b8265d5c)**_._**
-   **Routines** — Run Clay-managed functions, custom functions, and Workflows for enrichment, research, scoring, routing, and other repeatable GTM logic. **_Learn more about functions in_** [**_this video walkthrough_**](https://www.loom.com/share/7050c0b62b0648a984d6438112d02985)**_._**
-   **Tables** — Read structured data from known Clay tables. Available on Enterprise plans only.

Note: The CLI and API are currently supported on Mac and Linux. Windows is not supported in open beta.

## Plan availability and limits

The developer platform is available across all Clay plans, including free and trial plans. Clay's Agent Plugin open beta is available on all modern plans and, for a limited time, on legacy plans through the end of 2026.

Search result limits vary by plan:

| Plan | Search results per request | Total search results |
| --- | --- | --- |
| Free | 50 | 100/mo |
| Trial | 50 | 10k per 14 days |
| Paid self-serve plans | 10,000 | 1M/yr |
| Enterprise | 10,000 | 10M/yr |

## FAQs

### Does using the API or CLI cost extra credits?

No. API and CLI calls consume the same credits and actions as the equivalent work done in-product. There is no additional cost because work is triggered via the developer platform instead of the UI.

### What's the difference between the Clay Plugin and the Public API?

The Clay Plugin gives agent environments (Claude Code, Codex, Cursor) both Clay's MCP server and the Clay CLI — the fastest path for agent-first and interactive coding workflows. The Public API is better suited for backend services, queue workers, batch jobs, and custom app integrations where you want direct HTTP access without a CLI layer.

### What's the difference between MCP and the CLI/API?

MCP is used by interactive AI assistants (such as Claude Desktop and ChatGPT) using OAuth for conversational access. The CLI and Public API are designed for programmatic, headless, or automated workflows — including scripts, backend services, and coding agents.

### Can I build or write to Clay tables via CLI or API?

No. The CLI builds logic via Workflows, not tables. The `Tables` primitive in the Public API is read-only and is for querying data that already exists in known Clay tables (Enterprise only). There are no current plans to support table building via the developer platform.

### Can I build Workflows with the API or CLI?

Yes, Workflows are available from the CLI and plugin in Alpha. For production use, Clay-managed functions and custom functions are the more stable option.

### Are credit budgets available via the developer platform?

Credit budgets are not yet available in open beta. You can see run-level credit and action consumption from the `Runs` view in Workflows. Credit budget support is on the roadmap.
