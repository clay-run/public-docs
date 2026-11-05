---
title: Build your sequence
description: How to write, personalize, and pressure-test campaign sequence messages in Clay before launch, including steps, delays, variables, AI snippets, and pre-send checks.
last_synced: 2026-09-01T03:23:11.480Z
---

# Build your sequence

Write, personalize, and pressure-test the emails your campaign sends — before a single one goes out.

A campaign's `Sequence` tab is where you write the messages, set how far apart they land, and personalize them with your lead data. Everything here happens before launch, so you can iterate freely: preview the copy against real leads from your segment, check how well your fields are filled in, and send yourself a test.

**Note:** A campaign costs 1 action credit per lead enrolled. Adding AI snippets adds a variable number of data credits per lead on top of that, depending on how much work each snippet does. Clay shows you an estimate in the campaign, so you can see what a change to your sequence will cost before you commit to it.

## Adding steps

A sequence holds up to four messages. The first one does most of the work, so give it the most attention — the rest are follow-ups that catch people who didn't respond to it.

1.  Click `Add message` at the bottom of the `Sequence` tab. Each message has its own `Subject` and body, and the button disappears once you reach four.
2.  Open the delay pill between any two messages and pick anything from `Wait 1 day` to `Wait 10 days`.
3.  On every message after the first, set the `Send as reply` toggle. On, the message goes out as a reply on the same thread as the previous email and inherits that thread's subject line; off, it starts a fresh thread with a subject of its own.
4.  To remove a message, open its 3-dot `Message actions` menu and choose `Delete message`. A sequence always keeps at least one message, so `Delete message` is unavailable while a single message is all you have.

Delays count from the previous message in that lead's own sequence, not from when the campaign launched, so leads who enroll later simply run the same spacing on their own clock. Each message can hold up to 8 KB of text, which is comfortably more room than a cold email should ever need.

One thing worth settling before you go live: launching locks the shape of your sequence. The number of messages and their order are fixed once the campaign is live, because changing them mid-flight would break the analytics for leads already part-way through. Copy and step timing both reopen while a campaign is paused, so the delay between two messages is still yours to change.

## Plaintext vs. HTML

Sequences send plaintext by default, and for cold outbound that's the right call. Mailbox providers read heavy HTML as a signal of bulk marketing mail, so a plain message from a person tends to land in the primary inbox where a designed one lands in Promotions.

If you do need rich formatting, turn on `Enable HTML` under `Email format` in the campaign's `Settings`. Clay is upfront about the trade-off in the setting itself: `HTML enables links, images, formatting, and tracking`, and `HTML can negatively affect deliverability for cold outbound`. Everything HTML unlocks carries that same deliverability cost, which is why it is all off by default. For cold campaigns, replies are the more reliable signal to measure anyway.

| Available with Enable HTML on | What it adds |
| --- | --- |
| Message editor toolbar | Bold, italic, and underline, a font picker, bulleted and numbered lists, and a link inserter for hyperlinks and inline images. |
| Track email opens and Track link clicks | Open and click tracking. Each needs a link or an image in the message body, which is why HTML is the prerequisite. |
| Enable unsubscribe link | An unsubscribe link in the message, along with the Unsubscribe text that goes with it. |

Switching HTML back off is fine, but a message that already carries HTML-only formatting can't be rendered in the plaintext editor. Clay locks that message's body and says so on the card, pointing you back to the campaign settings to turn HTML on again if you want to see and edit it there.

## Personalizing with variables

Type `/` anywhere in a subject line or message body to open the insert menu — the editor prompts you with `Use / to insert variables or AI snippets`. Keep typing to search for a specific field, or pick one of the special options.

| Insert menu option | What it puts in your message |
| --- | --- |
| Any lead field, listed by name | A value from that lead's record in Audiences — first name, company, job title, and so on. Each row shows a sample value beside it so you can tell similar fields apart. |
| AI snippet | A piece of copy written per lead by AI, from a brief you write once. |
| Spintax | One value picked at random, per lead, from a short list of alternatives you supply. |
| Sender data | Opens a submenu of details drawn from whichever sending account the email goes out from. |
| Link | A hyperlink with its own display text. Appears only when Enable HTML is on. Both the URL and the Label accept lead fields and sender variables. |

