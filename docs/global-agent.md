---
title: Clay (global agent)
description: Chat with Clay's global agent (Beta) to plan, build, and run go-to-market work across Workflows, Audiences, Search, Sequencer, and Signals, including scheduling, permissions, and credit usage.
last_synced: 2026-11-19T07:45:50.367Z
---

# Clay (global agent)

Chat with Clay, our global agent, to build and run go-to-market plays: it plans, analyzes, and carries out work across many of Clay's surfaces.

`Agent` is the main tab where you work with our global agent. Tell the global agent what you’re trying to do, and it works across our products to help you get it done.

You can also open the global agent from the Agent icon in the top right bar, which opens the chat interface within the page you’re working on. Agent is available in Workflows, Search, Audiences, Sequencer, and the home screen.

**Note:** `Agent` is in Beta and available on Enterprise, Growth, and Launch plans, and for a limited time on legacy Starter, Explorer, and Pro plans. Results may not always be accurate while it is in Beta, so check its work before you rely on it.  

Working with the global agent spends data credits. Running what it sets up — enrichments, workflow runs, and other actions — spends credits just as it does when you run them yourself.

## Global agent capabilities

Our global agent allows you to easily interact with Clay’s existing products.

| Where in Clay | What the global agent does there |
| --- | --- |
| Workflows | Reads, builds, and updates workflows, adds enrichment steps, and can run an Account Agent as a step. |
| Audiences | Reads and analyzes your records, and creates and updates segments and fields. |
| Find leads | Finds net-new companies and people in Clay’s own dataset, edits searches you’ve already built, and can leave out accounts you already have. |
| Sequencer | Reads campaigns, creates them, edits their copy and settings, runs a spam check, and sends one test email. You launch the campaign yourself. |
| Signals | Creates the common signal types — job changes, promotions, new hires, job posts, and news — on records in Audiences, and reads what they pick up. A signal the global agent creates stays paused until you resume it. |
| Workbooks & tables | Reads, queries, and analyzes a table, and can rebuild one as a workflow. Building or editing the table itself stays with Sculptor. |

## Global agent vs Sculptor

Previous Sculptor entry points in Workflows, Search, and the home screen now open the global agent. Sculptor has not moved in tables or in Claygent Builder, where it keeps its own chat history.

So in a table and in Claygent Builder you may see two chats. They differ in what each one is for:

-   **The global agent** analyzes a table, and rebuilds one as a workflow — hand it several tables and it will consolidate them into one. _It cannot build or edit a table for you._
-   **Sculptor** builds and edits a table, and writes a Claygent prompt.

