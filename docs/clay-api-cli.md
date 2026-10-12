---
title: Clay API & CLI
description: Access Clay's data and enrichments programmatically with the Clay CLI and Public API — no UI required.
last_synced: 2026-08-06T01:44:05.562Z
---

# Clay API & CLI

Access Clay's data and enrichments programmatically with the Clay CLI and Public API — no UI required.

Clay's Agent Plugin lets you use Clay programmatically — from coding agents, terminals, and backend systems — without working in the UI. With the API and CLI, you can run searches over Clay's GTM dataset, call Clay enrichment functions, and build Workflows, all using Clay's existing integrations and data infrastructure.

**Note:** Clay's Agent Plugin is in open beta. Some capabilities — particularly Workflows — are in an earlier Alpha stage and are actively evolving.

## Getting started

### Install the Clay plugin

Tell any coding agent to set the plugin up for you — Claude Code, Codex, Cursor, or anything else. Copy this prompt:

`Set up the Clay plugin by following the steps in <https://github.com/clay-run/agent-plugins`\>

Your agent will install the plugin, put `clay` on its PATH, and sign you in.

### Setup guide

### Signing in without a browser

`clay login` authorizes the CLI by opening a browser on the same machine, which isn't possible in SSH sessions, containers, CI runners, headless machines, or internal deployment frameworks that can't receive a local redirect. In those environments, run `clay login --device` instead — it uses the standard OAuth 2.0 device authorization flow (RFC 8628), so you can approve the sign-in from a browser on any other device.

1.  Run `clay login --device`. The CLI prints a verification link with your code pre-filled, prints the code on its own, and then waits for approval. In an interactive terminal it also attempts to open that link in the machine's default browser; when it runs inside an agent's shell tool or a piped process, it only prints the link.
2.  Open the link in a browser on any device, and sign in to Clay if you aren't already.
    -   If you enter the verification URL without the code, Clay shows `Connect a device` — type the code from your terminal into the `Code` field and click `Continue`.
3.  On `Connect Clay CLI`, check that the code on screen matches the one in your terminal, choose a workspace under `Which workspace should Clay CLI connect to?`, and click `Authorize`. To reject the request, click `Deny`.
4.  The browser confirms `Device connected` and the CLI finishes signing in on its own — there is nothing to paste back into your terminal.

**Note:** The code expires 10 minutes after the CLI prints it, and it can only be approved once. If it expires before you approve it, or you deny the request, run the command again to get a new code.

For the full CLI quickstart, Public API setup, code examples, and guides for Searches, Routines, and Workflows, see [**developers.clay.com**](https://developers.clay.com/).

## What you can do

Agent Plugin has two primary features:

-   **CLI** — Build GTM workflows in natural language from coding agents (including Claude Code, Codex, and Cursor).
-   **Public API** — Access data from Clay or 200+ vendors in the data marketplace. Trigger functions, Claygents, or workflows.

Both paths consume the same credits and actions as equivalent in-product work. There is no additional cost to use the Agent Plugin.

The platform has three core primitives:

-   **Searches** — Find companies and people using structured filters over Clay's GTM dataset. Learn more about Searches in [this video walkthrough](https://www.loom.com/share/6a125988c8b14b89aded2e75b8265d5c).
-   **Routines** — Run Clay-managed functions, custom functions, and Workflows for enrichment, research, scoring, routing, and other repeatable GTM logic. Learn more about functions in [this video walkthrough](https://www.loom.com/share/7050c0b62b0648a984d6438112d02985).
-   **Tables** — Read structured data from known Clay tables. Available on Enterprise plans only.

**Note:** The CLI and API are currently supported on Mac and Linux. Windows is not supported in open beta.

## Plan availability and limits

The developer platform is available across all Clay plans, including free and trial plans. Clay's Agent Plugin open beta is available on all modern plans and, for a limited time, on legacy plans through the end of 2026.

Search result limits vary by plan:

**PlanSearch results per requestTotal search results**Free50100/moTrial5010k per 14 daysPaid self-serve plans5001M/yrEnterprise50010M/yr

## FAQs

### Does using the API or CLI cost extra credits?

No. API and CLI calls consume the same credits and actions as the equivalent work done in-product. There is no additional cost because work is triggered via the developer platform instead of the UI.

### What's the difference between the Clay Plugin and the Public API?

The Clay Plugin gives agent environments (Claude Code, Codex, Cursor) both Clay's MCP server and the Clay CLI — the fastest path for agent-first and interactive coding workflows. The Public API is better suited for backend services, queue workers, batch jobs, and custom app integrations where you want direct HTTP access without a CLI layer.

### What's the difference between MCP and the CLI/API?

Within the plugin, the MCP server is a local process (`clay mcp`) that your coding agent spawns and calls as part of its normal tool-use loop; the CLI is what you or your agent run in a shell for one-off runs, scripting, and inspecting data. Both authenticate with the same session created by `clay login`, so there is no separate key to configure. The MCP server resolves that session once at startup, so restart your agent after signing in — an already-running server won't pick up a new sign-in, and it stays pinned to the workspace it launched with.

### Can I build or write to Clay tables via CLI or API?

No. The CLI builds logic via Workflows, not tables. The `Tables` primitive in the Public API is read-only and is for querying data that already exists in known Clay tables (Enterprise only). There are no current plans to support table building via the developer platform.

### Can I build Workflows with the API or CLI?

Yes, Workflows are available from the CLI and plugin in Alpha. For production use, Clay-managed functions and custom functions are the more stable option.

### Are credit budgets available via the developer platform?

Credit budgets are not yet available in open beta. You can see run-level credit and action consumption from the `Runs` view in Workflows. Credit budget support is on the roadmap.

### Who can approve a device sign-in?

Whoever opens the verification link. They need to be signed in to Clay in that browser and have editor access to at least one workspace, since the credential is issued for the workspace they choose rather than for the machine running the CLI. If they don't have editor access anywhere, the page shows `Editor access required` instead of the authorization screen.

### What if my shell tool times out before the sign-in is approved?

`clay login --device` waits up to 10 minutes for approval, while the browser sign-in waits up to 5. If your agent's shell tool has a shorter timeout, have it run the sign-in in the background and poll `clay whoami` until that succeeds — or run `clay login --device` yourself in a terminal and let the agent pick up from there.

### Does device login store the credential differently from the browser sign-in?

No. Both flows validate the credential with Clay before writing anything to disk, then store it in the CLI's config file — `~/.config/clay/config.json` by default, or `clay/config.json` inside the directory named by `CLAY_CONFIG_HOME` or `XDG_CONFIG_HOME` when either is set. `clay whoami` and `clay logout` behave the same either way, and signing in again replaces the stored credential, which is also how you switch workspaces.
