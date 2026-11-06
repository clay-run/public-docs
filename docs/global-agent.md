---
title: Clay (global agent)
description: Use Clay's global agent (Alpha) to plan, build, and run go-to-market tasks across Workflows, Audiences, Find leads, Sequencer, Signals, and tables, including scheduling, context, and permissions.
last_synced: 2026-10-07T23:01:12.687Z
---

# Clay (global agent)

Chat with Clay, our global agent, to build and run go-to-market plays: it plans, analyzes, and carries out work across many of Clay's surfaces.

`Agent` is the main tab where you work with our global agent. Tell the global agent what you’re trying to do, and it works across our products to help you get it done.

You can also open the global agent from the Agent icon in the top right bar, which opens the chat interface within the page you’re working on. Agent is available in Workflows, Search, or the home screen.

**Note:** `Agent` is in Alpha and available on Enterprise, Growth, and Launch plans. Results may not always be accurate while it is in Alpha, so check its work before you rely on it.

**Note:** Chatting with Clay’s global agent is free while in Alpha. However, any downstream work (like enrichments and workflow runs) will consume credits like usual.

## Global agent capabilities

Our global agent allows you to easily interact with Clay’s existing products.

| Where in Clay | What the global agent does there |
| --- | --- |
| Workflows | Reads, builds, and updates workflows, adds enrichment steps, and can run an Account Agent as a step. |
| Audiences | Reads and analyzes your records, and creates and updates segments and fields. |
| Find leads | Finds net-new companies and people in Clay’s own dataset, and can leave out accounts you already have. |
| Sequencer | Reads campaigns, creates them, edits their copy and settings, runs a spam check, and sends one test email. You launch the campaign yourself. |
| Signals | Creates the common signal types — job changes, promotions, new hires, job posts, and news — and reads what they pick up. A signal the global agent creates stays paused until you resume it. |
| Workbooks & tables | Reads, queries, and analyzes a table, and can rebuild one as a workflow. Building or editing the table itself stays with Sculptor. |

## Global agent vs Sculptor

Previous Sculptor entry points in Workflows, Search, and the home screen now open the global agent. Sculptor has not moved in tables or in Claygent Builder, where it keeps its own chat history.

So in a table and in Claygent Builder you may see two chats. They differ in what each one is for:

-   **The global agent** analyzes a table, and rebuilds one as a workflow — hand it several tables and it will consolidate them into one. _It cannot build or edit a table for you._
-   **Sculptor** builds and edits a table, and writes a Claygent prompt.

