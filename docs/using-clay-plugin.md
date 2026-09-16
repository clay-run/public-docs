---
title: Guide: Using Clay plugin
description: Step-by-step guide to three go-to-market plays you can run from a coding agent using the Clay plugin — sourcing your total addressable market, scoring it for ICP fit, and routing high-scoring accounts.
last_synced: 2026-09-16T20:00:09.693Z
---

# Guide: Using Clay plugin

Three go-to-market plays you can run from a coding agent with the Clay plugin: sourcing your addressable market, scoring it for fit, and prioritizing who gets worked first.

Go-to-market plays you can run from a coding agent with the Clay plugin — source your market, score it for fit, and prioritize who gets worked first.

After installing the Clay plugin, here are some go-to-market use cases to help you get started. Each play has a prompt that you can customize for your own business case.

The three plays build on each other. Source the companies and people who match your ideal customer profile, score them so you know who deserves a rep's time, then route the best ones to whoever will work them. Take them in order, or jump straight to the one you need.

You'll need the plugin installed and signed in first, which the [**Clay Agent Plugin (API & CLI)**](https://university.clay.com/docs/clay-api-cli) doc covers. And if you'd rather work in code than in prompts, every play here has an equivalent in Clay's developer docs at [**developers.clay.com**](https://developers.clay.com/).

**Note:** Anything that writes records into Audiences — Clay's home for your workspace's own people, companies, and deals — needs Audiences enabled for your workspace. Searching Clay's data and scoring records you hand the agent directly both work without it.

## Writing a prompt an agent can act on

Your agent already knows Clay. The plugin ships with Clay's mental models — when a workflow beats a one-off lookup, how people and company data fit together, and the habits that keep credit use down — so you're briefing something that knows the tool rather than teaching it from scratch.

The prompt is still what separates a great result from a vague one. Five habits do most of the work:

-   **Say who you are and what the list is for.** Context beats a bare instruction — it shapes the filters your agent picks and the judgment calls it makes.
-   **Answer the questions it would otherwise ask.** Tie-breakers, exclusions, which record to prefer when two match. Every decision you make up front turns five exchanges into one.
-   **Set the quality bar out loud.** "Leave the email blank if it can't be verified — no guessed addresses" gets you blanks where the data doesn't exist, which is the right answer. A bounced email costs more than an empty cell.
-   **Ask for a plan and an estimate before anything spends.** Then approve with a cap rather than a bare yes.
-   **Name what gets built.** A workflow called `ICP fit score` is findable later; one called `test` isn't.

Two more habits pay off on the bigger plays. Ask for the plan first and read it before you say go — revising a plan in plain English costs nothing, while revising a built workflow costs a rebuild.

And if your agent starts hunting through your workspace for "your list," interrupt it and tell it to use the list from the conversation. One line saves several minutes.

## Play 1: Source your total addressable market

Your addressable market is every company you could sell to, including the ones your CRM has never heard of. This play pulls them out of Clay's go-to-market dataset and into your workspace, filtered to your ideal customer profile.

Because sourced records land in Audiences rather than in a single table, the size of your market isn't capped by a table's row limit.

Copy this prompt and swap in your own business and criteria:

`I'm on the revenue operations team at a company that sells scheduling software to independent hotels. Using Clay, find me 50 independent hotels in the US with fewer than 500 employees that are either hiring a revenue manager right now or still running legacy booking software. Show me the list with company names and websites, and tell me how many are already in our companies segment so we don't pay to source the same accounts twice.`

Three things to know about what comes back:

