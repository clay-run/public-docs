---
title: Clay MCP for Reps vs. Agent Plugin
description: Explains how to choose between MCP for Reps, which brings approved workflows to sellers in their AI tools, and the Clay Agent Plugin, which gives builders Clay's skills and CLI inside coding agents.
last_synced: 2026-09-15T15:07:09.649Z
---

# Clay MCP for Reps vs. Agent Plugin

Choose between MCP for Reps and the Clay Agent Plugin based on who will be using it and how much your ops team needs to approve in advance.

Clay gives you two ways to work with your workspace outside the Clay app. MCP for Reps brings Clay's data and your team's approved workflows into the AI tools sellers already use, and the Clay Agent Plugin gives builders Clay's skills and the `clay` CLI inside their coding agent.

## Quick reference

|  | MCP for Reps | Clay Agent Plugin |
| --- | --- | --- |
| Built for | AEs, SDRs, and CSMs | RevOps, GTM engineers, and developers |
| Runs in | Claude, ChatGPT, Microsoft Copilot, Glean, Claude Code, and Codex | Coding agents — Claude Code, Codex, and Cursor — on Mac and Linux |
| What you get | Contact and company search, enrichment, account questions, and the Functions your team enables | Clay's skills and the clay CLI, plus the Public API |
| Who sets it up | An admin enables access and invites each rep; the rep adds the connection in their AI tool | The person installs it in their own coding agent and signs in |
| Governance | An admin decides which Functions a rep can run, their permission type, and their credit budget | Follows the person's own workspace permissions |
| Typical work | Running approved research and outreach prep inside a conversation | Building and running Searches, Routines, and Workflows |

## Choosing between them

The reliable signal is the person's job, not which surface is more capable.

-   **They run plays other people built.** MCP for Reps. The rep prompts in their AI tool, and what they can reach is what your ops team approved.
-   **They build the plays.** The Clay Agent Plugin. It puts Clay's skills and the `clay` CLI in their coding agent, so they can compose new logic rather than only invoke it.
-   **They need Clay inside a backend job, internal tool, or product feature.** The Public API, which comes with the plugin, rather than either interactive surface.

One thing trips people up here: the AI tool someone is sitting in doesn't settle it. MCP for Reps connects from coding agents as well as chat apps, so a rep and a GTM engineer can both be working in Claude Code and still need different surfaces.

## MCP for Reps

MCP for Reps is the access layer that brings Clay's workflows and go-to-market context into the AI tools reps already use. Setup has two halves: an admin enables access, invites each rep, and chooses which Functions and credit budget they get, and each rep then adds the connection in their own AI tool. You can get started at [**clay.com/mcp**](https://www.clay.com/mcp).

What reps do with it:

-   **Prospect net-new leads** with a reason to reach out attached to each one.
-   **Ask account questions in natural language** instead of assembling the answer across several tools.
-   **Draft outreach grounded in enrichment data** rather than in whatever the model already knows.
-   **Prepare for meetings** with a briefing per account.
-   **Run a Function your ops team built** from a single prompt.

**Note:** Credit controls and usage monitoring are available on modern paid plans and Legacy Enterprise. The Audiences controls — which let reps query the accounts they own and the opportunity data behind them — are an Enterprise feature, and the meeting-prep use case depends on them. Reps in a workspace without Audiences still get contact and company search plus any Functions you have enabled.

Where to go next:

