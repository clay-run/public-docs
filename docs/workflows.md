---
title: Workflows
description: Overview of Clay Workflows, the graph-based orchestration layer for building trigger-driven, per-record automation with branching, conditions, and actions.
last_synced: 2026-08-11T16:37:56.237Z
---

# Workflows

Build a graph of connected steps that starts on a trigger, branches on your logic, and acts on one record at a time.

Workflows is Clay's primary orchestration layer. A workflow is a graph of connected nodes that a trigger starts. It runs once per record or event — where a table enriches a list row by row, a workflow moves a single record along a path, with branching, conditions, and logic on the way.

**Note:** Workflows is in open beta, and you turn it on by enrolling your workspace in the beta program from your workspace settings. If you don't see `Workflows` in the left sidebar under `Orchestration`, check your enrollment there first. Your Growth Strategist or Clay support can help if it still doesn't appear.

### What Workflows is

Common things people build:

-   **Inbound lead qualification and routing** — enrich a form submission, score it, and send it to the right rep.
-   **Signal-based outbound** — start from an intent signal, research the account around it, and fire the play once the full picture qualifies.
-   **Account-based marketing** — qualify accounts into a coordinated multi-channel play instead of working from a static named-account list.

## Building a workflow

Workflows lives under `Orchestration` in the left sidebar. Three surfaces build the same thing, so you can start in one and continue in another.

**Already using Clay tables?** `Import a table` on the empty canvas is the fastest way in. Clay scaffolds the graph from the table's schema, so your columns arrive as steps and you start from something that already matches your data rather than describing a workflow from scratch.

**From your terminal or a coding agent.** The Clay CLI and agent plugin create workflows, edit steps, look up actions and their input schemas, test runs, inspect them step by step, and manage version history — and they print JSON, so they script cleanly.

Workflows is the Clay surface built for this; tables can't be created through the API or CLI. See [Clay API & CLI](https://university.clay.com/docs/clay-api-cli) for installing the plugin and signing in.

### Build a workflow from the CLI

**With the in-app assistant.** Sculptor sits in a side panel in the workflow editor and builds or edits the graph from a description of what you want. It runs in a live session, so stay on the page while it works — navigating away ends the session. It tends to reach for `Run Claygent` steps, so read what it produces before you publish.

### Build a workflow with Sculptor

**On the canvas.** Click `Workflows` → `New workflow`. Clay creates it as `Untitled workflow` and drops you straight onto the canvas with the name selected, so you can rename it and start building.

The empty canvas offers three ways in — `Start with a trigger`, `Start with segment`, or `Import a table` to scaffold the graph from a table's schema. From there, open the node palette with `Add` to pick from `Triggers` and `Nodes`, or drag out from a node's handle, then connect steps by drawing an edge between them.

**Who can do what.** Workspace members can create, edit, and run workflows, and deleting one is admin-only. `Integrations` in workflow settings is the section that exposes a workflow as a routine, so it can be called from `API & CLI` or as a tool inside a Claygent. Everyone can see that section, but changing what it exposes takes permission to manage workspace access.

## Triggers

Every workflow starts at its trigger node: it defines the run's initial input, and it's the only step with nothing upstream of it. Click the node to open `Choose trigger`, and add more than one if the same logic should fire from several places.

Some triggers depend on your plan. `On webhook call`, `New member in segment`, and `Segment on a schedule` stay visible on a plan that doesn't include them, but show an `Upgrade` badge in place of the option to add them.

-   `Run manually` — you click `Run workflow` and supply the input, so the trigger needs a defined input schema before a manual run becomes available. Best for testing on one record or a small batch while you build. This is also the trigger behind a workflow called from the CLI or from a Clay table. A workflow that starts from a segment can't be run manually.
-   `New member in segment` — one run for each record that joins an audience segment, and optionally each time a record already in the segment changes. Best for plays that should fire as soon as a contact or account meets a condition, like routing a new inbound lead. To act on a signal, build a segment where that signal is true, so entering the segment is the event.
-   `Segment on a schedule` — reruns the workflow for every member of a segment on a schedule you set. Best for recurring passes over a whole segment, like a nightly re-score.
-   `On a schedule` — runs on a recurring schedule that isn't tied to a segment. Best for a standalone job, like a daily digest.
-   `On webhook call` — Clay generates a URL, and each POST to it becomes a run. Best when the event starts outside Clay, like a form submission. Define the payload by pasting a sample JSON body or a cURL command and Clay infers the input schema, then copy the URL and a ready-made cURL from the trigger card.
-   `On CSV upload` — a run for each row of a file you upload. Best for a one-off list you want to push through a workflow you already have.