See [Sculptor](https://university.clay.com/docs/sculptor) for what it does inside a table and in Claygent Builder.

## Global agent vs Clay CLI

Our global agent runs on the same engine as the Clay CLI, so anything you can do from the command line you can do here, with Clay’s own interface around it. See [Clay API and CLI](https://university.clay.com/docs/clay-api-cli) for the command-line route. Which one you reach for comes down to how you want to work.

|  | Global agent | Clay CLI |
| --- | --- | --- |
| Best for | Getting work done in Clay with guidance, whether or not you write code. | People who already work inside a coding agent. |
| Experience | Previews, links, and artifacts you can open, check, and refine without leaving Clay. | Scripts, custom logic, and wiring Clay into systems outside it. |
| Context | Starts from your Knowledge Hub, so your business context is already there. | You supply and maintain the context each run needs. |

For the tools themselves, see [Workflows](https://university.clay.com/docs/workflows), [Audiences](https://university.clay.com/docs/audiences), [Search](https://university.clay.com/docs/search) for `Find leads`, [Sequencer](https://university.clay.com/docs/getting-started-with-sequencer), and [Signals](https://university.clay.com/docs/signals). [Account Agents in Workflows](https://university.clay.com/docs/account-agents-in-workflows) covers the workflow step that researches one account at a time, and when to add one.

## Starting a task

1.  Open `Agent` in the left nav, then select `New task`. The start screen asks `What should we work on today?`.
    -   The suggested prompts are based on your workspace context.
2.  Say what you want to end up with, not just what you want to look at. “Save these to a segment” and “build this as a workflow” get you something you can use; “show me some accounts” stops at a list.
    -   The global agent’s own examples are shaped this way: `Route inbound leads`, `Build a prospecting workflow`, `Score and prioritize accounts`, `Build and enrich a lead list`.
3.  Say what to leave out. Accounts you already own, and anyone you’ve already engaged — naming them up front is what keeps them out of the results.
4.  Answer the questions it comes back with. The global agent asks for the detail you left out before it starts building, and you can `Skip` any question you’d rather not answer. Closing the question card instead stops the task.
5.  Open what it built. The `Artifacts` panel collects what the global agent made in this task.

## Giving the global agent more context

The global agent starts from your `Knowledge Hub`, your workspace’s record of what you sell and who you sell it to. When a task should lean on something specific, add a reference to it as you write the message:

-   Type `@` for a part of your `Knowledge Hub`, or a document you’ve uploaded there.
-   Type `$` or `/` for your `Workspace skills`, the instructions your team has written for work the global agent does often. Your team creates them on the `Agent skills` page in workspace settings.
-   Select `Attach file` to add one or more files to a message: spreadsheets including CSVs, PDFs, Word documents, text files, and images, up to 50 MB each.

**Note:** One message can carry up to 50 references. Add more and the send button stays locked until you remove some.

See [Knowledge Hub](https://university.clay.com/docs/knowledge-hub) for what lives there and how to change it.

## Permissions and approvals

Every task carries a permission level that decides what the global agent does without stopping to ask. `Allow changes` is the default. Set it in the message box before you send a task.

| Level | What it allows |
| --- | --- |
| Allow changes | The global agent edits freely and runs test data. It waits for your approval before running a workflow outside test data, and before deleting a workflow or a Claygent. |
| Allow everything | Nothing waits for approval, including workflow runs and deletions. |

**Note: a task set up before `View only` was retired still shows it.** Nothing breaks, and changing it means picking one of the two levels above.

### What runs without asking

`Allow changes` holds a short, specific list, so plenty of real work — including work that spends credits — goes ahead on its own. Before you leave a task running, it’s worth knowing that these need no approval:

-   Runs on a trigger’s records: a CSV’s rows, a `Find leads` search’s results, or a segment’s members.
-   Publishing a workflow, which turns on its live triggers so runs start from new events.
-   Resuming a paused run, testing a single action or code step, function runs, and searches.
-   Creating or resuming a signal, which then checks records on a schedule.

Deletions outside that list go ahead too: archiving a segment, deleting a segment field, a signal, a webhook, or an API key, and taking a destination off an ad sync that’s paused or still a draft, or off an always-on sync that failed.

The same goes for credentials and billing — creating, renaming, or deleting an API key, turning auto top-ups on or off, and starting a credit purchase, which you still complete yourself. Sending a test email from a campaign, or a test event to a webhook, needs no approval either.

## What the global agent won’t do on its own

The global agent works through a task without stopping for approval at each step, so it’s worth knowing where it stops on purpose. The actions that reach people outside your workspace, or that you can’t take back, stay with you:

-   **It won’t launch or send a campaign.** The global agent drafts one, edits the copy and settings, runs a spam check, and sends a single test email. Starting it, pausing it, and completing it happen in Sequencer, by you.
-   **A signal it creates starts paused**, so you can read it back before it starts checking records and spending credits. It resumes the signal once you confirm, not on its own initiative.
-   **It won’t create or edit a table.** Ask it to rebuild one as a workflow instead.
-   **It won’t delete a campaign or an ad sync.** It can take a destination off an ad sync that’s paused or still a draft, or off an always-on sync that failed.

Everywhere else the global agent acts as it goes, and that includes spending credits on enrichments and workflow runs. So the checkpoint is you reading its work, not it asking permission: open the `Artifacts` panel, check the workflow or segment it produced, then run it yourself once it looks right.

It does come back to you mid-task when a decision is genuinely yours and would change the outcome — which list to start from, which of two scoring approaches to take. It gathers those onto one card rather than interrupting you repeatedly.

## Credits and pricing

The global agent spends data credits as it works, and the work it sets up spends credits and actions the same way it does when you run it yourself. Two kinds of spend sit behind a task:

-   **The agent’s own work.** Reading your workspace, answering a question, and planning an approach cost very little. Building something — a workflow, a campaign, a segment — costs more, because it takes more steps across more of Clay.
-   **What the agent runs for you.** Enrichments, workflow runs, and other downstream work spend credits and actions as usual. That spend lands under whatever the agent built, not under the agent.

Working with the global agent spends data credits only; it doesn’t consume actions. What you pay for its own work doesn’t change with the model behind it, so a model change on our side never changes your cost. Asking it to redo something, or changing direction partway through a build, spends credits on top of the first attempt.

**Tip:** If you’re not sure what a task will take, ask the global agent to plan it before it builds. Planning is cheap, and you get to check the approach first.

### Free credits in Beta

Every eligible workspace gets free credits to spend on the global agent’s own work — reading your workspace, answering questions, and planning and building what you ask for.

| Plan | Free credits |
| --- | --- |
| Enterprise | 10,000 |
| Growth, Launch, and legacy self-serve plans | 1,000 |

Free credits are spent first. Every message draws on them until they run out, and after that the global agent spends your workspace’s regular data credits. A charge that uses up your last free credits takes what’s left of them and bills the remainder to your regular balance.

Free credits don’t cover what the global agent runs for you. Enrichments, workflow runs, and other downstream work always spend your regular credits and actions. A workspace on a trial gets no free credits, so the global agent spends the credits the workspace already has.

**Note:** Free credits apply during Beta. Pricing may change before general availability, and we’ll post the change here first.

### Keeping an eye on spend

When the global agent stops for your approval, the card carries an `Estimated cost` in credits and action executions before anything runs. Some actions can’t be priced ahead of time, and the card says `Cost can’t be estimated` when that happens.

The permission level you set decides how often you see a card at all, so it’s also the lever on how much runs unwatched.

While your workspace has free credits left, the global agent shows how many of them have been used so far.

To see what the global agent has spent, free credits included, select your account name, go to `Settings` then `Usage`, and open the `Agent` tab. It breaks spend down by person over the period you pick, and anyone who isn’t a Workspace Admin sees only their own. The work the agent set up shows up in the other tabs, under the workflow or table it belongs to.

If your workspace runs out of credits, the global agent stops: you can’t start a new task or send a follow-up until the balance is topped up. Clay tells you so in the task, with `Add credits` alongside.

See [Actions & Data Credits](https://university.clay.com/docs/actions-data-credits) for how the two meters work, and [Credit usage](https://university.clay.com/docs/credit-usage) for the rest of the dashboard.

## FAQs

### Why is this taking a few minutes?

Work that spans several steps runs for as long as it needs and shows its progress as it goes, so a task that builds something takes longer than one that answers a question. Your task list marks it `Working` while it runs, and `Unread` when there’s something new.

You don’t have to wait it out — send your next message while it runs and the global agent queues it, marked `Sends after this run`. `Stop` ends a run you no longer want, and you can send again straight away. If a run fails, the partial output is saved and the task offers `Retry`.

### Can my teammates see a task I started?

Only if you share it. Select `Share task`, turn on `Share with workspace`, and copy the `Task link`.

Anyone in the workspace with that link can read the task’s saved messages. They can’t send anything in it, and only the person who started a task can rename it.

### Does the global agent know which page I’m looking at?

Yes. The global agent can see the page you have open, so you can ask about what’s in front of you — “score the accounts in this segment”, “why is this workflow failing” — without naming or linking it first. Opening the global agent inside a workflow, an audience, or a search also changes the suggested prompts to match.

### Can I speak a message instead of typing it?

Yes. Select `Dictate`, the microphone in the message box, and speak. It works when you start a task, when you follow up, and when you answer one of the global agent’s questions.

When you finish, what you said lands in the message box as text you can edit, and nothing sends until you send it. A recording finishes on its own after five minutes.

### Should I use `Core` or `Deep`?

The picker in the message box sets how much reasoning the global agent puts into your next message. `Core` is the default and covers most everyday work. `Deep` reasons longer, for complex work such as building a new workflow from scratch, and can spend more credits as a result. You can switch between them on any message.
