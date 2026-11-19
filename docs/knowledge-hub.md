---
title: Knowledge Hub
description: A reviewable record of what you sell, who you sell to, and which signals matter — drafted by Clay, edited and approved by workspace admins.
last_synced: 2026-11-19T07:44:08.380Z
---

# Knowledge Hub

Keep one reviewable record of your business in Clay — what you sell, who you sell to, and what signals matter — that Clay drafts and you edit.

`Knowledge Hub` is a tab at the top of Clay’s main left nav.

It’s a living record of what you sell, who you sell to, and which signals matter. Clay builds it from your website and public information, your workspace activity, your chats with Clay, and documents you upload or connect from Notion, Google Drive, and GitHub, so every play starts with context specific to your business. Clay keeps proposing updates as it learns, and you accept or dismiss each one.

**Note:** `Knowledge Hub` is in beta and rolling out gradually, so you may not see it in your workspace yet. Making and approving edits, including adding documents and connecting apps, needs the `Admin` role. If you can read the page but not change it, ask a workspace admin to make the change for you.

Clay fills in the same five sections for every workspace:

-   `Company Description`
-   `Ideal Customer Profile`
-   `Buyer Personas`
-   `Interest Signals`
-   `End Market`

You can add up to three sections of your own.

Clay, [our global agent](https://university.clay.com/docs/global-agent), works in the `Agent` tab, and every task you hand it starts from your `Knowledge Hub`.

**Note:** Clay will automatically create your `Knowledge Hub` — you don’t set it up. It starts from the company domain Clay already has for your workspace, and writes the five sections for you. Only when Clay has no domain it can use does `Knowledge Hub` open on the `Clay works better when it knows your business` screen, where you can start it from the `Company website` field, a file, or a connected app.

## Reviewing and editing your Knowledge Hub

1.  When Clay has an update to propose from your workspace activity or an uploaded document, the page shows `Review suggestions` with a count. Selecting it narrows the page to what’s waiting, and `Show all sections` brings the rest back. Only workspace admins see suggestions.
2.  Read the change and choose `Accept` or `Dismiss`. Accepting writes the change into the section; dismissing leaves the section as it is. Each suggestion carries its own pair, so you decide them one at a time.
    -   One suggestion can change several sections at once. It shows up under each of them, and a single `Accept` applies all of its changes.
3.  Once a section has no suggestions waiting, you can edit it yourself:
    -   `Edit`, to rewrite a section.
    -   `Add subsection`, in the menu on `Ideal Customer Profile` and `Buyer Personas` — one customer profile or persona at a time, up to five each.
    -   `Add section`, for one of your own.
    -   `Delete`, in the menu on any subsection, or on a section you added. Deleting a section takes its subsections with it, and neither can be undone.

A section Clay hasn’t written yet shows a short hint instead of a body, with `Write section` to fill it in yourself.

## Adding documents and apps

Your documents sit in the `Context` panel, beside your sections — up to 20 of them, counting files you upload and documents from connected apps together. You can remove one there, and uploading a file with the same name replaces it. Removing a document doesn’t undo what it already contributed.

1.  In `Context`, select `Add from files or apps`.
2.  Choose `Files` to upload from your computer, or `Notion`, `Google Drive`, or `GitHub` to add documents from an app.
    -   The first time, sign in to connect the app. The connection is shared across your workspace, and with Notion you choose which pages Clay can read.
3.  Select what you want, then `Save changes`. Clay reads each document and proposes any changes as suggestions.

This table shows what you can add to your `Knowledge Hub` from each source:

| Add from | What you can add |
| --- | --- |
| Files | Markdown, text, or CSV up to 1,000,000 characters, and PDF, PowerPoint, or Word up to 10 MB |
| Notion | Pages shared with Clay, but not databases |
| Google Drive | Google Docs and Slides, plus PDF, PowerPoint, Word, text, Markdown, and CSV files, up to 10 MB each |
| GitHub | Markdown and text files under 1 MB, from repositories your GitHub account can access |

`Knowledge Hub` only reads from connected apps. To pull in recent edits from them, select `Refresh from connected apps`, the refresh icon beside `Context`.

To disconnect an app, open it from `Add from files or apps`, open the `Connection` menu, and choose `Disconnect…`. Its documents leave your `Knowledge Hub`, and your sections and the app’s account in Clay stay as they are.

## Refining your Knowledge Hub with our global agent

As a workspace admin, you can ask our global agent to update your `Knowledge Hub`, or select `Refine your context` in the `Keep building` panel to start a chat where it asks about your business. Each change it proposes shows up in the chat as a suggestion you can `Accept` or `Dismiss`, and it waits under `Review suggestions` too. Nothing changes until it’s accepted. If five suggestions are already waiting, accept or dismiss one before asking for another.

## Using the Clay CLI

The Clay CLI, our command-line tool, can read your `Knowledge Hub` and work with its suggestions from a terminal or a coding agent. To set it up, see [Installing Clay Plugin (API & CLI)](https://university.clay.com/docs/clay-api-cli). Its commands sit under `clay knowledge-hub business-context`:

| Command | What it does |
| --- | --- |
| clay knowledge-hub business-context get | Reads your sections and subsections |
| clay knowledge-hub business-context propose | Opens a suggestion for review, from a proposal passed with --input and a unique --request-id |
| clay knowledge-hub business-context suggestions list | Lists the suggestions waiting for review |
| clay knowledge-hub business-context suggestions get | Shows one suggestion’s changes against your current text, by its ID |
| clay knowledge-hub business-context suggestions accept | Accepts a suggestion, with --review-revision naming the version you reviewed |
| clay knowledge-hub business-context suggestions reject | Dismisses a suggestion, with an optional --reason |

Proposing, accepting, and rejecting need the `Admin` role, and a proposal changes nothing until it’s accepted. Add `--help` to any command for its input format and examples.

## FAQs

### What does Clay use my `Knowledge Hub` for?

Every task you hand our global agent starts from it, so you don’t re-explain your business each time. It shapes which accounts Clay looks for, how it scores and prioritizes them, and the copy it drafts.

You can also point one message at a single piece of it. Type `@` in the agent’s message box to pull in a whole section (including one you added yourself), a single customer profile or persona, or a document you’ve uploaded. Prompts in Claygent, Clay’s AI research agent, and in Sequencer campaigns offer the same sections and subsections in their `@` menu, under `My business context`.

### Where did the `AI context` page in workspace settings go?

Your business context lives in `Knowledge Hub` now. The `AI context` page no longer appears in workspace settings once your workspace has one, and an old bookmark or link into it opens `Knowledge Hub` instead.

### When does my Knowledge Hub update?

Adding or removing a document, or disconnecting an app, starts an update right away. Past that it’s always on: as Clay learns from your workspace activity and your chats with it, it proposes a change whenever something in your sections should change. A stretch can pass with nothing waiting for you, and if you leave one of Clay’s suggestions waiting, a later update can replace it with a fresh one.

### Does Knowledge Hub cost anything?

No, `Knowledge Hub` itself is free. Refining it in a chat with our global agent spends credits the same way any other chat with it does. See [Clay (global agent)](https://university.clay.com/docs/global-agent) for how that works.
