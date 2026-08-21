---
title: Topic Intent
description: Track which companies and contacts are actively researching topics relevant to your business, using data from Bombora, Delivr, and Intentsify.
last_synced: 2026-08-21T16:00:00.000Z
---

# Topic Intent

Track which companies and contacts are actively researching topics relevant to your business, using data from Bombora, Delivr, and Intentsify.

> **Currently in open beta.** Topic Intent must be enabled for your workspace. Contact your Clay account team or [Clay support](https://www.clay.com/university/guide/contacting-support) to get access.

Topic Intent surfaces companies and contacts that are actively consuming content on the topics you choose to monitor — such as a competitor name, a product category, or an industry theme. Each result identifies which entity (company or person) is researching the topic, which provider detected it, and how strong the intent signal is.

You can use Topic Intent in two ways:

-   **As a signal** — Monitor a known list of companies or contacts and receive a new event row whenever a new topic is detected or a tracked topic's score changes.
-   **As a source** — Discover net-new companies or people not already in your Clay tables who are currently researching your topics.

## How Topic Intent data is collected

Topic Intent draws from three third-party data providers that track B2B content consumption across their respective publisher networks:

| Provider | Company-level | Person-level |
| --- | --- | --- |
| Bombora | ✓ | — |
| Delivr | ✓ | ✓ |
| Intentsify | ✓ | ✓ |

Clay queries all selected providers in parallel and merges the results — so an account may appear in one, two, or all three providers' data. A match from **any** provider counts as a result.

**Topic Intent data does not include exact timestamps or content details.** The signal reflects aggregate research behavior over a time window — it tells you that a company or person was actively consuming content on a topic during that period, not the specific articles read or the precise moment it happened. This is inherent to how intent data providers collect and share signals.

## What each result shows

Results are organized by provider. For each matching provider, you receive:

-   **Intent tier** — A categorical label (`high`, `medium`, or `low`) indicating how strongly the entity is researching the topic relative to its baseline activity.
-   **Raw score** — A numeric score underlying the tier, useful for fine-grained prioritization.
-   **Topics** — The specific topics detected, including per-topic tier and score.
-   **Provider** — Which data source (Bombora, Delivr, or Intentsify) found the match, so you know exactly where the signal came from.

## Lookback window

The lookback window controls how far back Clay searches for intent activity. Available options:

| Timeframe | Description |
| --- | --- |
| Last 7 days | Freshest signal; smallest set of matches |
| **Last 14 days** (recommended default) | Balances recency and reach |
| Last 30 days | Expansive signal for a moderate set of matches |
| Last 60 days | Broadest reach with some older signal |

**Delivr always uses a fixed 14-day lookback** regardless of your selection. The timeframe setting applies to Bombora and Intentsify only.

## Setting up Topic Intent

### As a signal (monitor known accounts or contacts)

Use this to watch a list of companies or contacts you already track and get an event row whenever a new topic is detected.

1.  In your company or people table, click `Tools` → `Monitor for topic intent`.
2.  Select the source table and view you want to monitor.
3.  Map the identifier column: **company domain** for company-level monitoring, or **LinkedIn URL** for person-level monitoring.
4.  Select one or more data providers. Note that Bombora supports company-level intent only; Delivr and Intentsify support both company and person-level.
5.  Choose your topics using plain-language descriptions — Clay maps them to each selected provider's topic catalog.
6.  Set the intent tier filter (high, medium, low) to control which signals surface in your table.
7.  Set how often the signal should run.
8.  Click `Save and run`.

### As a source (find net-new companies or people)

Use this to discover companies or people not yet in your Clay tables who are currently researching your topics.

1.  From the workbook homepage or any table, add a new table and choose the Topic Intent source (Find companies with topic intent or Find people with topic intent).
2.  Select providers and configure your topics.
3.  Apply filters (industry, company size, location, intent tier).
4.  Run to pull results into your table.

## FAQs

### Why do nearly all of my accounts show topic intent signal?

High match rates are expected when your topics are broad or commonly researched. Because Clay checks all selected providers in parallel — and a match from **any** provider counts as a result — having multiple providers active significantly increases the likelihood that an account appears in at least one. To get higher-quality, more actionable signals:

-   Use more specific topics (for example, a particular competitor name rather than a broad category like "artificial intelligence").
-   Filter by intent tier — focus on `high` matches to prioritize the accounts most actively researching your topic.

### Why does my first signal run return so many new events?

The first run of a Topic Intent signal is called the **initial check**. Because Clay has no prior baseline for comparison, every account or contact that matches during the initial check is recorded as a `new_topic` event with `Is Initial Check: true`. This is expected behavior. On subsequent runs, only newly detected topics or changed scores generate new event rows.

### What does the intent tier mean?

Each result includes an intent tier — `high`, `medium`, or `low` — that reflects how strongly a company or contact is researching a topic compared to its typical baseline activity. `High` indicates substantially elevated research activity for that entity. A numeric raw score underlies each tier and is available in the result data for finer-grained ranking.

### Why doesn't the data include exact dates or content details?

Bombora, Delivr, and Intentsify surface patterns of research activity at the company or person level — not individual page views or article reads. The providers do not expose per-event dates or the specific content consumed; they share whether and how much a company or person has been researching a topic during the window. The signal is a directional indicator of active interest, not a precise activity log.

### What is the difference between Bombora, Delivr, and Intentsify?

All three providers track B2B content consumption, but they differ in scope and behavior:

-   **Bombora** — Company-level only. Does not surface individual contact-level intent.
-   **Delivr** — Supports both company and person-level intent. Lookback is fixed at 14 days.
-   **Intentsify** — Supports both company and person-level intent. Lookback is configurable (7, 14, 30, or 60 days).

Each provider maintains its own topic catalog. When you select a topic in Clay, Clay maps your plain-language description to the closest match in each selected provider's catalog.

### What plans include Topic Intent?

Topic Intent is currently in open beta and requires workspace enablement by the Clay team. It is not yet available on free plans. Contact your Clay account team or [Clay support](https://www.clay.com/university/guide/contacting-support) to enable it for your workspace.