See [Sculptor](https://university.clay.com/docs/sculptor) for what it does inside a table and in Claygent Builder.

## Global agent vs Clay CLI

Clay’s global agent runs on the same engine as the Clay CLI, so anything you can do from the command line you can do here, with Clay’s own interface around it. See [Clay API and CLI](https://university.clay.com/docs/clay-api-cli) for the command-line route. Which one you reach for comes down to how you want to work.

|  | Global agent | Clay CLI |
| --- | --- | --- |
| Best for | Getting work done in Clay with guidance, whether or not you write code. | People who already work inside a coding agent. |
| Experience | Previews, links, and artifacts you can open, check, and refine without leaving Clay. | Scripts, custom logic, and wiring Clay into systems outside it. |
| Context | Starts from your Knowledge Hub, so your business context is already there. | You supply and maintain the context each run needs. |
| Ongoing work | Recurring tasks you schedule in the product. | More flexible, but you build the orchestration and guardrails yourself. |

For the tools themselves, see [Workflows](https://university.clay.com/docs/workflows), [Audiences](https://university.clay.com/docs/audiences), [Search](https://university.clay.com/docs/search) for `Find leads`, [Sequencer](https://university.clay.com/docs/getting-started-with-sequencer), and [Signals](https://university.clay.com/docs/signals). [Account Agents in Workflows](https://university.clay.com/docs/account-agents-in-workflows) covers the workflow step that researches one account at a time, and when to add one.

## Starting a task

1.  Open `Agent` in the left nav, then select `New task`. The start screen asks `What should we work on today?`.
    -   The suggested prompts are based on your workspace context.
2.  Say what you want to end up with, not just what you want to look at. “Save these to a segment” and “build this as a workflow” get you something you can use; “show me some accounts” stops at a list.
    -   The global agent’s own examples are shaped this way: `Route inbound leads`, `Build a prospecting workflow`, `Score and prioritize accounts`, `Build and enrich a lead list`.
3.  Say what to leave out. Accounts you already own, and anyone you’ve already engaged — naming them up front is what keeps them out of the results.
4.  Answer the questions it comes back with. The global agent asks for the detail you left out before it starts building, and you can `Skip` any question you’d rather not answer. Closing the question card instead stops the task.
5.  Open what it built. The `Artifacts` panel collects what the global agent made in this task.

## Scheduling a task to repeat

You can ask the global agent to make any task recurring, so the same work runs on a cadence instead of once — daily, on weekdays, weekly, or monthly. Recurring tasks live under `Scheduled` in the `Agent` sidebar.

Each schedule keeps the `Instructions` it follows, its `Next run`, and every run it has had, so you can read back what changed between one run and the next. A run that needs an answer from you waits rather than guessing, and the schedule stands still until you reply.

You can pause a schedule, run it early, or end it from the schedule’s own page.

## Giving the global agent more context

The global agent starts from your `Knowledge Hub`, your workspace’s record of what you sell and who you sell it to. When a task should lean on something specific, add a reference to it as you write the message:

-   Type `@` for a part of your `Knowledge Hub`, or a document you’ve uploaded there.
-   Type `$` or `/` for your `Workspace skills`, the instructions your team has written for work the global agent does often. Your team creates them on the `Agent skills` page in workspace settings.
-   Select `Attach file` to add one or more files to a message: spreadsheets including CSVs, PDFs, Word documents, text files, and images, up to 50 MB each.

**Note:** One message can carry up to 50 references. Add more and the send button stays locked until you remove some.

See [Knowledge Hub](https://university.clay.com/docs/knowledge-hub) for what lives there and how to change it.

## Permissions and approvals

Every task and every schedule carries a permission level that decides what the global agent does without stopping to ask. `Allow changes` is the default. Set it in the message box before you send a task, and on a schedule’s own page for runs nobody is watching.

| Level | What it allows |
| --- | --- |
| Allow changes | The global agent edits freely and runs test data. It waits for your approval before running a workflow outside test data, and before deleting a workflow, a Claygent, or a schedule. |
| Allow everything | Nothing waits for approval, including workflow runs and deletions. |

**Note: a task or schedule set up before `View only` was retired still shows it.** Nothing breaks, and saving a change to that task or schedule means picking one of the two levels above.

### What runs without asking

`Allow changes` holds a short, specific list, so plenty of real work — including work that spends credits — goes ahead on its own. Before you leave a task running, it’s worth knowing that these need no approval:

-   Runs on a trigger’s records: a CSV’s rows, a `Find leads` search’s results, or a segment’s members.
-   Publishing a workflow, which turns on its live triggers so runs start from new events.
-   Resuming a paused run, testing a single action or code step, function runs, and searches.
-   Creating or resuming a signal, which then checks records on a schedule.

Deletions outside that list go ahead too: archiving a segment, deleting a segment field, a signal, a webhook, or an API key, and taking a destination off a draft ad sync.

The same goes for credentials and billing — creating, renaming, or deleting an API key, turning auto top-ups on or off, and starting a credit purchase, which you still complete yourself. Sending a test email from a campaign, or a test event to a webhook, needs no approval either.

## What the global agent won’t do on its own

The global agent works through a task without stopping for approval at each step, so it’s worth knowing where it stops on purpose. The actions that reach people outside your workspace, or that you can’t take back, stay with you:

-   **It won’t launch or send a campaign.** The global agent drafts one, edits the copy and settings, runs a spam check, and sends a single test email. Starting it, pausing it, and completing it happen in Sequencer, by you.
-   **A signal it creates starts paused**, so you can read it back before it starts checking records and spending credits. It resumes the signal once you confirm, not on its own initiative.
-   **It won’t create or edit a table.** Ask it to rebuild one as a workflow instead.
-   **It won’t delete a campaign or an ad sync.** It can take a destination off an ad sync that’s still a draft.

Everywhere else the global agent acts as it goes, and that includes spending credits on enrichments and workflow runs. So the checkpoint is you reading its work, not it asking permission: open the `Artifacts` panel, check the workflow or segment it produced, then run it yourself once it looks right.

It does come back to you mid-task when a decision is genuinely yours and would change the outcome — which list to start from, which of two scoring approaches to take. It gathers those onto one card rather than interrupting you repeatedly.

## FAQs

### Why is this taking a few minutes?

Work that spans several steps runs for as long as it needs and shows its progress as it goes, so a task that builds something takes longer than one that answers a question. Your task list marks it `Working` while it runs, and `Unread` when there’s something new.

You don’t have to wait it out — send your next message while it runs and the global agent queues it, marked `Sends after this run`. `Stop` ends a run you no longer want, and you can send again straight away. If a run fails, the partial output is saved and the task offers `Retry`.

### Can my teammates see a task I started?

Only if you share it. Select `Share task`, turn on `Share with workspace`, and copy the `Task link`.

Anyone in the workspace with that link can read the task’s saved messages. They can’t send anything in it, and only the person who started a task can rename it.

### Does the global agent know which page I’m looking at?

Yes. The global agent can see the page you have open, so you can ask about what’s in front of you — “score the accounts in this segment”, “why is this workflow failing” — without naming or linking it first. Opening the global agent inside a workflow, an audience, or a search also changes the suggested prompts to match.

### Why don’t I see `Agent` in my workspace?

The global agent is rolling out gradually during Alpha, so you may not see it yet even once it has reached other people.

If you’re an Enterprise customer and want to try it, ask your Growth Strategist for access. On a Growth or Launch plan, sign up for the early adopter program, then have a Workspace Admin turn on `Beta program` in your workspace settings. Clay notifies you in the product once you have access.
