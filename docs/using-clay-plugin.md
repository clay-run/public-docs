---
title: Guide: Using Clay plugin
description: Three go-to-market plays you can run from a coding agent with the Clay plugin — sourcing your addressable market, scoring records for ICP fit, and routing accounts by score.
last_synced: 2026-09-16T19:06:14.064Z
---

# Guide: Using Clay plugin

Three go-to-market plays you can run from a coding agent with the Clay plugin: sourcing your addressable market, scoring it for fit, and prioritizing who gets worked first.

The Clay plugin doc covers getting installed and signed in. This one covers what to do next — three plays a go-to-market team runs constantly, taught as the prompts you send a coding agent rather than as code you write yourself.

The plays build on each other. You source companies and people who match your ideal customer profile, score what you sourced so you know which records deserve time, then rank and route the survivors so the right accounts reach the right rep. Each one also stands on its own if that's the only part you need.

Everything below assumes the plugin is installed and you're signed in, which the [**Clay Agent Plugin (API & CLI)**](https://university.clay.com/docs/clay-api-cli) doc walks through. For the code-level version of these plays — endpoints, request shapes, and paging — see [**developers.clay.com**](https://developers.clay.com/).

**Note:** Anything that writes records into Audiences — Clay's home for your workspace's own people, companies, and deals — needs Audiences enabled for your workspace. Searching Clay's data and scoring records you hand the agent directly both work without it.

## Writing a prompt an agent can act on

The gap between a useful result and a vague one is almost entirely in the prompt. Five habits carry most of the difference:

-   **Say who you are and what the list is for.** Context the agent can lean on beats a bare instruction — it shapes the filters it picks and the judgment calls it makes.
-   **Answer the questions it would otherwise ask.** Tie-breakers, exclusions, which record to prefer when two match. Every decision you make up front turns five exchanges into one.
-   **Set the quality bar out loud.** "Leave the email blank if it can't be verified — no guessed addresses" gets you blanks where the data doesn't exist, which is the right answer. A bounced email costs more than an empty cell.
-   **Ask for a plan and an estimate before anything spends.** Then approve with a cap rather than a bare yes.
-   **Name what gets built.** A workflow called `ICP fit score` is findable later; one called `test` isn't.

Two more habits pay off on the bigger plays. Ask for the plan first and read it before you say go — revising a plan in plain English costs nothing, revising a built workflow costs a rebuild.

And if the agent starts hunting through your workspace for "your list," interrupt it and say to use the list from the conversation. One line saves several minutes.

## Play 1: Source your total addressable market

Your addressable market is every company you could sell to, including the ones your CRM has never heard of. This play pulls them out of Clay's go-to-market dataset against your ideal customer profile.

Copy this prompt and swap in your own business and criteria:

`I'm on the revenue operations team at a company that sells scheduling software to independent hotels. Using Clay, find me 50 independent hotels in the US with fewer than 500 employees that are either hiring a revenue manager right now or still running legacy booking software. Show me the list with company names and websites, and tell me how many are already in our companies segment so we don't pay to source the same accounts twice.`

Three things to know about what comes back:

