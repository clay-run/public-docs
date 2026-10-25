---
title: Reusing saved enrichment data
description: Learn how Clay saves enrichment data in Audiences and how to reuse saved values instead of paying for the same data again.
last_synced: 2026-10-20T15:07:08.152Z
---

# Reusing saved enrichment data

Keep the data your enrichments return so later runs can reuse it instead of paying for the same answer twice.

When an enrichment runs and a provider answers, Clay can keep that data point on the record in `Audiences`, the shared store of people and companies your workspace builds up as it works. A later enrichment that needs the same data point reuses the saved value instead of buying it again.

**Note:** Saved enrichment data is in beta and still rolling out, so the settings described here may not have reached your workspace yet.

## How saved data works

Saving and reuse are separate switches, which is what lets a workspace build up saved data before anything starts reading from it.

-   **Saving** records what a provider returned. It's on by default and costs nothing extra, because you have already paid for the answer. It applies workspace-wide, across both tables and Workflows, Clay's automation builder.
-   **Reuse** serves a saved value in place of a live call, and it's the half that saves credits. It's opt-in — nothing reaches for saved data until you turn it on for an enrichment or make it an action's default.
-   **Expiration** keeps reuse honest. Every saved value has a window, `30d` unless you change it, and past that the next run buys the data fresh and saves it again.

A reused value costs no data credits, nor does it draw on your allowance for Companies, People, Jobs, Clay's own data provider. It still uses one action, the same as any enrichment run, because Clay is still filling the cell for you. The [actions and data credits](https://university.clay.com/docs/actions-data-credits) doc covers how the two units differ.

Not every action can save data. An action qualifies only once Clay has reviewed it and confirmed it changes nothing outside Clay, which rules out anything that writes to another tool — a CRM update served from saved data would silently skip the update. Everything else is marked `Can't save data` in your enrichment settings.

## Turning on saving for your workspace

The workspace-level controls live on the `Enrichments` page in workspace settings, which is available to members who can manage workspace access.

1.  Open workspace settings, go to `Enrichments`, and stay on the `Enablement` tab.
2.  On the `Save enrichment data in Audiences` card at the top, click `Manage saved data`.
3.  Set `Save enrichment data in Audiences` to choose whether Clay records what providers return.
4.  Set `Reuse saved data by default` to choose what happens on an enrichment that hasn't made a choice of its own. Left off, each enrichment opts in for itself; turned on, every action starts from reuse.
5.  Click `Save changes`.

Turning saving off stops new values being recorded and stops anything being served, so every enrichment buys fresh data. It doesn't delete what you already have — stored values sit out their windows, so turning saving back on inside that window picks up where you left off.

