---
title: Topic intent
description: How to find net-new companies and people based on topic research activity, or monitor existing lists for intent signals using Bombora, Delivr, and Intentsify.
last_synced: 2026-08-20T01:55:39.279Z
---

# Topic intent

Find and monitor the companies and people researching the topics you care about.

Topic intent shows you which companies and people are consuming content about topics you choose — a competitor, a product category, an industry theme — before they ever fill out a form. You can start from topics to build a net-new list, or point topic intent at accounts you already track and get an event each time their interest changes.

**Note:** Topic intent is in open beta.

**Cost:** Topic intent bills in credits, the same way other actions and signals in Clay do. "Sourcing net-new records charges **per result returned** (and if a result matches multiple topics, you're charged for each matched topic)."

**Note:** Monitoring bills for every selected topic on every record checked, whether or not a provider returns intent for that topic. Starting with a focused topic list and a smaller view keeps spend predictable while you calibrate, and Clay shows the estimated cost of a run before you turn the signal on.

**There are two ways to use topic intent:**

-   **Find net-new records** — start from topics alone and get back companies or people you don't have yet, as new rows in a table.
-   **Monitor a list you already have** — start from an audience, a table, or a CSV you've imported, and get an event each time one of those companies or people shows intent on your topics, or moves to a different intent level.

The two work well together: source a list of accounts that are in market now, then monitor that list so you hear about them again when their interest shifts.

## Choosing providers

Three providers supply the intent data, and they resolve activity differently:

-   **Bombora** — companies only. Scores an account against its own historical baseline, which suits account prioritization and territory planning.
-   **Delivr** — companies and people. Resolves open-web activity to named individuals, so it's the one to reach for when you want the specific people researching a topic rather than just the account.
-   **Intentsify** — companies and people. Aggregates and validates signals from several sources before scoring them.

You can select more than one, and it's worth doing when coverage matters: each provider has its own publisher relationships, so a second or third widens the slice of the web you can see intent across. Each provider you add is billed separately, and Bombora is priced as a premium provider, so it costs more per check than Delivr or Intentsify. Starting with one and adding others once you've seen the fill rate keeps the cost in check.

## Finding new records with topic intent

This route runs in a workbook, so Audiences isn't involved.

1.  In a workbook, open the `Create` panel.
2.  Under the source options, select `Find with topic intent`.
3.  Choose whether you're finding companies or people.
4.  Add the topics you want to match on. Providers are chosen in the same place, under `Data providers`.
5.  If you're connecting your own provider account, add it under `Account credentials`.
6.  In each provider's configuration section, set the options that apply to that provider alone:
    -   `Minimum topics matched` — require a record to show intent on more than one of your topics.
    -   `Company limit` or `People limit` — cap how many records that provider returns.
7.  Optionally set `Timeframe` to change how much intent history is included. It applies to Bombora and Intentsify; Delivr always uses a fixed lookback.
8.  Optionally set `Intent score tiers` to limit results to the intent levels you want.

## Setting up a topic intent signal

**If the records you want to watch already live in Audiences:**

Add topic intent from that audience's signals panel — the `Topic intent configuration` section there holds the same provider, topic, and tier settings as the steps below.

**To monitor a table instead:**

1.  Go to `Signals`, then choose `Topic intent` from the quick links.
2.  Under `What to monitor`, choose `Monitor companies` or `Monitor people`.
3.  On `Select a source`, choose the table and view holding the records to monitor.
    -   Company monitoring reads a domain column, and person monitoring reads a professional profile URL column.
    -   The view needs to hold fewer than 250,000 records.
4.  On `Configure topic intent signal`, add your topics, then set `Intent tiers`. Providers are selected in the same place, under `Data providers` — a provider left with no topics isn't checked and isn't charged.
5.  On `Choose run frequency`, choose how often Clay rechecks the list. Weekly is both the default and the shortest interval available.
6.  On `Configure optional enrichments`, add any enrichments you want on the results table.

### Choosing topics

Describe what your buyers research in plain language, and Clay maps that to each provider's own topic catalog — so you don't configure providers one by one.

1.  Click `Add topic or category`.
2.  Search for a topic, or create a category and describe it, as in `Describe the topics your audience researches, e.g. payroll compliance tools`.
3.  Use `Generate more topics` to expand a category into more provider topics.
4.  Open `Provider topics` to see exactly which topics each provider was mapped to.