-   **Searches cover people and companies.** A [search](https://university.clay.com/docs/search) runs structured filters over Clay's dataset and hands back records of one of those two kinds. Hiring activity, news, and funding are filters on those records rather than result types of their own, so "companies hiring a revenue manager" hands you companies. Say which of the two you want back.
-   **Results arrive a page at a time, and the search only moves forward.** Ask for the whole list in one go; there's no going back to re-read an earlier page.
-   **Count before you source.** Counting what your workspace already holds is free and instant, so it's the cheapest way to avoid paying twice for records you have.

Sourced records reach Audiences through a step in a Clay workflow rather than a direct import. A segment is the container they land in — a named, live filter over your records, so its membership keeps up as those records change. Ask for it explicitly:

`Take the hotels from this conversation and build me a Clay workflow that writes them into a new companies segment called "Independent hotels — US".`

For the code-level version of this play, see the [search-and-enrich recipe](https://developers.clay.com/recipes/search-and-enrich) in Clay's developer docs.

To keep the play running instead of sourcing by hand, ask for a `Source on a schedule` trigger: it re-runs your search on a schedule and starts one run per new record it finds. It's rolling out gradually, so you may not see it in your workspace yet.

The same play covers two other standing requests. Ask for your results split by territory and you get per-rep starting lists out of a single prompt, which is the quickest way to get a new hire productive.

Ask for companies that resemble your closed-won accounts and you get a lookalike list instead of a filter-built one — worth re-running each quarter as your win list grows.

## Play 2: Score and qualify with an ICP fit score

A list is only worth having once you know which rows deserve a rep's time. An ICP fit score gives you a number and the reasoning behind it, produced by a [Workflow](https://university.clay.com/docs/workflows) so that every account is judged the same way.

Start with the plan, not the build:

`Design a Clay workflow that scores how well an account fits our ideal customer profile. It takes a company as input, disqualifies chains, franchises, and soft brands, enriches whatever survives with firmographics and a verified work email for the property's general manager, then scores fit from 1 to 10 with a written reason for the score. Decisions so you don't need to ask: leave the email blank if it can't be verified, with no guessed addresses and no generic inbox addresses; skip the paid enrichment steps on anything already disqualified. Present a short plan with the top three risks before you build anything, and name the workflow "ICP fit score".`

Read the plan, say what you'd change in plain English, and only then hand over the build:

`The plan looks good. Build it as a Clay workflow in my workspace, then test it on one company from this conversation. Show me the run results, fix anything that fails, and keep going until a test run passes end to end. Show me the estimated cost before anything that spends.`

A few notes on the result:

-   **The written reason is the point.** Claygent, Clay's AI research agent, does the research and writes the reasoning, so a score you disagree with comes with an explanation you can argue with.
-   **Qualify before you enrich.** Putting the disqualification step ahead of the paid steps means a bad-fit account costs you almost nothing.
-   **Ask for a sample, not the whole segment.** Segment runs are bounded, so say how many records to put through — a handful first, the rest once you trust the scores.

The [build-a-Workflow recipe](https://developers.clay.com/recipes/build-workflow-alpha) in the developer docs is the same play written as code.

## Play 3: Prioritize and route what you scored

A score changes nothing until it moves a record. This play takes what your scoring workflow produced, ranks it, and puts each band in front of the person who'll act on it.

`Extend the ICP fit score workflow to route what it scores: 8 and above into an outbound segment, 4 to 7 into an ads segment, below 4 into nurture, and post a Slack message to #pipeline-alerts whenever an account scores 8 or above. Build the Slack step and the segment writes to preview what they would send or write first, so I can check them before anything goes out for real.`

Keep that last sentence as a habit. A preview run lets you read the exact Slack message and the exact segment write before either one happens.

To rank rather than route, ask for the top of the list by score. A sorted read hands back the top of the ranking rather than everything, which is what a rep's daily queue wants anyway. The **Audiences for agents and the CLI** doc covers how those reads behave in more detail.

For prioritization that reacts to events rather than a timer, point the workflow at an `On a signal` trigger. [Signals](https://university.clay.com/docs/signals) are Clay's watches on real-world change, covering a job change, a new hire, a promotion, a new job posting, company news including funding, and research into topics you care about.

Then query your own machine from chat, without opening Clay:

`Which ten accounts in the outbound segment scored highest, and what's the one-line reason for each? Then show me the exact Slack message the workflow would have sent for the top one.`

## Choosing when a play runs

Every play above starts as something you run by hand. Give it a trigger and it runs itself:

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

Describe any of these in plain language and let your agent wire it up. "Run this every Monday morning" or "run it whenever an account joins the outbound segment" is enough to go on.

## Keeping an agent on budget and on track

These aren't specific to any one play. They're the habits that make agent-driven work feel predictable:

-   **Ask for the cost, then approve with a cap.** Treat the number as a planning figure rather than a quote — Clay publishes a base price per action, which an agent can add up but can't turn into a guaranteed total for your configuration.
-   **Check the real cost afterward.** Every run reports the data credits and action credits it actually used, so ask for that on the first run of anything you plan to repeat.
-   **Long silences mean it's working.** Enrichment and a build take minutes, and resending the prompt doubles both the work and the spend. Ask "what's your status?" instead.
-   **A first test failure is normal.** The useful pattern is an agent that hits an error, patches it, and reruns. Step in only if it loops on the same error several times — then ask it to explain what's failing and give you two options.
-   **A low score is the gate working.** An account that comes back disqualified with the paid steps skipped is your qualification logic saving money, not a broken run.

**More use cases from the Clay team:**

-   Spencer's event lead scanner — scan a contact at an event, then enrich, qualify, and route them so reps can book a meeting on the spot.
-   Luca's shared prospecting workflow — turns one rep's process into a team-wide one that finds contacts, verifies emails, and drafts outreach.
-   Chris's post-event follow-up — turns event leads into personalized Sequencer emails.
-   Alex's leadership org chart — pulls contacts, researches a company's executive team, and builds a full org chart of its leadership.
-   Rana's bug bot — investigates failing workflow runs, proposes fixes, and applies them through the CLI after human approval.
-   Andrew's signals-to-pipeline workflow — turns product signals into enterprise pipeline.
-   Mopi's account research workflow — researches a company's business, hiring, tech stack, and recent signals to recommend a use case and an outreach angle.
-   Bhaumik's engagement dashboard — connects engagement on employees' posts to target account tiers, showing which posts reach the right customers.

## FAQs

### Can I search for job postings or news directly?

Not as a result on their own. Job postings, news, and funding are criteria you filter people and companies by, so the thing you get back is always a person or a company.

That distinction is worth making explicit in your prompt. "Companies hiring a revenue manager" returns companies, while "people at companies hiring a revenue manager" returns the contacts at them — same underlying criteria, different list.

### Do I have to publish a workflow before it does anything?

Only before a trigger can use it. Test runs use the current draft, which is what lets you build, run, fix, and rerun without committing to anything.

Publishing makes the current draft the live version for the triggers that aren't paused. Edits you make afterward stay in the draft until you publish again, so a scheduled or signal-driven play keeps running the version you last published.

### A run says `waiting` — is it stuck?

Usually not. `waiting` means the run is sitting on a step that hasn't come back yet, or waiting its turn behind other runs, and it picks up again on its own.

`paused` is the one that needs you: it means someone stopped the run, and it stays stopped until it's resumed. `failed` means it ended with an error, and the run report names the step that caused it.

### How do I find out which accounts have already been through a play?

Ask for the runs rather than the records. Workflow runs are queryable by status and by date, so "show me every run of the ICP fit score workflow that failed this week" or "how many accounts went through it yesterday" are both single questions.

That's also the quickest way to spot a play that has quietly stopped producing: a healthy schedule shows a steady run count, and a broken one shows none.