The same card charts how many lookups were served from saved data over the last 12 weeks, with an estimate of the credits that saved. The figure is an estimate because credit rates vary by action; the [credit usage](https://university.clay.com/docs/credit-usage) dashboard is where you'll find actual spend broken down by table, integration, and time period.

## Setting policies per provider and action

Below the card, the `Enablement` tab lists every provider available to your workspace. Each card's footer counts its actions and how many of them can save data — `12 actions · 8 save data`, or `9 actions · can't save data` where none can. The toolbar filter narrows the list to `All providers`, `Can save data`, or `Can't save data`, which is the quickest way to see what your workspace can reuse from today.

Click `Manage provider` on a provider to open its settings. The top section sets the provider as a whole — `Save [provider name] data`, `Keep saved data for`, and `Reuse saved data by default` — and the `Actions` list beneath it sets each action individually.

Each action row carries four controls:

| Control | What it does |
| --- | --- |
| Enabled in workspace | Whether anyone in the workspace can add this action to an enrichment. This one isn't about saved data, and turning it off keeps whatever is already saved. |
| Save data | Whether Clay records what this action returns, so a later enrichment can reuse it instead of buying it again. |
| Keep for | How long a saved value stays on file before it expires. Actions start at 30d, and the choices are 7d, 30d, 60d, and 90d. |
| Reuse by default | Whether an enrichment reaches for this action's saved data without being asked. Off, each enrichment opts in for itself. |

An action that can't save data shows `Can't save data` in place of those controls. Where the actions under a provider disagree on a setting, the provider row above them reads `Mixed`.

One `Save changes` stores everything you touched, across the provider and its actions together.

**Note:** Some providers cap how long their data may be kept. On those actions the `Keep for` list offers only the windows that fit under the cap, plus the cap itself where it falls between two of them, and the cap holds even where a wider setting would otherwise allow longer.

### How the three levels combine

Saved-data policy can be set at the workspace, at a provider, or on a single action, and the levels resolve differently depending on the setting.

`Save data` off anywhere wins. Turn it off for the workspace and every provider and action beneath it stops saving, with their controls locked so you can see why. A provider works the same way over its own actions.

`Keep for` and `Reuse by default` follow the most specific setting instead. An action's own window overrides its provider's, which overrides the workspace's, so you can put a short window on one action without touching anything around it.

## Reusing saved data on an enrichment

Reuse is chosen wherever the enrichment is configured, so the same section turns up in three places: the sidebar of a single enrichment column, the sidebar of a waterfall that runs several providers in order, and the panel of an enrich node in Workflows.

Where the choice isn't offered — a workflow node running a Clay function rather than a single action, or a waterfall built inside a workflow — runs follow the default set in your enrichment settings.

1.  Open the enrichment and find the `Reuse saved data from Audiences` section. The switch starts from the action's default in settings, so it may already read `Enabled`.
2.  Turn the switch on to reuse saved data on this enrichment.
3.  Where the enrichment runs more than one provider, tick the checkbox beside each provider you want to reuse from.

Under each provider's name the section shows how much saved data you currently hold for it and how old the newest value is, so you can tell whether reuse will hit anything. A line at the bottom gives the window those values expire after, and `How saved data works` opens a short refresher.

A provider that can't be reused from says why in the same spot:

-   `Not available for this provider` — this action hasn't been cleared for saving.
-   `Saving is off for this workspace` or `Saving is off for this provider` — nothing has been recorded to reuse. Members who can manage workspace access get a `Turn it on in Settings` link here.
-   `Update this column to its latest version to reuse saved data` — the column is pinned to an older version of the action, and only the current version is cleared for saving.

## When to reuse saved data

Reuse pays off wherever you're likely to look up the same records again and a result from the last few weeks answers the question just as well as today's would.

Good fits:

-   Re-running a table you've already enriched.
-   Rebuilding or duplicating a workflow over the same records.
-   Testing and tweaking a table before a full run.
-   Teammates enriching overlapping companies or contacts in the same workspace.

Run fresh instead when:

-   You need the latest answer, such as recent job changes, new contact details, or timely signals.
-   You're validating or verifying data right before you reach out.

Because reuse is set per enrichment, you don't have to pick one way for everything — reuse on the columns that tolerate it, and leave the verification step at the end of your table buying fresh.

## FAQs

### Does turning reuse off on one enrichment stop Clay saving that data?

No. An enrichment set to buy fresh data every time still records what it gets, so everything else can reuse it. Saving stops only from workspace settings, and there you can stop it for the workspace, a provider, or a single action.

### What makes two runs count as the same lookup?

Reuse happens when the same action runs with the same inputs. Change an input and it's a new lookup that buys fresh data, so a column that normalizes its inputs — trimming whitespace, lowercasing a domain — will hit saved values more often than one that doesn't. A new major version of an action also starts fresh, since its saved values are kept separately from the previous version's.

### What happens when a run finds nothing, or fails?

A run that comes back empty is recorded wherever that run was charged for, so you don't pay twice to learn the same blank. Where Clay refunds a run that found nothing, there's nothing to save you, so nothing is recorded. A run that failed records nothing either way.

### What happens to values I've already saved when I change a window?

Shortening a window takes effect at the next lookup, and values already older than the new window stop being served right away. Lengthening one works the same way in reverse: values still in storage but older than the previous window become eligible again immediately, rather than the change applying only to runs from here on.

### Does reusing a value push back its expiration?

No. A saved value expires a set time after the provider produced it, and serving it again doesn't restart that clock. Once the window lapses the next run buys the data fresh and saves it with a new date.

### Does a reuse choice travel with a preset or a recipe?

No. Reuse is a choice about the one step you set it on, so a preset or recipe leaves it behind and a column built from one starts from whatever the destination workspace has set as its default. Set reuse on the new column if you want it.

### Why didn't an enrichment reuse a value a teammate's run already paid for?

Saved values never leave your workspace, but where an enrichment runs on a connected account of your own, they're kept separately per account. That separation is there because some providers return different answers to different accounts, so one account's result isn't safe to hand to another.
