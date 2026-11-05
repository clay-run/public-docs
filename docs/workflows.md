---
title: Clay Workflows
description: Build graph-based automations with Claygent, enrichment, and Gate (Conditional) nodes. Covers triggers, how Gate nodes route records, and the fixed Default branch.
last_synced: 2026-08-11T00:00:00.000Z
---

# Clay Workflows

Clay Workflows is a visual automation builder where you connect nodes into a directed graph. A record enters through a trigger and moves through connected nodes — AI agents, enrichments, and routing decisions — until the workflow ends.

## Node types

| Node type | What it does |
| --- | --- |
| **Claygent (agent) node** | Runs an LLM with a prompt for reasoning, drafting, classifying, or summarizing |
| **Send / Enrich (tool) node** | Runs a single Clay action — an enrichment, HTTP call, or CRM write |
| **Gate (Conditional) node** | Routes each record to exactly one outgoing branch |
| **Trigger node** | Defines how the workflow starts — audience segment, schedule, webhook, or Clay table |

## Gate nodes (routing logic)

A Gate node routes each incoming record to exactly one outgoing path. In the workflow canvas, the node is labeled **"Gate: [description]"** — for example, "Gate: Outreach vs Instantly".

**How a Gate node works:**

1. A record enters the Gate node.
2. The node evaluates its routing rules in order, top to bottom.
3. The record is sent down the **first matching rule's** path.
4. If no rule matches, see **The Default branch** below.

### The Default branch

Every Gate node always includes a **Default** branch, shown last on the canvas. The Default branch cannot be removed and its label cannot be renamed — "Default" is fixed on all Gate nodes.

**What happens when no rule matches** depends on one setting inside the Gate node:

- **"End run when no rule matches" unchecked** (the default): records that match no rule are sent down the Default path. You can connect any downstream node to the Default branch — a manual review step, a catch-all action, or leave it unconnected to end the run for that record.
- **"End run when no rule matches" checked**: the run stops immediately for that record and the Default path is not followed.

To change this setting, open the Gate node's configuration panel.

### Routing modes

| Mode | Use when |
| --- | --- |
| **Rules** (recommended) | Branching on specific field values — equality, comparison, contains, empty/not-empty |
| **Agentic** | The routing decision requires open-ended reasoning (for example, "classify this as billing, technical, or general") |
| **Code** | You need to compute or transform a value to decide the route |