-   [**MCP in Clay**](https://university.clay.com/docs/mcp-settings) — the admin side: permission types, credit budgets, Functions, and the Audiences controls.
-   [**Connect to Clay MCP**](https://university.clay.com/docs/connect-to-clay-mcp) — what to send reps so they can add the connection themselves.
-   [**Roles and permissions**](https://university.clay.com/docs/roles-and-permissions#sales-rep) — what the `Sales rep` permission type can and can't reach.
-   [**MCP security and privacy**](https://university.clay.com/docs/mcp-security-privacy) — how workspace data is handled once a rep connects.
-   [**MCP — Troubleshooting & FAQ**](https://university.clay.com/docs/mcp-troubleshooting-and-faqs) — connection errors and Function configuration problems.
-   Courses for both sides: [**Clay MCPs for reps**](https://university.clay.com/courses/clay-mcps-for-reps) and [**Clay MCP for ops**](https://university.clay.com/courses/clay-mcp-for-ops).

## The Clay Agent Plugin

The Clay Agent Plugin is a headless way to build in Clay. It installs Clay's skills and the `clay` CLI into your coding agent, so you can create and run enrichment and end-to-end workflows without opening the Clay app — and results land back in Clay, where the rest of your team can see them. You can get started at [**clay.com/agent-plugin**](https://www.clay.com/agent-plugin).

What builders do with it:

-   **Source a total addressable market** across 200+ data providers, with waterfall logic validating emails and phone numbers.
-   **Build prospect lists that call your existing functions, Workflows, and Claygents**, so the agent reuses centrally governed logic instead of rebuilding one-offs.
-   **Automate workflows described in natural language**, with run observability staying in the Clay app.
-   **Read and segment Audiences** — your workspace's own people, companies, and deals — from the terminal.
-   **Wire Clay into a backend job, internal tool, or product feature** using the Public API and a Clay API key.

**Note:** The Clay Agent Plugin installs Clay's skills and the `clay` CLI. It does not include an MCP server, so installing the plugin doesn't give your coding agent the MCP for Reps toolset — that connection is set up separately.

A few boundaries are worth knowing before you plan around the plugin:

-   The CLI reads and segments Audiences rather than writing to it, so there's no command that sets a field value on a record, imports records, or uploads a CSV.
-   Campaigns stay in the Clay app — the plugin won't launch, pause, or resume one.
-   `clay tables query` reads data that already exists in known Clay tables, and it needs API table sync, which is an Enterprise feature.
-   Mac and Linux are supported. Windows isn't yet.

Where to go next:

-   [**Clay Agent Plugin (API & CLI)**](https://university.clay.com/docs/clay-api-cli) — install, sign-in, and the per-plan search limits.
-   [**developers.clay.com**](https://developers.clay.com/) — the CLI quickstart, Public API setup, code examples, and guides for Searches, Routines, and Workflows.
-   [**CLI security and privacy**](https://university.clay.com/docs/cli-security-privacy) — how the CLI handles your credentials and data.
-   [**Audiences for agents and the CLI**](<https://Audiences for agents and the CLI>) — the `clay audiences` command reference.

## FAQs

### What happens if someone has both connected in the same coding agent?

The two surfaces expose overlapping tools, so an agent with both connected can reach for the wrong one — calling a rep search when the `clay` CLI was the better fit for the job. The plugin ships instructions telling the agent to leave the rep tools alone, so the plugin's own path wins where they overlap. They aren't designed to run side by side, though, so it's cleaner to give each person only the surface their work needs.

### If the plugin can do more, why would a rep use MCP for Reps?

Capability isn't the deciding factor — governance is. The plugin gives a person their own Clay access, so they can build new logic as well as run it, and nothing narrows which logic they reach for. MCP for Reps inverts that: your ops team builds and approves the logic, and the rep runs it from a prompt.

Ops also gets to shape what that logic costs. A Function can check your CRM for a phone number before it spends anything on a vendor, and reps calling it inherit that decision without having to know it was made.

### Can a rep build their own Function?

No — Functions are built in the Clay app by someone with workspace access, then exposed to reps by turning on the function's `MCP for reps` surface. That's the split the rep surface is designed around: your ops team decides what the logic does, and reps decide when to run it. If the person asking wants to build the logic themselves, they want the plugin, and they'll need more than the `Sales rep` permission type.

### Which one gives us tighter control over credit spend?

MCP for Reps. An admin sets a monthly credit budget per rep from `Settings → MCP users`, and a rep who reaches their cap is blocked until the next reset, which an admin can lift by raising the limit. The plugin doesn't carry per-person credit budgets; you see consumption after the fact from the `Runs` view in Workflows.

Neither surface adds a surcharge. Work costs the same credits and actions as the equivalent work done in the Clay app.

### Do we have to pick one for the whole workspace?

No — both are assigned per person. You give the `Sales rep` permission type to the people who should have MCP-only access, and anyone with their own Clay access can install the plugin. Plenty of teams run both, with ops and GTM engineers on the plugin and the sellers they support on MCP for Reps.