Topic limits are per provider: 50 topics each for Bombora and Intentsify, and 25 for Delivr. Narrow topics tend to beat broad ones — a broad category will match far more accounts, but many of them won't be in market for what you actually sell.

### Setting intent tiers

Intent comes back as one of three tiers — `Low`, `Medium`, and `High` — reflecting how much relevant content a record has consumed and what kind. The tier setting applies across every provider you've selected. A signal includes all three tiers by default, and the source step starts at `Medium and high`.

`Medium` reflects an account's baseline level of intent. `High` means the account is showing in‑market signals beyond its baseline — and it's the tier most teams act on.

Delivr returns medium and high intent only, so adding `Low` widens results from the other providers rather than from Delivr.

## Reading topic intent results

Results are grouped by provider under `Provider scores`. Each provider's block holds:

-   `Intent tier`: That provider's overall tier for the record.
-   `Raw score`: The provider's own numeric score behind the tier.
-   `Topic count`: How many of your topics the provider returned intent for.
-   `Topics`: One entry per matched topic, each with its `Topic name`, its own score, and — for companies — the number of people at the company showing intent for that topic.

A signal adds one event per topic as it surfaces, so a company that starts researching three of your topics produces three events. Each event records which provider surfaced it, along with that provider's own data date.

### How tiers map to scores

`Raw score` runs on a 0–100 scale, and these are the bands behind the tier labels:

| Tier | Raw score | What it means |
| --- | --- | --- |
| High | 60 and above | In market — worth acting on now. |
| Medium | 40–59 | Baseline interest — somewhat in market. |
| Low | Below 40 | Less activity than normal for that record. |

Inside the high band, 60–74 is the actionable lower half and 75 and above is as in-market as a record gets. A higher score means a more intense signal, not a higher chance of a deal. Intent is best read as a prioritization cue you combine with fit — an account can surge on a topic because of an internal project or a competitor's research.

## Using topic intent as an enrichment

Topic intent also runs as an enrichment on a table you already have, which is the route to take when you want to check whether a specific set of companies is in market right now. Each provider has its own topic intent enrichment: all three cover companies, and Delivr and Intentsify also cover people.

Enrichment is priced the way monitoring is rather than the way sourcing is — per record checked, plus one action per row. Running the same enrichment by hand week after week costs more than having a signal do it on a schedule, so move to a signal once you know your topics are right.

## FAQs

### How do the providers track intent?

Providers run large networks of B2B publishers and content sites. They tag pages and classify them into big topic taxonomies using natural-language analysis. What they measure is _content consumption_ — what people actually read.

Intent is recorded when activity on a topic rises meaningfully above a company's usual baseline. At the account level, activity is resolved to a company (e.g., IP-to-company matching and device graphs) and then aggregated. At the person level, providers use identity resolution to tie reading to a professional profile — coverage varies by provider.

### How is topic intent different from web intent?

Web intent identifies visitors to your own website. Topic intent covers research happening off your site, across provider and publisher networks, so it surfaces accounts that haven't found you yet. Plenty of teams run both and score them together.

### How is topic intent priced?

Topic intent bills in credits, on the same action-based model as the rest of Clay — what a run costs depends on how many topics you select and how many records get checked. Sourced records that come back without intent data are refunded, so you only pay where a provider found something. It's available on any paid plan, and during a trial.

### Why can't I check a list more often than weekly?

The providers refresh their intent data on a weekly cadence, so checking more often would re-read data that hasn't changed while still charging for the check.

Daily intent is also harder to read, since a spike only means something against a record's own recent baseline and a day or two of activity rarely establishes one. A week is long enough to give you a comprehensive picture while still being fresh, and it keeps spend predictable.

### Can I change providers on a signal after I create it?

Provider selection locks once the signal exists. Topics and intent tiers stay editable, so if you want to monitor a different set of providers, create a new signal.

### Which regions does topic intent cover?

You can find intent across the globe, and coverage is strongest in North America today. The providers' networks index mostly .com domains, so companies whose main web presence sits on a country-specific domain come back less often.

### Can I bring my own contract with one of the providers?

Bombora and Intentsify run on the Clay credits you already have, with provider access included — there's nothing to connect. Delivr works a little differently: if you hold your own Delivr contract, you can connect that account under `Account credentials` and run on it.
