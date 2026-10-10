---
title: Account Research Agents
description: Account Research Agents are always-on agents that run across every account in an Audience segment, synthesizing CRM data, call transcripts, and signals into agent-managed fields that can sync to your CRM or data warehouse.
last_synced: 2026-07-22T05:45:57.101Z
---

# Account Research Agents

Account Research Agents are always-on agents that run across every account in an Audience segment, synthesizing CRM data, call transcripts, and signals into agent-managed fields that can sync to your CRM or data warehouse.

Account Research Agents are Clay's always-on agents built on [**Audiences**](https://university.clay.com/docs/audiences) — they run across every account in a segment, synthesizing CRM data, call transcripts, and signals into structured, auditable fields. These fields can be written back to your CRM or data warehouse, or used to trigger plays. Unlike a Claygent in a table, Account Research Agents come pre-configured with context, scheduling, and enrichment built in, and maintain persistent memory per account — so intelligence compounds across runs rather than resetting after each run.

**Note:** Account Research Agents are in open beta.

**Cost:** Variable credits (same pricing model as Claygent) + 1 action per record processed. During open beta, Account Research Agents are available on any plan with access to Audiences — Enterprise, Growth, and Launch.

## **Setting up Account Research Agents**

**Note:** Audiences must be set up before you can create an Account Research Agent. This means connecting at least one data source — Salesforce, HubSpot, Snowflake, BigQuery, Databricks, or Gong — and having at least one Audience segment defined.

