---
title: Enrichment in Workflows
description: Guided workflow for enriching an Audiences segment with third-party data, with pre-configured trigger and write-back steps, test panel, and scheduling options.
last_synced: 2026-09-08T15:41:56.218Z
---

# Enrichment in Workflows

Enrich an Audiences segment through a guided workflow that opens with its trigger and write-back step already configured.

Enrichment in Workflows is the guided way to add third-party data to a segment in Audiences. Because the trigger and the write-back are already in place when you start from a segment, the first thing you do is pick an enrichment — and you can test it on real records before it touches the whole segment.

**Note:** This experience is in beta, and it needs both Audiences and Workflows enabled in your workspace. If you open a segment's `Enrichments` panel and don't see `Create enrichment workflow` under the `+` button, it isn't switched on for your workspace yet.

## Before you start

The guide builds the enrichment from data you already have in Audiences, so the segment needs to exist first.

1.  **Connect your sources in Audiences.** Whatever the enrichment should read from — your CRM, your warehouse, a CSV — see [Audiences](https://university.clay.com/docs/audiences) to get set up.
2.  **Build the segment you want to enrich.** Keep the first one small, so you can read every result while you're still tuning the setup.
3.  **Spot-check the fields the enrichment needs.** The guide maps enrichment inputs from segment fields, so a record with a blank company domain or email has nothing to map from.

## Building the enrichment

The guide runs in four steps — `Source`, `Enrich segment`, `Map fields`, and `Review & run`.

1.  Open the segment you want to enrich and go to its `Enrichments` panel. Click `+`, then choose `Create enrichment workflow`.
2.  On `Source`, confirm the segment you started from. Add more segments here if the same enrichment should cover several.
3.  On `Enrich segment`, pick what to run. Alongside the enrichment catalog you can add a Claygent, a function, or a utility step — `Run code` and `Delay` are always offered, and `Conditional` appears wherever the graph can take one.
    -   Clay fills in most of the input mapping for you from the segment's fields. It's worth checking before you run, especially on enrichments that take more than one input.
    -   Placement and wiring are handled for you. You pick the spot — the `Enrich segment` placeholder at the end of the flow, or an insertion point before, after, or in parallel with a step that's already there — and Clay inserts the step and reconnects whatever sat on either side of it.
    -   The canvas position of each step follows the shape of the flow, so there are no connections to draw and nothing to drag into place. That's specific to the guide; the manual builder gives you the freeform canvas back.
4.  On `Map fields`, point each `Workflow output` at the `Segment field` it should land in. Suggested pairings arrive already filled in, and `Add field` creates a new segment field when nothing existing fits.

Moving on from `Map fields` adds the `Upsert segment record` step that writes the data back.

### Testing as you build

`Test data` gives you one row per record and one column per step, so every intermediate output is visible rather than just the field that lands in the segment. It's the fastest way to see what an enrichment actually returned for a particular person or company.

-   `Add data` pulls records in from the segment. Include a few thin ones on purpose — the records missing a domain or a title — since those are where mappings tend to break.
-   To iterate on one step, change its settings and run just that node, on a single record if you like. Nothing upstream has to run again.
-   The run log for a row shows why a step returned nothing.

### Switching to the manual builder

The guide covers the common shape: read a segment, enrich it, write the results back. For anything more involved, the utility steps are where the orchestration lives, and you can add them at any point in the guide rather than switching editors.

If you'd rather build the rest by hand, `Guide actions` → `Switch to manual builder` hands the workflow over to the standard editor. Your steps stay exactly as they are, but the guide doesn't come back for that workflow, so finish the field mapping before you switch. `Close guide` only hides the panel, and you can reopen it.

## Reviewing and running

`Review & run` summarizes what you built, and it's where the workflow goes live. `Status` fills in `Completed rows`, `Errored rows`, and `Credit cost` once there are runs to count, and `Manage runs` opens the full run history.

The `Run` button gives you three ways to finish, and the one you pick decides whether you spend credits now.

-   `Publish` saves the workflow and its triggers without running anything, which is what you want when the setup should be in place but you're not ready to spend credits.
-   `Publish and run on …` publishes and then runs across the whole segment. A credit estimate sits on the option, and Clay asks you to confirm before it starts.
-   `Test on …` runs against the rows in the test panel instead of going wide, so you can keep iterating.

### Keeping the segment enriched over time

Two settings on `Review & run` decide whether the enrichment keeps working after that first run:

-   `Auto-enrich new records` enriches records in the background as they join the segment.
-   `Recurring enrichments` re-enriches everything in the segment on a schedule. This is the setting that keeps the data fresh: without it, an enriched field holds whatever was true on the day it ran, while titles, headcount, and funding keep moving.

Either one can be paused and picked back up later. A paused workflow shows `Resume` on `Review & run`, or `Resume all` when more than one of its triggers is paused.

## Where the enrichment lives afterward

What you built is a workflow, so it's reachable from Audiences and from Workflows both — the same enrichment, three ways in.

| Where to find it | What you can do there |
| --- | --- |
| The segment's Enrichments panel | Read its status at a glance, open View runs or View workflow, rename it, or delete it. Each card also shows which segments it's Operating on. |
| Data hub → Enrichments | Compare every enrichment across Audiences in one table, with Status, Audiences, Fields, Credit spend (30d), and Run cadence. |
| Workflows | Everything the standard editor gives you: the Graph, and Runs for tracing a single record across every step. |

See [Workflows](https://university.clay.com/docs/workflows) for how runs, versions, and publishing work more generally.

## FAQs

### Why doesn't the guide appear on a workflow I already have?

The guided stepper is attached to a workflow when it's created from a segment's `Enrichments` panel — it isn't a mode you can switch on afterward. A workflow built in the standard editor opens in the standard editor, and so does one where someone has chosen `Switch to manual builder`, since that choice is permanent for that workflow. To get the guide back, create a new enrichment workflow from the segment.

### Can I change the field mappings after the enrichment has run?

Yes, and nothing has to be rebuilt. Reopen the workflow from the segment, go back to `Map fields`, and repoint an output or add a new segment field. Adding a whole enrichment step works the same way — the `Upsert segment record` step picks up the new output as soon as you map it.

### How do run conditions and formulas from tables translate here?

They become steps rather than column settings, but you don't have to build them on the canvas. For a run condition, open the enrichment's setup panel and use `Run if` — Clay adds a `Conditional` in front of that step and connects it, and records that don't meet the condition stop there rather than running the enrichment. Come back to the same section later and it offers `Edit run condition` instead.

A formula becomes a `Run code` step returning the value you want mapped. It's the same logic expressed a different way, so give yourself a bit more time on the first one than a table column would take.

### Is this the same as bulk enrichment?

They're separate things that both sit under `+` in the `Enrichments` panel. `Create enrichment workflow` builds what this doc describes, while `Create enrichment table` is labeled `Legacy bulk enrichment` in-product and gives you the older table-shaped setup. Some workspaces see only the workflow option.

There's also a separate `Bulk enrichment` product, created from `New` on the homepage. That one sends results straight out to a destination like Salesforce or Snowflake instead of writing back to Audiences, and it deletes enriched rows once the export succeeds — see [Bulk enrichment](https://university.clay.com/docs/bulk-enrichment) for that one.
