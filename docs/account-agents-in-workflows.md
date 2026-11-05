---
title: Account Agents in Workflows
description: How to add an Account Agent node to a workflow so the agent runs with the account's full Audiences history and the workflow executes on what it decides.
last_synced: 2026-08-25T01:19:30.686Z
---

# Account Agents in Workflows

Run an Account Agent as a node inside a workflow, so a play decides what to do next with the account's full history already in hand.

Account Agents in Workflows lets you drop an Account Agent into a [workflow](https://university.clay.com/docs/workflows) as a node. The agent arrives already knowing the account — past contacts, prior campaigns, deal history, and what it concluded the last time it ran — and the workflow executes on what it decides.

**Note:** Account Agents need Audiences, so this is available on Enterprise, Growth, and Launch plans. If you don't see the `Account Agents` tab when you add an agent node, confirm Audiences is set up in your workspace.

**Cost:** Variable data credits (the same pricing model as Claygent) + 1 action per record the agent processes. Every other node in the workflow is priced under the standard Workflows rules.

## Account Agent or Claygent?

Both run as the same node type, and the picker asks you to choose between them. The difference is whether the decision depends on the account's history.

|  | Claygent | Account Agent |
| --- | --- | --- |
| What it sees | Only the inputs you map into it | The account's full state and history from Audiences |
| Memory | Stateless — one-shot, resets each run | Persistent per account; tracks what changed since its last run |
| Scope | Any record you hand it | One account per run, resolved from the trigger |
| Reach for it when | The answer stands on its own | The decision depends on the account's history |
| Example | Tag an industry, draft a subject line, read a page and return a verdict | Pick the follow-up path given past conversations; re-engage knowing why the deal was lost |

Reach for a Claygent when the answer stands on its own — tagging an industry, drafting a line of copy, reading a page and returning a verdict. Reach for an Account Agent when the answer depends on what came before: which play to run given past conversations, or re-engagement copy that remembers why the deal stalled the first time.

## Before you start

An Account Agent reads the account from Audiences, so the account layer has to exist before the agent can do anything useful.

1.  **Connect your sources in Audiences.** Salesforce, HubSpot, Snowflake, BigQuery, Databricks, or Gong — whatever the agent should reason over. See [Audiences](https://university.clay.com/docs/audiences) to get set up.
2.  **Create an account segment** for the accounts the play should cover. Keep the first one small, in the range of 10 to 25 accounts, so you can read every run while you're still tuning the prompt.
3.  **Spot-check the data.** Open five accounts in that segment and confirm the fields you expect the agent to use are actually populated. A thin account record is the most common reason an agent returns something generic.

## Adding an Account Agent to a workflow

1.  Open your workflow and click `Add`, then choose `Run Claygent` from the `Nodes` section. Account Agents aren't a separate node type — they're a choice you make inside this node.
2.  Connect the node downstream of something that supplies an account. An account segment trigger is the common path, since it hands the agent its account automatically, but the node works anywhere downstream of a step that passes in an account ID. See **Giving the agent account context** below for which triggers work.
    -   `Start with a segment` on the workflows home is the quickest way to a trigger that carries account context. It opens on `People`, so switch to `Companies` and pick an account segment there.
3.  In the node's side panel, switch to the `Account Agents` tab and pick an existing agent in your workspace. To build a new one instead, click `Create` and choose `Create Account Agent`, which opens the agent builder. `See all agents` opens the full list when the recent ones aren't enough.
4.  Confirm the node is bound to an Account Agent. The `Account Agent` section at the top of the panel reads `This is an Account Agent` and lists the sources it can reach. In `Inputs`, `Account ID` fills itself in from the trigger's ID — that auto-wiring is the second confirmation that account context resolved.
5.  Check the agent's `Outputs`. These are the fields the agent returns, each with a type — this is what your downstream nodes will branch on, so it's worth reading before you wire anything up.
6.  Wire the downstream path.
    -   Note: A single action node after the agent is enough when the play always does the same thing. For routing, put a `Conditional` on the agent's decision field and the action nodes on each branch.
7.  Test on one record with a `Run manually` trigger, then open the run and confirm the agent used the data you expected before you scale the segment.

<div style="background-color:#F0FDF4; padding:16px; border-radius:8px; border:1px solid #D2F0DB; font-family:Arial, sans-serif;"><h3 style="margin:0 0 12px 0; font-family:Arial, sans-serif; font-size:16px;">Add an Account Agent to a workflow</h3><div style="position:relative; padding-bottom:56.25%; height:0;"><iframe src="[https://www.loom.com/embed/79e32a3166844bb6a80cb5164fa4ce16](https://www.loom.com/embed/79e32a3166844bb6a80cb5164fa4ce16)" frameborder="0" webkitallowfullscreen mozallowfullscreen allowfullscreen style="position:absolute; top:0; left:0; width:100%; height:100%;"></iframe></div></div>

### Building it from a prompt

Sculptor can also build the whole play from a description. Ask for it from the prompt box at the top of the workflows home — _build me a workflow that sends a Slack message with the next best action for an account among my top accounts_ — and it comes back with a couple of questions before it starts: which segment should trigger the run, and which connected account should send the message.

Two things to expect. It takes a few minutes on a workflow this size, and the graph it produces often looks different from one you'd wire by hand — different node names, sometimes a different shape for the same result. While you're still learning what each node does, building manually is the faster way to see what you're getting; once you know, the prompt is quicker.

### Upgrading a Claygent you already have

If you've already got a Claygent with a prompt that works, you can turn it into an Account Agent from the node. Select the Claygent, then in the `Account Agent` section click `Upgrade` and confirm on `Upgrade to Account Agent?`.

This creates a _new_ Account Agent as a copy and repoints the node at it. Your original Claygent isn't modified, so it keeps working everywhere else you use it. The copy is permanently an Account Agent — it can't be turned back — so if you want both, you already have both.

## Giving the agent account context

Account context from Audiences is what makes the node an Account Agent rather than a Claygent, and it's resolved by tracing the node back to the trigger that started the run. That tracing is what decides whether the agent knows which account it's looking at, so the trigger you pick matters more here than anywhere else in Workflows.

| Trigger | Carries account context | Use it for |
| --- | --- | --- |
| New member in segment | Yes, on an account segment | Plays that fire as accounts meet a condition. The default choice. |
| Segment on a schedule | Yes, on an account segment | Recurring passes over a whole segment, like a nightly re-score. |
| Run manually | For testing | Single-record testing while you build. |
| On a signal | No | Build a segment where the signal is true and trigger on segment membership instead. |
| On webhook call | No | Events originating outside Clay. Supply the account yourself in an earlier step. |
| On a schedule | No | Standalone jobs not bound to a segment. |
| On CSV upload | No | One-off lists pushed through an existing workflow. |

Three rules to design around:

-   **The trigger has to be on accounts, not contacts.** A segment trigger built on a contact segment won't resolve account context, even though it's an Audiences trigger. Use an account segment.
-   **Keep one trigger node upstream of the agent.** When more than one trigger node can reach the agent, Clay can't tell which one supplied the account, and context won't resolve. Split the entry points into separate workflows instead.
-   **To act on a signal, make the signal a segment.** Build a segment where the signal is true and trigger on `New member in segment`, so entering the segment _is_ the event. The `On a signal` trigger doesn't carry account context today.

The agent doesn't have to sit directly next to the trigger. You can put enrichment or code steps in between and the agent will still resolve the account, as long as there's only the one trigger node upstream of it.

### Starting from an event outside Clay

An account segment trigger hands the agent its account automatically. When the play has to start somewhere else — an inbound form fill landing on a webhook, say — you resolve the account yourself instead: look it up in Audiences in an earlier step, then map that account's ID into the agent node's account input.

That's the shape of a typical inbound play. The webhook starts the run, a lookup step resolves the lead to an account, and the agent picks it up from there with full history. The only difference from a segment-triggered play is that you're supplying the account rather than letting the trigger supply it.

## Working with the agent's output

The agent's conclusions come back as its output fields, readable by any downstream node in the same run the way any other node's output is. Because those fields are the agent's fields on the account, the same conclusions are available in Audiences rather than living only inside the run — which is what lets the next play read what this one decided.

A few habits make the downstream wiring much easier:

-   **Ask for discrete, typed fields rather than one block of prose.** A decision, a reason, and any drafted copy as three separate outputs means a conditional can branch on the decision while the reason and the copy ride along into the notification. One freeform output forces you to parse it back apart in a code step.
-   **Pin anything that has to be exact.** For a score, an ID, or a boolean, point the downstream reference at the agent node and field so the value is copied verbatim rather than model-filled.
-   **Branch after the agent, not before it.** A trigger connects to exactly one node, so in this pattern the agent is that node and all branching happens downstream of it.

Every node's inputs, outputs, timing, and cost per record show up in the workflow run, and the agent's reasoning sits in the same trace. When a play routes an account somewhere surprising, open the run, find the data point the agent used, and adjust the prompt from there. Runs are deep-linkable, so a surprising one can be shared the way you'd share a table URL.

### Routing to more than one action

When the play should do different things for different accounts, the agent's output fields become the routing variables. Design the output schema and the routing rules together, since what the agent emits is what the `Conditional` reads.

A three-way play makes the shape concrete: the agent returns one field per path — send the email, send a message instead, or the contact still needs an email address — alongside the recipient and the drafted copy. The `Conditional` reads those flags with `Rules`, evaluated top to bottom so the first match wins, and ends the run when none of them match. Each branch is then an ordinary action node: add the contact to a sequencer, post the message, or enrich the person for an email address and add them after.

-   **Let Clay wire the mappings.** `Suggest input mappings` on the conditional detects the agent's outputs and maps them for you. To do it by hand, type `/` in a field to open a picker of every upstream node and its output fields.
-   **Put the guardrails in the prompt, not just in the routing.** When an agent can start outbound, spell out in its prompt what should stop a send — an open opportunity you don't want to cut across, an account flagged as a competitor — and ask for the reasoning on both the true and the false case. The conditional routes on the flag; the prompt is where you decide what the flag means.

### Route the agent's decision to three actions

## FAQs

### How is this different from an Account Agent in Audiences?

An Account Agent in Audiences keeps a data point true about every account, all the time — an account health score, an ICP tier, a closed-lost reason — on a schedule, written back as a field you can export anywhere. An Account Agent in a workflow answers a narrower question: something happened, what's the right response right now. Most teams run both, with the Audiences agent keeping the account layer current and the workflow reading that layer and acting on it. See [Account Research Agents](https://university.clay.com/docs/account-research-agents) for the Audiences side.

### Which model does the agent use?

Account Agents run on a Clay-selected model rather than one you choose per agent. If the agent you picked has a model set on it from elsewhere, that setting is ignored when it runs as an Account Agent. One consequence worth knowing: if the agent has MCP connections configured and the selected model doesn't support them, the node fails rather than running without those tools — remove the MCP tools from the agent to clear it.

### Can the agent act on accounts it discovers mid-run?

Not today. The agent reasons over accounts that are already in Audiences, so anything the play touches needs to be in your account layer first. If the accounts you want aren't there yet, import them into Audiences and let the segment trigger pick them up.

### Why is the node asking me for an Account ID?

`Enter or map a valid Account ID.` means nothing upstream has told the agent which account to work on. If you meant to trigger from a segment, check the trigger: either it isn't an account segment trigger, or more than one trigger node can reach the agent. Fix that and the field fills itself in.

If the play starts from a webhook or another non-segment trigger, this message is expected and it's your cue to supply the account — resolve it in an earlier step and map that ID in here.

### The agent ran but the output is generic. What happened?

Nearly always thin data rather than a thin prompt. Confirm the node's `Account Agent` section reads `This is an Account Agent`, then open one of the accounts in Audiences and look for the specific data you expected the agent to reason over. If the Gong calls, deal history, or usage fields aren't populated on the record, the agent has nothing to work from and will fall back to something generic.

### Is there a spending cap on the agent inside a workflow?

Not yet — the credit controls built for Account Agents in Audiences don't extend to a workflow run, which goes through a different execution path. Scale the segment in steps rather than all at once and read the per-node cost in the run trace between passes. A fast-changing segment is the case worth planning around: a bulk import that touches thousands of records fires thousands of runs at once, so for a high-churn segment `Segment on a schedule` gives you the same coverage at a pace you set.