1.  In `Audiences`, connect your data sources. Import your CRM, data warehouse, and Gong — the import wizard walks through field mapping. If you haven't done this yet, click `Add data` from anywhere in Audiences to get started. See [**Setting up Audiences**](https://university.clay.com/lessons/setting-up-audiences) for a full walkthrough.
2.  Create an Audience segment for the accounts you want the agent to run over — for example, high-signal expansion accounts or a closed-lost cohort.
3.  Open the segment and click the `Claygents` button in the top right. This opens [**Claygent Builder**](https://www.clay.com/university/guide/claygent-builder), where you configure your Account Research Agent. Just describe what you want (e.g., `build me an agent to analyze closed-lost opportunities`) to [**Sculptor**](https://www.clay.com/university/guide/sculptor), our AI copilot, and it generates the prompt and output fields for you. From here you can also configure what tools, functions, and context the agent has access to.
4.  Before running across the whole segment, click `Test` to try the agent on a few sample records in the builder, and review the `Total cost estimate` in the run modal so you don't spend credits unexpectedly. Then save the agent and run it against the segment. Once complete, click into any account to inspect its agent-managed field outputs and the reasoning behind each one.

## **Agent-managed fields**

An agent-managed field is an output the agent maintains per account over time. You define which fields you want and the agent populates and updates them as context evolves. Common examples include:

-   **Closed/lost reason**: Captures the real reason an account said no, so re-engagement campaigns can be built off substance instead of guesswork.
-   **Engagement summary**: Gives any rep — including one picking up an account after a handoff — full relationship history without digging through old email threads.
-   **Usage / expansion signals**: Surfaces the moment usage crosses a threshold, so expansion plays don't wait on someone remembering to check a dashboard.
-   **Account health / churn risk**: Flags early warning signs — a usage drop, a failed payment, a delayed shipment — before they turn into churn, so the team can step in while there's still time to act.

Every time a field updates, it's written back into Audiences. From there, you can sync those fields to your CRM or data warehouse (human-approved) — so your account data stays current without relying on rep updates or quarterly cleanup sprints. Each field also carries the agent's reasoning, so you can see what it read and why it updated a value rather than receiving a black-box answer. Bringing your own model API key isn't supported during open beta — the agent runs on a Clay-provided model chosen for you.

## **Monitoring agents from the Data hub**

Every agent's activity lives in the `Data hub` in Audiences, under the `Claygents` tab — it appears once you've configured an agent on an account Audience. From there you can:

-   **See what's running at a glance.** Each agent lists its `Run cadence`, the Audience segment it runs over, its `Credit spend`, and a `Status` of `Running`, `Active`, or `Configured`.
-   **Review any run.** Click into an agent to see each run it's made — marked `Completed`, `Running`, `Failed`, or `Canceled` — then open a run to inspect it record by record. Each row shows the record's `Status`, the `Time`, the `Credits` it cost, and an `Open record` link to the account it touched, filterable to just `Errors` or `Success`.
-   **Trace any decision.** Opening a record takes you to that account's agent-managed fields and the reasoning behind each, so you can trace any single value back to the data the agent read and why it landed where it did.

## **FAQs**

### **Do I need Audiences set up before I can use Account Research Agents?**

Yes. Account Research Agents run on [**Audiences**](https://university.clay.com/docs/audiences). You need at least one data source connected (CRM, Gong, or a data warehouse) and a defined Audience segment before creating your first agent. See [**Audiences FAQs and best practices**](https://university.clay.com/docs/audiences-faqs-and-best-practices) for help getting set up.

### **How is an Account Research Agent different from a Claygent in a table?**

A Claygent in a table looks up one record at a time and resets after each run — you configure which specific field or source it checks, and it only finds what you tell it to look for. An Account Research Agent fetches whatever's relevant on its own (a Gong call, a CRM field, a funding signal) without you wiring up a lookup per field — which means it can catch things you didn't know to ask about. It also runs across every account in a segment at once, with no per-field lookups to configure and no cell size limit, and maintains persistent memory per account so context builds over time rather than starting fresh on every run.

|  | Claygent in a table | Account Research Agent |
| --- | --- | --- |
| Scope | One record at a time, in a table cell | Every account in an Audience segment at once |
| What it retrieves | Only the field or source you configure per column | Fetches whatever's relevant on its own — a Gong call, a CRM field, a funding signal — across all connected data |
| Memory | Resets after each run | Persistent memory per account; context compounds across runs |
| Setup | A lookup wired up per field | Pre-configured with context, scheduling, and enrichment — you set the output fields |
| Limits | Bound by cell size | No cell-size limit; built for whole-book volume |
| Freshness | Current only when you rerun it | Re-runs on a schedule or trigger to stay current as new signals arrive |
| Output | Values in table cells | Agent-managed fields written back to Audiences → CRM/data warehouse (human-approved), each with the agent's reasoning |
| Example | "Does this account have a recent funding round, right now, for a call this afternoon?" | "Score every account for expansion readiness and keep it re-scored as new signals arrive" |

### **How is this different from a one-time enrichment run?**

A one-time enrichment fires once and goes stale. An Account Research Agent re-runs on a set schedule, when an account enters the Audience segment, or whenever you run it manually — picking up new signals like a Gong call, a title change, or a product usage event, and accumulating context per account. Intelligence compounds over time rather than resetting with every pull.

### **Who sets up an Account Research Agent vs. who uses it?**

RevOps typically sets it up: connecting data into Audiences, defining the segment, and configuring the agent's output fields and instructions. Reps consume the outputs — pre-populated account context ahead of calls, with the reasoning behind each field already attached.

### **What happens when a new signal comes in?**

When the agent runs and finds a new signal in Audiences — a Gong transcript, a contact role change, a product usage event — it reads that signal alongside the full existing account context, evaluates whether any agent-managed field has changed, synthesizes the updated value if so, and writes it back to Audiences. That update then syncs to your CRM or data warehouse once approved.

### **What plan do I need?**

During open beta, Account Research Agents are available on any plan with access to Audiences — Enterprise, Growth, and Launch.

### **How much does it cost?**

Account Research Agents use variable credit pricing (the same model as Claygent) plus 1 action per record processed by the agent. See [**How AI is priced**](https://university.clay.com/docs/ai-pricing) for credit rates by model.
