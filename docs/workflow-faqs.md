---
title: Workflow FAQs
description: Answers to common questions about Workflows access, scale, list handling, branching, cost estimation, and how Workflows relates to Audiences and tables.
last_synced: 2026-08-11T15:45:07.872Z
---

# Workflow FAQs

Answers to common questions about access, scale, list handling, and how Workflows sits alongside Audiences and tables.

Workflows is Clay's orchestration layer — a graph of connected steps that a trigger starts and that runs once per record. This page covers the questions that come up most often once you start building, and the workarounds for the things Workflows doesn't do yet.

## FAQs

### Who can create and edit a workflow?

Anyone with member access can create workflows, edit them, and run them. Deleting a workflow is reserved for workspace admins. View-only roles can open a workflow and read its runs but not change it. If you see `You do not have the proper access for workflows in this workspace`, your role is what's in the way.

`Integrations` in workflow settings is visible to everyone, but changing what a workflow exposes there takes permission to manage workspace access.

Access to Workflows itself is separate from your role: it's switched on workspace by workspace during open beta. If `Workflows` isn't in your left sidebar under `Orchestration` at all, it isn't enabled for your workspace yet — signing in to the Clay CLI turns it on, and your Growth Strategist can confirm where things stand.

Once it's on, Workflows is available on every plan, including free and trial plans, and on legacy plans through the end of 2026. Individual pieces still vary: the free plan includes rules-based conditionals but not `Run code` or the `Code` and `AI` conditional modes, and some triggers need a paid plan.

### When should I use a workflow instead of a table or Bulk Enrich?

Reach for a workflow when something needs to run on its own — on a trigger or a schedule — and when different records should take different paths depending on what you learn about them. Routing, branching, and event-driven plays on individual records are what it's built for.

Tables are still the better fit when you want cell-by-cell visibility on a working set you're exploring or prototyping, or when you need a data source that isn't in Workflows yet. [Bulk enrichment](https://university.clay.com/docs/bulk-enrichment) is the better fit for running the same set of enrichments across a large existing record set and keeping it current over time. The durable split: [Audiences](https://university.clay.com/docs/audiences) is where your data lives, and Workflows is how you act on it.

### How do Workflows and Audiences work together?

Audiences holds the records and the segments; Workflows acts on them. The usual shape is a loop — a record enters a segment, that starts a run, the run does its work, and `Update audience members` writes the result back to the profile.

That write-back is what makes the loop useful. Results land on the record rather than in the run, so a field a workflow produced is immediately available as a filter in every other segment, including segments that trigger other workflows. Keeping Audiences as the source of truth is also what lets separate runs coordinate at all.

### What happens when a run fails?

The run stops at the step that failed and keeps everything it produced up to that point, so you can open it and read that step's input, its error, and any partial output. Failed runs generally cost little or nothing, since you're only charged for the lookups and AI that actually ran before the failure.

A few errors have recognizable causes. A tool-not-found error usually means the integration isn't configured for your workspace. An invalid-input error usually means a reference is pointing at a field that doesn't exist in the upstream output. A rate-limit error means a provider throttled you rather than anything being wrong with the graph. Fix the cause, publish, and re-run — a run carries the version it started on, so your fix applies to the next run rather than retroactively to the one that failed.

### Can one workflow call another?

Not from inside the graph — a workflow is started by its trigger rather than called by another workflow. Functions are the reuse mechanism: build the logic once as a function, then drop `Run function` into as many workflows as need it, and each one stays in sync with the single definition. The framing that tends to click is that functions are ingredients and workflows are recipes; you can put an ingredient into any number of recipes, just not a whole recipe into another recipe.

There is one indirect route worth knowing about. Someone who can manage workspace access can expose a workflow as a routine under `Integrations` in workflow settings, including to `Claygent` — and a `Run Claygent` step can then reach it as a tool. It's a longer way around than a function, and the calling step is agentic rather than deterministic, so treat a function as the default and this as the exception.

### Can a step run once for each item in a list?

Yes, through `Run Claygent`. Give the agent the list and the function you want applied to each item, and it calls the function per item, one after another — that's how one-to-many work inside a single run gets done today. Because the agent decides the order and pacing, treat it as less predictable than a deterministic step, and keep the list modest.

`Run code` is the steadier option when the work is pure logic, since it can iterate freely over data within a record. The one thing it can't do is call an enrichment repeatedly — a code step can call an enrichment once, not loop one over a set. For per-item enrichment across a long list, running that enrichment as a bulk enrichment on a segment tends to be more reliable, and the workflow can then read the results off each record.

### Can a workflow loop back on itself?

No — the graph runs one way, so there's no cycle or counting loop between steps. Iteration happens inside a step instead, either in `Run code` within a single record or in `Run Claygent` over a list.

If what you want is for something to happen repeatedly over time rather than within one run, that's a trigger question rather than a graph question: `Segment on a schedule` or `On a schedule` gives you a fresh run on each pass, which is usually what people are reaching for.

### Can a step query several objects at once, or join across sources?

A step reads from one source at a time, so joins happen a step later rather than inside the query. Load each source in its own step, then use `Run code` to match and merge them in memory. That's also where many-to-many mapping belongs — scoring a set of accounts and assigning each one to a rep is a single code step once both sets are loaded.

### Can two runs share data?

Each run is fully independent, which is exactly what lets a batch process thousands of records at once without them queueing behind each other. The trade-off is that a run can't read another run's output.

When two runs genuinely need to see the same state, keep that state in Audiences: have the first run write it with `Update audience members`, and have the second read it off the record. Audiences is the shared memory between runs.

### Can I run just part of a workflow?

You can run a single step on its own from its run button on the canvas, against a recent run's data or values you type in. That's the fast way to prove out one step's configuration without paying for the steps around it.

What you can't do yet is start at a step and let the run continue through everything downstream of it — a step you run this way executes on its own and stops. So for checking a whole path, a `Run manually` trigger with one record or a handful is still the move. Running against a slice of a segment isn't available either; point a manual trigger at a few records instead.

One thing worth knowing before you publish: a manual run and a triggered run can resolve input mappings differently, so a mapping that renders correctly on a manual run is worth confirming on a real trigger.

### How much will a run cost before I run it?

Estimates show up in three places: each step's configuration panel as you set it up, the panel when you run a single step, and next to `Run on all members now` when you publish a workflow onto a segment. Between them you can size most things before committing.

What there isn't yet is a whole-graph estimate or a per-run cost breakdown after the fact beyond the per-step credit usage on the trace. For anything large, run a small test batch first, read the actual credit usage on those runs, and scale up from there rather than relying on the estimate alone.

### Is every enrichment, source, and signal available in Workflows?

The action library is at parity, so anything you can run as an enrichment in a table you can run in a `Run enrichment` step. Table data sources and signals are still being brought across, so a few aren't in Workflows yet, and which actions you see depends on your plan exactly as it does in a table.

When you need one that isn't, build that part where it does exist and meet the workflow at the record: run the source or signal against your data so the results land in Audiences, then trigger the workflow off a segment that filters on them. The workflow reads the record, so it doesn't matter which surface filled the field.

### Are waterfalls available in Workflows?

Not as a step type — a `Run enrichment` step runs one action, so a waterfall's provider fallback isn't something you draw on the canvas. Where you need one, put it inside a function and call that function with `Run function`: the function runs the waterfall, and the workflow branches on whatever it returns. That keeps the fallback logic in one governed place and available to your tables at the same time. See [Managed functions](https://university.clay.com/docs/managed-functions).