## Node types

| Node | What it does | When to use it | Cost |
| --- | --- | --- | --- |
| Run enrichment | Runs one Clay action, like finding an email, enriching a company, or writing to a CRM | Any single data lookup or external action | 1 action + credit cost of enrichment |
| Run function | Calls a reusable Clay function | Reusing governed enrichment or qualification logic | No added credit or action cost — the steps inside it charge as usual |
| Run Claygent | Runs a Claygent — an agent with a prompt, a model, and its own tools | Work that needs reasoning or judgment | 1 action + credit cost of AI run |
| Update audience members | Writes results back to a contact or account in Audiences | Persisting what the run produced | Free |
| Conditional | Branches the graph on rules, code, or an AI judgment | Sending a record down one of several paths | Free for Rules and Code; For AI, same as Run Claygent |
| Run code | Runs Python for transforms, scoring, and routing logic | Deterministic work between agent and action steps | Free |

### `Run enrichment`

Runs a single Clay action: find an email, enrich a company or a person, read or write a CRM record, post to Slack. This step has Clay's full action library behind it, and you can choose which connected account runs the action. Its output is wrapped one level deeper than you'd expect — see **Connecting nodes** below.

### `Run Claygent`

Points the step at an existing Claygent rather than configuring one inline. Pick the agent, then pick a `Version` — `Current` to follow the agent as it changes, or a pinned `v#` to hold this workflow steady while the agent evolves.

The `Prompt` and `Model` show read-only here; `Builder` opens the Claygent builder if you need to change them. If the agent has moved on since you wired the step, Clay surfaces `Not using current Claygent version` with a one-click update.

The agent's tools are set in the builder, not on the node:

-   `Web search` gives it the internet.
-   `Find contacts and jobs` lets it look up people and open roles at a company.
-   `Access all business context` hands it your ICP and company details.
-   You can also connect your own MCP servers.

Use this step for the parts of a play that need judgment rather than a fixed lookup: scoring a lead, classifying a company, reading a site and returning a structured verdict. Because the agent chooses which tools to call and in what order, the same input can produce slightly different output run to run.

### `Conditional`

Branches the graph. Each branch gets its own outgoing connection point, and you pick how the decision is made from three tabs:

-   `Rules` — a filter builder over field values, evaluated top to bottom with the first match winning. Free. Use it for clear-cut routing, like a personal email address against a work one. `End run when no rule matches` decides what happens to a record that satisfies none of them.
-   `Code` — a Python expression, for logic the filter builder can't express, like a combined recency-and-status gate. Free.
-   `AI` — a prompt plus named routes, for a call that needs reasoning, like whether an account is a strategic fit. Costs about one action.

Reach for the cheapest mode that expresses the decision. When a rule checks a field that may be missing, a positive content check like _email contains @_ holds up better than a not-empty check, which can pass on an absent value. Switching modes clears the step's existing connections, so Clay warns you first.

### `Run code`

Runs a Python `handler(context)` function for deterministic work:

-   Reshaping data and computing a score.
-   Building a prompt string, or filling a fallback so a downstream prompt variable is never empty.
-   Unpacking a Claygent's structured output into typed fields.
-   Formatting a message.
-   Iterating over data inside one record.
-   Joining and matching records you loaded in earlier steps — the closest thing to a table formula.

`Run code` is free to run, with a one-second ceiling on each step. It's included on every paid plan; the free plan is the exception, where rules-based conditionals are available but `Run code` and the `Code` and `AI` conditional modes are not.

### `Run function`