-   **Searches cover people and companies.** A [search](https://university.clay.com/docs/search) runs structured filters over Clay's dataset and hands back records of one of those two kinds. Hiring activity, news, and funding are filters on those records rather than result types of their own, so "companies hiring a revenue manager" hands you companies. Say which of the two you want back.
-   **Results arrive a page at a time, and the search only moves forward.** Ask for the whole list in one go; there's no going back to re-read an earlier page.
-   **Count before you source.** Counting what your workspace already holds is free and instant, so it's the cheapest way to avoid paying twice for records you have.

Getting the sourced records into Audiences happens through a step in a Clay workflow rather than a direct import. A segment is the container they land in — a named, live filter over your records, so its membership keeps up as those records change. Ask for it explicitly:

`Take the hotels from this conversation and build me a Clay workflow that writes them into a new companies segment called "Independent hotels — US".`

For the code-level version of this play, see the [search-and-enrich recipe](https://developers.clay.com/recipes/search-and-enrich) in Clay's developer docs.

To keep the play running instead of sourcing by hand, ask for a `Source on a schedule` trigger: it re-runs your search on a schedule and starts one run per new record it finds. It's rolling out gradually, so you may not see it in your workspace yet.

## Play 2: Score and qualify with an ICP fit score

A sourced list is only useful once you know which rows deserve a rep's time. An ICP fit score is a number plus a written reason, produced by a [Workflow](https://university.clay.com/docs/workflows) — Clay's canvas for repeatable go-to-market logic — so that every record is judged the same way.

Ask for the plan first:

`Design a Clay workflow that scores how well an account fits our ideal customer profile. It takes a company as input, disqualifies chains, franchises, and soft brands, enriches whatever survives with firmographics and a verified work email for the property's general manager, then scores fit from 1 to 10 with a written reason for the score. Decisions so you don't need to ask: leave the email blank if it can't be verified, with no guessed addresses and no generic inbox addresses; skip the paid enrichment steps on anything already disqualified. Present a short plan with the top three risks before you build anything, and name the workflow "ICP fit score".`

Read the plan, say what you'd change in plain English, and only then hand over the build:

`The plan looks good. Build it as a Clay workflow in my workspace, then test it on one company from this conversation. Show me the run results, fix anything that fails, and keep going until a test run passes end to end. Show me the estimated cost before anything that spends.`

A few notes on the result:

-   **The written reason is the point.** Claygent, Clay's AI research agent, is what does the research and writes the reasoning, so a score you disagree with comes with an explanation you can argue with.
-   **Qualify before you enrich.** Putting the disqualification step ahead of the paid steps means a bad-fit account costs you almost nothing.
-   **Ask for a sample, not the whole segment.** Segment runs are bounded, so say how many records to put through — a handful first, the rest once you trust the scores.

The [build-a-Workflow recipe](https://developers.clay.com/recipes/build-workflow-alpha) in the developer docs is the same play written as code.

## Play 3: Prioritize and route what you scored

Scores only change anything once they move records. This play ranks what the scoring workflow produced and sends each band somewhere a person will actually look.

`Extend the ICP fit score workflow to route what it scores: 8 and above into an outbound segment, 4 to 7 into an ads segment, below 4 into nurture, and post a Slack message to #pipeline-alerts whenever an account scores 8 or above. Build the Slack step and the segment writes to preview what they would send or write first, so I can check them before anything goes out for real.`

That last sentence is worth keeping as a habit: a preview run lets you read the exact Slack message and the exact segment write before either one happens.

To rank rather than route, ask for the top of the list by score. A sorted read hands back the top of the ranking rather than everything, which is what a rep's daily queue wants anyway. The **Audiences for agents and the CLI** doc covers how those reads behave in more detail.

For prioritization that reacts to events rather than a timer, point the workflow at an `On a signal` trigger. [Signals](https://university.clay.com/docs/signals) are Clay's watches on real-world change, covering a job change, a new hire, a promotion, a new job posting, company news including funding, and research into topics you care about.

Then query your own machine from chat, without opening Clay:

`Which ten accounts in the outbound segment scored highest, and what's the one-line reason for each? Then show me the exact Slack message the workflow would have sent for the top one.`

## Choosing when a play runs

A workflow does nothing until something starts it. These are the options:

| Trigger | When it fires |
| --- | --- |
| Run manually | You or your agent start a single run and pass the record in. |
| New member in segment | A record joins the segment you pointed it at. |
| Segment on a schedule | Members of a segment, on a repeating schedule. |
| On a signal | A signal fires against a person or company. One trigger per signal. |
| On a schedule | On a repeating schedule, with no record attached. |
| Source on a schedule | A saved search looks for records and starts one run per record it finds. |
| On webhook call | Another system posts a payload to the workflow. |
| On CSV upload | A file is uploaded to the workflow. |

You can describe any of these in plain language and let the agent wire it up — "run this every Monday morning" or "run it whenever an account joins the outbound segment" is enough to go on.

## Keeping an agent on budget and on track

Nothing here is specific to one play. These are the reflexes that make an agent-driven build feel predictable:

-   **Ask for the cost, then approve with a cap.** Treat the number as a planning figure rather than a quote — Clay publishes a base price per action, which an agent can add up but can't turn into a guaranteed total for your configuration.
-   **Check the real cost afterward.** Every run reports the data credits and action credits it actually used, so ask for that on the first run of anything you plan to repeat.
-   **Long silences mean it's working.** Enrichment and a build take minutes, and resending the prompt doubles both the work and the spend. Ask "what's your status?" instead.
-   **A first test failure is normal.** The useful pattern is an agent that hits an error, patches it, and reruns. Step in only if it loops on the same error several times — then ask it to explain what's failing and give you two options.
-   **A low score is the gate working.** An account that comes back disqualified with the paid steps skipped is your qualification logic saving money, not a broken run.