### Lead variables

A lead variable is more than a raw field reference — click the token you inserted and you get a small panel of controls over how that value behaves.

| Control | What it does |
| --- | --- |
| Format variable | Normalizes casing on the way in: None, Title Case, Lower Case, Upper Case, or Sentence Case. Useful when your source data is inconsistently capitalized. |
| Sanitize variable | Removes emojis and special characters from the value — handy for names and company names carrying decorative punctuation. |
| Require variable data | Makes the field mandatory. A lead with nothing in it isn't enrolled until the data is there, which protects you from sending a message with a hole in it. |
| Fallback value | The text used when a lead has no value. Available once Require variable data is off, and required in that case, so a variable always resolves to something. |

Variables you insert start out required, with no fallback. That's the safe default, but it also means every variable you add narrows the pool of leads eligible to send. If a variable is nice-to-have rather than essential, switch `Require variable data` off and write a fallback that reads naturally in the sentence.

### Sender variables

Sender variables let campaign copy reference something that differs per sending account, like a meeting link or a signature. Insert one from the `Sender data` submenu, and the value resolves per lead based on which account that lead's email is sent from.

This is what lets a single sequence work across a whole pool of senders without reading as though it came from one person. They work inside a link too, in both the `URL` and the `Label`, so one shared campaign can give every rep their own booking link.

You manage the values on the `Sender variables` tab of the `Campaigns` page, and creating a variable walks you straight into filling them in:

1.  Give the variable a `Name` and a `Default value` in `New sender variable`, then choose `Create sender variable`. Clay confirms it with a `Sender variable created` toast.
2.  `Set values for each sender` opens next, with a field for every sending account. Fill in the accounts that need their own value, and leave the rest blank to use the variable's default. Past 100 accounts, the modal shows the first 100 and points you to the email accounts tab for the rest.
    -   With no sending accounts connected yet, Clay shows a `Sender variable created` confirmation instead, and you set the values later from the email accounts settings.
3.  Choose `Save values` to store them — a `Sender values saved` toast confirms the save — or `Skip` to leave every account on the default and come back to it later.

To change one account's values afterwards, use that account's `Update sender variables` option.

### Spintax

Spintax randomizes wording so that no two leads receive a byte-identical email — repetitive, high-volume copy is one of the patterns spam filters look for.

1.  Insert `Spintax` from the `/` menu. The `Spintax options` panel opens on the new token straight away.
2.  Fill in your alternatives — `Option 1`, `Option 2`, and so on, up to five. At least two are required, and the panel tells you so.
3.  Choose `Save`. Closing the panel with fewer than two values removes the token again, and clicking a saved token reopens the panel whenever you want to change the list.

Clay picks one of those alternatives at random for each lead. Spintax is a deliverability tool, not a measurement tool: Clay doesn't track which alternative a lead received, so if you want to know which of two phrasings performs better, run an [A/B test](https://university.clay.com/docs/ab-test-sequence-copy) instead.

## AI snippets

An AI snippet writes copy from a lead's data at enrollment. It can be one clause of one sentence, or the whole body of an email — whatever you point it at.

1.  Insert `AI snippet` from the `/` menu, and a panel opens for the `Snippet brief`.
2.  Describe what you want in plain language, the way the placeholder suggests: `Describe what this snippet should generate...`. Briefs work best when they're specific about the job, the length, and the tone.
3.  Point the brief at your data. The brief is itself a template, so `/` inside it references lead fields, and `@` references one of the documents attached under `AI context` — that's how you tell the AI which data to look at rather than hoping it finds the right thing.

Three buttons sit at the bottom of the panel:

-   `Update preview` — regenerates the snippet against the lead currently in preview, so you can read a real result before committing. It needs a lead selected in the preview to run.
-   `Discard` — throws the draft away and leaves your message as it was.
-   `Accept` — saves the brief and closes the panel.

Snippets are generated per lead at enrollment and then frozen, so what a lead receives is whatever the brief produced for them at that moment. Iterate on the brief while the campaign is still in draft, and preview across several leads rather than judging it on one.

