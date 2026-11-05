---
title: Get leads ready to sequence
description: How to prepare leads for campaign enrollment in Clay by building a People segment, ensuring email coverage, enriching data upstream, and configuring exclusions and cooldowns.
last_synced: 2026-09-01T03:27:07.441Z
---

# Get leads ready to sequence

Everything a lead needs before a campaign can enroll it — a People segment in Audiences, an email address, and the enrichment your sequence draws on.

A campaign in Clay doesn't build its own lead list. It draws on the people already in your Audiences, which means the work that decides how many leads reach a send happens upstream, before you open the `Sequence` tab.

**Note:** Leads have to exist in Audiences, with an email address, before a campaign can enroll them. Enrichment happens upstream — in Audiences, in a table, or in a workflow — not inside the campaign. A campaign reads the data that is already there and enrolls whoever is ready.

## What a campaign needs from you

Two things, and that is genuinely it:

-   **A segment of People in Audiences.** Campaigns enroll from contact segments, so build a People segment with the filters that describe who you want to reach.
-   **An email address on every lead you want to send to.** A lead with no usable email address is skipped at enrollment rather than blocking the rest.

### Point a campaign at a segment

Three routes get a segment onto a campaign:

-   **While you create it** — click `Campaigns` in the left sidebar, then `New campaign`, then `People`, and pick your segment from the list.
-   **Without a segment at first** — in that same `People` tab, click `Create blank campaign` and attach one later.
-   **From the other end** — open the segment in Audiences and choose `Export to campaign`.

### What `Lead setup` shows

Once a campaign has a segment, `Lead setup` at the top of the `Sequence` tab sidebar shows which segment it is and how many people are in it. When no segment is attached yet, you get `Add leads` instead.

The 3-dot menu there gives you:

-   `Open segment in new tab`
-   `Change segment`
-   `Lead email field` — by default a campaign sends to the contact's standard email field. If your leads carry more than one email field and you want a different one, choose from this menu; the standard column is listed with `(default)` after its name.

### Readiness warnings

Clay checks readiness as you build, so you can see the gaps before you launch rather than after. When fewer than 70% of eligible leads have every field the sequence needs, `Lead setup` shows an `Only X% of leads are ready to send` warning.

Expand it for a field-by-field readout, which reports one of:

-   `None missing`
-   `Under 1% missing`
-   The percentage that is short

## Enriching before you sequence

Fill the gaps before you enroll, not after. A lead's copy is generated from its Audiences data at the moment it is enrolled and then frozen, so an email address or a job title that lands tomorrow won't reach a lead that was already enrolled today.

Three places do this work well, and all of them write back to the same records a campaign reads:

-   **Audiences** — run enrichments straight onto a segment, and filter to the slice you actually want to spend on first.
-   **Tables and workflows** — build the list, enrich it, then send the results into Audiences. Workflows suit anything that should keep running on its own.
-   **Email waterfalls** — cascade across several email-finding providers in sequence, which is the most reliable way to lift email coverage on a list.

