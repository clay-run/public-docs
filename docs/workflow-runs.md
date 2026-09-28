---
title: Managing workflow runs
description: Monitor, filter, and bulk re-run workflow runs from the Clay runs dashboard. Resume runs from where they failed, from a specific node, or from the original trigger.
last_synced: 2026-09-28T00:00:00.000Z
---

# Managing workflow runs

Monitor, filter, and bulk re-run workflow runs from the Clay runs dashboard.

## Runs dashboard

The runs dashboard shows every execution of your workflow — its status, when it ran, and what it processed. From the dashboard you can inspect individual runs, filter by status or date, and kick off bulk re-runs across many runs at once.

## Bulk re-run

Bulk re-run lets you re-run many workflow runs at once, straight from the runs dashboard. Filter or select the runs you care about, choose how to restart them, and kick them all off in a single action. Available on all workspaces.

### Selecting runs

From the runs dashboard, select the runs you want to re-run in one of two ways:

- **Select specific runs** — check individual run rows from the dashboard list.
- **Filter, then select all** — apply a filter (by status, date range, or search query) and select all matching runs at once.

### Restart modes

When you start a bulk re-run, choose one of three modes:

- **From where they failed** — Each run restarts at its failed step. Steps that already succeeded are not re-run, so no credits are spent redoing work that completed correctly.
- **From a specific node** — All selected runs restart from a step you choose. The run continues from that node and executes all downstream steps.
- **From the top** — Each run is recreated fresh from its original trigger. Runs that were started manually or via API (rather than by a trigger node) are skipped in this mode, because there is no trigger to replay.

### Preview before you commit

Before submitting a bulk re-run, Clay shows you a preview with two pieces of information:

- **Number of runs that will be created** — the count of distinct records the re-run will process after deduplication (see below). This is the number shown in the preview, not the number of runs you selected.
- **Estimated credit cost** — an upper-bound approximation of the data and action credits the re-run will consume. The estimate prices each step in the workflow against its executable set (the restart point and all downstream steps), without replaying individual run conditions or skipped branches — so actual charges may be lower.

Review the preview and confirm before Clay creates any runs or charges any credits.

### Deduplication

Runs are deduped by record before the re-run starts. If the same person or company appears in multiple selected runs, Clay creates only one new run for that record — you won't spend credits running the same subject twice when selecting a large batch.

The preview's run count already reflects the deduped total, so the number of new runs created will always be equal to or less than the number of runs you selected.