## Giving the AI context

Snippets write better copy when they know what you're selling and why you're writing. That context lives in the `AI context` section of the left sidebar, and every snippet in the campaign inherits it automatically — you don't restate it per snippet.

Start with `Campaign goals`. Describe the offer, the audience, and what a good outcome looks like, in a few sentences. It accepts `/` for variables and `@` for documents, so you can make the goal itself lead-aware where that helps. Then attach reference material with `Add context`:

| Add context option | What it pulls in |
| --- | --- |
| Files | Documents uploaded to your workspace. |
| Google Docs | Available once a Google account is connected. |
| Notion | Available once a Notion account is connected. |
| Any skill under Skills, listed by name | One of your workspace's skills — a saved set of instructions the AI follows, so an approach you have already refined carries into a campaign without being written out again. |
| Create skill | Opens the skill editor, where you give the skill a Skill name, a Description, and its Instructions. It attaches to this campaign as soon as you create it. |

`Manage business context` sits at the bottom of the same popover, as a link out to where your workspace's business context is defined — shared facts about your company that every campaign can draw on.

Everything you attach shows up under `Documents and skills`, and you can remove any of it at any time. Fewer, sharper documents generally beat a large pile: a one-page positioning summary is easier for the AI to use well than a fifty-page deck.

## Checking your data before you send

Personalization is only as good as the data behind it, and the editor is built to show you that data rather than let you assume it.

### Preview

At the top of the sequence sits a `Preview` control with back and forward arrows. It renders your copy against a real lead from your segment, and the arrows step through leads one at a time. `Refresh` re-runs the AI snippets for the lead you're looking at, which is how you check that a brief holds up across different kinds of records rather than just the first one.

### Sample data

The `Sample data` panel shows the raw values behind your variables, on two tabs:

-   `Lead data` — the fields on your leads, each with a sample value.
-   `Sender data` — the details available from your sending accounts.

Search the panel, or narrow it with the filter:

-   `All datapoints` — everything available.
-   `Used in sequence` — only the fields your copy actually references.
-   `With coverage` — only the fields that have values in the sample.

### Lead setup

`Lead setup`, higher in the same sidebar, tells you how much of your list is genuinely ready. When fewer than 70% of leads have everything the sequence needs, Clay raises a warning telling you what share of the list is ready to send, and reminding you that leads missing required inputs won't be enrolled until their data is added.

Choose `Run diagnostic` in that warning and Clay breaks the shortfall down per required field, with a readout on each. Each field is its own coverage query, so the breakdown arrives when you ask for it rather than loading with the rest of the sidebar.

| Readout | What it means |
| --- | --- |
| None missing | Every sampled lead has a value. |
| Under 1% missing | A negligible gap. |
| A percentage | The share of leads without a value. |
| Couldn't check | The coverage query didn't come back; try again in a moment. |

When a field's coverage is thinner than you'd like, you have two good options:

-   Enrich the field upstream in Audiences so more leads have a value.
-   Open the variable in your copy, turn `Require variable data` off, and give it a `Fallback value` that reads naturally.

## Spam check and test sends

`Spam check` in the left sidebar grades your copy out of 100 and labels it `Looks good`, `Needs work`, or `High risk`. Expand it and you get the specific signals it found — flagged phrases, formatting patterns, and so on — each marked with how serious it is, so you know which one to look at first.

Treat the score as a first pass. Clay describes it plainly in the panel as a lightweight heuristic to catch common flags, not a guarantee of deliverability — a clean score is a good sign, not a promise about the inbox.

### Test sends

A test send is the only way to see the finished article: variables resolved, snippets generated, spintax picked, sender variables filled in, and formatting applied.

1.  Save your changes and select a lead in the preview — Clay needs both to build the message.
2.  Open a message's 3-dot `Message actions` menu and choose `Send test email`.
3.  Pick a sender under `Send from`, which lists the accounts this campaign sends from, put your own address in `Send to`, and choose `Send test email`.

If a test send fails, it's usually transient, so try once more; if it keeps failing, check that the sender account is still connected.