Calls a Clay function — a reusable block of logic shared across tables and workflows. The function has to exist before you can add it, and it charges the actions inside it. Use it to keep standard enrichment or qualification logic in one place rather than rebuilding it in each workflow. See [Functions](https://university.clay.com/docs/functions) and [Managed functions](https://university.clay.com/docs/managed-functions).

### `Update audience members`

Writes what the run produced back to the contact or account in Audiences. Results land on the record rather than in the run, so anything you write back is immediately filterable in every other segment. Writing back is free.

### Where the deterministic and agentic parts sit

The graph itself is deterministic: the edges are fixed and every run follows the same connections. The judgment happens inside `Run Claygent` steps and `AI` conditionals. That split is the main design lever you have. Keep a step in `Run enrichment`, `Run code`, or a `Rules` conditional when you want it predictable and repeatable, and move it into a Claygent when you want it to adapt.

A common division of labor is to let a Claygent derive the judgment — scoring weights, say — from a sample, then have a `Run code` step apply it across the full set, so you get reasoning where it helps and repeatable math at scale.

## Connecting nodes

Two separate things move data through a workflow, and mixing them up is the most common reason a step comes back empty.

**Edges draw the flow.** One node's output can feed several downstream nodes, so you can branch three or more ways from a single step, and split paths can converge back onto a shared one. The trigger connects to exactly one node, so your first branch happens at the step after it.

**References say where a value is read from.** You don't add an edge to pull a value from a node several steps back — you reference that node and field by name. The source only has to sit upstream on the path that leads to this step. If it sits on a different branch, its output won't exist when this step runs, and Clay flags it as not upstream.

**Filling a Claygent's prompt.** A prompt contains `{{placeholders}}`, and each one is filled one of two ways.

-   **Letting the Claygent fill it** — the step immediately before writes the value in as it hands off. Good for free-form text, but the value is model-decided, so it can vary, and it only reaches back one step.
-   **Pinning it** — the placeholder points at an exact node and field, so the value is copied verbatim and can come from anywhere upstream.

Pin numbers, IDs, booleans, and anything else that has to be exact: if a scoring step five nodes back produced `score = 87`, pinning `{{score}}` to that node's `$.score` is what guarantees this step sees 87.

**Mapping a tool step's parameters.** `Run enrichment` and `Run function` steps have no prompt, so instead of placeholders you map each of the action's parameters. Each one is either a static value you type — object type = "Contact" — or a reference to an upstream field, like email = the trigger's `Email`.

**Reference syntax.** A reference is a path into the source step's output:

-   `$.field` for a top-level field, `$.nested.field` for a nested one, and `$.records[0].Id` to index into an array.
-   Grouped action parameters use a pipe: `fields|domain`.
-   Tool step outputs are wrapped. A field the action returned as `name` is read as `$.toolResult.result.name`, not `$.name`.

That last one is worth committing to memory — a missing `toolResult.result` prefix is the single most common wiring mistake, and it fails quietly by handing the next step an empty value rather than raising an error. There's no autocomplete for upstream fields yet, so the reliable way to get a path right is to run the workflow once and read the actual output structure on the step you're referencing.

## Testing and observability

You can see exactly how a workflow reached any result — visually trace the path an individual account or contact took, see which conditions applied at each branch, and read an agent's reasoning where the call wasn't deterministic. That's what turns an unexpected result into something you can reverse-engineer and fix rather than guess at.

The workflow editor has two views, `Graph` and `Runs`.

**Testing as you build.** Hover any node and click its run button to try that one step on its own, either against a recent run's data or with values you type in — `Recent` and `Enter manually`. The panel shows a credit estimate for the selection before you commit.

This runs the step you started from rather than continuing through the rest of the graph, so use it to prove out a single step's config, and a `Run manually` trigger to prove out a whole path. Runs started this way carry a `Partial` badge in the list so they're easy to tell apart.

**Data observability.** Every run is recorded, and the record is fixed once written: it keeps the version it ran against, each step's inputs and outputs, timings, and any error. `Recent runs` on the canvas is the quick view — hovering a run previews its path on the graph, and clicking pins its trace so you can step through it. `View all runs` opens the full history, where `Standard` lists runs chronologically and `Table` lays them out as a grid so you can compare outputs across many at once.

Narrow the list by time (`All`, `1d`, `1w`, `1m`), or by `Status`, `Versions`, and `Triggers`. A run reads as `Pending`, `Running`, `Waiting`, `Paused`, `Done`, or `Failed`.

Open one to see its `Inputs` and `Outputs`, its step-by-step trace with per-step duration and credit usage, and the routing decision behind an `AI` conditional. From the list you can re-run a run with the same inputs, or pause and resume one that's still going. A new run can take around 30 seconds to appear, so give it a moment before assuming a trigger didn't fire.

**Reading how a decision was made.** Opening a run lights up the path it actually took on the graph, so you can see which branch each record went down and which steps never fired.

Each conditional shows its own evidence: `Matched rule` for a `Rules` branch, `Script output` for `Code`, and `Reasoning` for `AI`, where the model writes out why it routed the record the way it did. A `Run Claygent` step surfaces its reasoning the same way, alongside a summary of the tools it called.

That's what you work backwards from when a record ends up somewhere you didn't expect — the decision itself, not just its outcome.

### Read the runs dashboard

## Version history and publishing

Clay autosaves the whole graph — nodes, edges, prompts, code, and tools — as you work. Autosaved versions are locked once saved, and each run is pinned to the version it started on, so editing a workflow never changes a run already in flight.

What reaches your live triggers is a version you publish.

1.  Build and test freely. While a published workflow has unpublished changes, the badge next to the version selector reads `Edit` rather than `Live`, and a trigger you haven't published sits in `Draft` and won't fire.
2.  When it's ready, click `Publish`. On `Ready to go live?`, name the version in `Version name` — Clay suggests the next number, like `V4` — and confirm with `Publish`. This sets every trigger on the workflow live at that version. If `Publish` is unavailable, the workflow has no trigger yet.
3.  For a workflow on a segment, check `Run on all members now` to also run it across the segment's current members. Clay shows how many records that covers and a credit estimate for the backfill before you confirm.

The `Versions` dropdown in the topbar lists published versions by name or number alongside when each went live. For the full picture, open workflow settings and click `History` to see `Workflow history`, which shows published versions with their autosaves underneath.

From any version there you can:

-   `Restore this version` to roll back.
-   `Create new workflow` to spin it off rather than replace what you have.
-   `Copy version ID`.

Restoring rewrites your working copy, so it moves the workflow back into `Edit` until you publish again. Pausing and resuming a single trigger stays available independently, and a later publish resumes it.

## Credits and performance

Workflows bills on the same two meters as the rest of Clay. If a node consumes an action or credits, those will be billed per record per node. There's no difference in cost to run the same work through a workflow or a table.

Workflows is available on Enterprise, Growth, and Launch plans indefinitely, and on legacy Starter, Explorer, and Pro plans through the end of 2026. Free and trial plans include it as well, with some limitations.

Most cost sits in the enrichment and Claygent steps, and a few habits keep it in proportion:

-   Do transforms, routing, and formatting in `Run code` rather than asking a model to do them.
-   Reuse a value you already fetched upstream instead of calling the same enrichment twice.
-   Map an action's parameters yourself so the step doesn't need a model call to fill them in.
-   Match the model to the task, and save the most capable ones for real reasoning.
-   Prune as you go. Graphs collect steps over time, and unreachable ones still add clutter and cost.

**Speed.** Most runs finish in seconds to a couple of minutes, and because runs go in parallel, throughput comes from concurrency rather than from any single run being fast. Within one run, branching independent lookups from the start instead of chaining them shortens data-heavy runs noticeably. A single heavy Claygent — a research-and-compile step, say — can take several minutes and use tens of data credits on its own; that's a step doing more work, not a problem.

**Scale.** Workflows is built for scale. Unlimited records and unlimited steps.

In practice that means you point a workflow at an entire audience rather than a slice of it. Where a table caps the rows you can work with and the columns you can add, a workflow caps neither, so a long play keeps its whole sequence in one graph instead of being split across several tables.

A single step also isn't the place to load a very large result set — each node handles up to 5MB of data per record, so a warehouse query returning a hundred thousand rows into one node will hit that ceiling. Land the data in [Audiences](https://university.clay.com/docs/audiences) and read it off the record instead — that's the pattern to reach for, since the result stays reusable in every other segment and workflow rather than trapped in one run. If you do need it inside the step, page through with limit and offset.

A segment that changes rapidly is the one case worth planning around: a bulk import that touches thousands of records fires thousands of runs at once, which spends credits quickly and can hit a provider's rate limits. For a high-volume segment, `Segment on a schedule` gives you the same coverage at a pace you control.

Have questions about Workflows? See [Workflows FAQs](https://university.clay.com/docs/workflow-faqs).