Full detail lives in the [Audiences](https://university.clay.com/docs/audiences) doc for segments and enrichment, the [Work Email waterfall](https://university.clay.com/docs/work-email-waterfall) doc for email coverage, and the [Workflows](https://university.clay.com/docs/workflows) doc for automating any of it.

## Two ways to enroll leads

A campaign gets its leads one of two ways, and you choose which when you create it.

|  | Attach a segment | Enroll from a workflow |
| --- | --- | --- |
| How leads arrive | Clay pulls from the attached segment on a repeating enrollment run | A workflow pushes one person at a time, when its own logic decides to |
| How you create it | New campaign then People, then pick a segment | New campaign then Workflow then Create workflow campaign |
| What Lead setup shows | The segment and its lead count | Enrolled by a workflow, plus a card listing the workflow nodes enrolling into it |
| Best for | A list you have already defined, sent at volume | Enrolling off the back of a signal, a form, or an enrichment result |

Pick deliberately, because this one can't be changed after the campaign is created. Everything else about a campaign — the segment, the copy, the settings — you can revisit.

### Attach a segment

This is the default, and the right choice for most campaigns. You attach a segment and Clay handles the pacing: while the campaign is `Active` it keeps checking the segment and enrolling the leads that are eligible, so people who newly qualify get picked up without you touching anything.

Eligibility is checked at each run rather than frozen at launch. A lead is enrolled when it:

-   Is in the segment
-   Is not already in this campaign
-   Is not excluded
-   Has every field the sequence needs

### Enroll from a workflow

Choose `Workflow` in the `New campaign` modal and Clay creates a campaign with no lead list attached — you write the sequence there, then point a workflow at it.

The `Enroll in campaign` node identifies each lead by an `Entity ID` from Audiences, which you map in from an earlier node's output. Any node upstream of it will do. The ID has to come from somewhere above the enroll node in the graph, but not necessarily from the node immediately above it.

1.  In the workflow, add a node that puts the person in Audiences — an `Upsert segment records` node or a `Search Audiences` node. This is also how the lead's campaign activity gets tracked back onto their record.
2.  Somewhere after it, add an `Enroll in campaign` node.
3.  Choose the campaign from the picker. The campaign has to be live, so publish it first — a node pointing at a draft campaign returns a message saying the campaign is not active rather than queuing the lead.
4.  Set the record to enroll, taken from that Audiences node's output.

**Note:** The `Entity ID` has to come from a node upstream of the `Enroll in campaign` node — a mapping that points anywhere else is rejected with `This input must reference an upstream node.` Upstream is the whole of the constraint, so the two nodes don't have to be adjacent. An enrichment, a conditional, or a delay can sit between the Audiences node and the enroll node without breaking the mapping.

The node reports its outcome back into the workflow, so you can branch on it. Re-running it for someone already in that campaign is safe: it reports them as already enrolled instead of enrolling them twice.

When it does decline a lead, the reason is specific:

-   The contact was missing data the campaign requires
-   The contact had no usable email address
-   The contact was enrolled in a related campaign too recently
-   The workspace was short on credits

On the campaign side, `Lead setup` reads `No lead list` until a node enrolls someone, then switches to `1 workflow node` or `N workflow nodes` and lists each node with the number of contacts it has enrolled and an info tooltip explaining what that count covers.

## Setting up exclusions before your first send

Exclusions are worth ten minutes before your first send, because they are the cheapest way to keep a campaign off the people who shouldn't hear from you. In `Lead setup`, the `Exclusions` row shows how many leads are currently being filtered out and by what — `Audiences, cooldown, blocked`. Click the pencil to open `Configure exclusions`.

The row appears once a segment is attached, so on a blank campaign you'll see `Add leads` first.

### Exclude by segment

Under `Exclude by segment`, use `Select a segment to exclude` to add a People segment whose members should never be enrolled. The usual candidates:

-   Do-not-contact lists
-   Existing customers
-   Accounts already in a live conversation

You can add more than one, and each row shows how many leads it removes on top of the ones above it, with a running total at the bottom of the modal.

Exclusions are editable while a campaign is `Draft` or `Paused` and become view-only once it is live, so set them before you launch. On a live campaign the pencil becomes an eye and the modal header reads `Exclusions` instead of `Configure exclusions`, so you can still check what is filtering without changing it.

### Add to the blocklist

If you don't have a segment for it — or the list is simply a pile of addresses someone sent you — the blocklist is faster. It works across every campaign in the workspace and is applied at the moment of enrollment.

1.  Go to `Campaigns` in the left sidebar, then the `Blocklist` tab.
2.  Click `Add to blocklist`.
3.  In `Add to global blocklist`, use `Manual` for a single `Email or domain`, or `Import CSV` for a list.
4.  For a CSV, put one email address or domain per line, up to 1,000 entries per import. `Download example CSV` gives you the shape.
5.  Once the file is read, Clay reports how many valid entries are ready to add. Duplicates are collapsed, and rows that aren't valid addresses or domains are listed as ones that will be skipped rather than failing the import. Go over 1,000 and the import is blocked with `Too many entries` until you remove the excess.
6.  Confirm with the add button, which names the number of entries it is about to add.

Blocking a domain covers everyone at it, which makes a short list of competitor and customer domains a good first pass.

## Cooldowns and cross-campaign rules

Within a single campaign, each lead is enrolled once and receives one sequence. If you want to reach the same person again, build a second campaign — and as a rule of thumb, leave a couple of months between attempts unless the offer is genuinely different.

### Set a cooldown window

Across campaigns, the spacing is yours to set. Where you set it depends on how the campaign enrolls:

-   **Segment campaigns** — open `Configure exclusions` from the `Exclusions` row in `Lead setup`.
-   **Workflow campaigns** — these have no `Exclusions` row, because there is no attached segment to filter. Instead, `Lead setup` carries its own `Cooldown` row, subtitled `Cooldown, blocked`, which opens `Configure cooldown`. Once the campaign is live the pencil becomes an eye labelled `View cooldown` and the header reads `Cooldown`.

Either way, choose a `Cooldown window`:

-   `None`
-   `30 days`
-   `60 days`
-   `90 days`
-   `Custom`, where `Custom cooldown window in days` takes anything up to 365

It is the number of days to wait before a lead can be sequenced again, and it is set per campaign — so a campaign with a 60-day window skips anyone enrolled elsewhere in the last 60 days.

### Choose which campaigns trigger a cooldown

Which campaigns count toward that window is controlled by `Trigger cooldowns`, on the `Settings` tab under `Enrollment`. It is on by default, meaning enrolling a lead in a campaign makes them ineligible for other campaigns during those campaigns' cooldown windows. Turn it off on a campaign whose enrollments shouldn't hold anyone back — a small internal test, say.

**Note:** A new campaign starts with `Cooldown window` set to `None`, so nothing stops the same person appearing in two campaigns at once until you set one. If you want a lead in only one campaign at a time, set a window on each campaign and leave `Trigger cooldowns` on across the board.

## FAQs

### What makes a field required, and why does a blank one stop a send?

Every field your sequence references becomes required for enrollment, and the lead's email field is required too. Clay generates each lead's copy once, at enrollment, so a variable with nothing behind it would go out as a hole in the email — skipping that lead instead is the safer outcome. A field counts as blank if it is empty or contains only whitespace.

Two details are easy to miss:

-   Fields that come from the lead's company are read from their primary account in Audiences, so a lead can be missing a required field without anything looking wrong on the person.
-   When a campaign is running an A/B test, readiness is judged against the union of the fields both variants reference, because a lead could be assigned to either one.

### How do I stop sending to someone mid-sequence?

Pause them. An enrolled lead can't be deleted, but pausing stops the remaining emails while keeping their history and analytics intact.

Some of that happens for you. `Pause lead on segment exit`, on the `Settings` tab under `Enrollment`, is on by default: when a lead drops out of the attached segment, Clay pauses them in the campaign. That makes editing your segment filters a practical way to pull a group out at once.

Adding an address to the blocklist stops future enrollments rather than stopping a sequence already in flight, so pause first and blocklist second if you want both.

### Can I sequence a segment of companies?

Not directly — campaigns enroll people, so a campaign reads from a People segment. That is also why `Export to campaign` appears on People segments and not on Companies ones, and why an exclusion segment has to be a People segment too.

Target accounts by working from the people at them instead. Build a People segment filtered on the company attributes you care about — industry, headcount, tech, a signal on the account — and the campaign follows your account list without ever leaving the person level.
