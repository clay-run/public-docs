---
title: Audiences for agents and the CLI
description: Use the clay audiences CLI commands to create and manage segments, read and filter records, and query activities and signal events — from the terminal or Clay's in-app agents.
last_synced: 2026-09-15T15:07:09.664Z
---

# Audiences for agents and the CLI

Read, segment, and manage your workspace's people, companies, and deals from the Clay CLI — and from the Clay agents that run it for you.

Audiences is the home for your workspace's own people, companies, and deals. The `clay audiences` command group brings those records to your terminal: you can create and edit segments, manage field definitions, count or read records, and read the activities and signal events attached to them — all without opening the Clay app.

**Note:** These commands need Audiences enabled for your workspace, plus the Clay Agent Plugin installed and signed in. Install and sign-in steps live in the plugin doc, linked below.

## Where these commands run

One command surface serves three places, so the behavior is the same wherever you drive it from:

-   **The Clay CLI** — you or your coding agent run `clay audiences` commands directly in a terminal.
-   **Sculptor** — Clay's in-app go-to-market co-pilot runs the same commands for you when you ask it about your records.
-   **The `Agent` surface in Clay** — runs the same commands while it reasons through a play and builds the workflow. It's rolling out gradually, so you may not see it in your workspace yet.

In Sculptor and the `Agent` surface there is nothing to type: they reach for these commands on their own and report back in plain language. The command reference below is still worth skimming, because it tells you what those agents can and cannot get to.

## Getting set up

1.  Install the Clay Agent Plugin and sign in, then confirm the CLI is working with `clay whoami`. For the full install and sign-in walkthrough, see [**Clay Agent Plugin (API & CLI)**](https://university.clay.com/docs/clay-api-cli).
2.  Check that Audiences is available to you by running `clay audiences records search-count --entity-type people`.
    -   An exit code of `3` on an audiences command usually means Audiences isn't enabled for the workspace. That's a workspace-configuration answer rather than something to retry.
3.  Read the field catalog once and save it — `clay audiences fields list --entity-type people` — then slice the saved copy rather than re-running the command.
    -   Field ids, not display names, are what filters and record payloads key on. A company's name field is `org_name`, for example, so never infer an id from what you see on screen.

## Managing segments

A segment is a named filter over one entity type. Nothing is copied into it: it selects records live, so its membership changes as the underlying records change.

-   `clay audiences list --entity-type people`: Lists the segments over one entity type, 50 per page. Pass the returned cursor back with `--cursor` for the next page.
-   `clay audiences get <audienceId>`: Returns one segment, including the filter that selects its records.
-   `clay audiences create --entity-type people --name "Missing emails" --filter ./filter.json`: Creates a segment from a filter. `--description` is optional.
-   `clay audiences update <audienceId> --name "…" --description "…" --filter ./filter.json`: Updates a segment. Only the flags you pass change; the rest are left alone.
-   `clay audiences archive <audienceId>`: Archives the segment. It's a soft delete, it's safe to repeat, and the records themselves are untouched.

A few things worth knowing before you write your first one:

-   `--entity-type` takes `people` or `companies` on these commands. Segments exist over people and companies only.
-   `--filter` accepts inline JSON, a path to a JSON file, or `-` for stdin. Reach for a file or stdin on anything non-trivial — inline JSON in a shell invites quoting mistakes.
-   Segments take the filter AST, not a DSL query. `--query` belongs to the `records` search commands; there's no `--query` on `create` or `update`.
-   `update` replaces the whole filter rather than merging into it, and a segment's entity type is fixed once it exists.
-   `clay audiences create --help` carries the full filter node and operator reference, so read it once instead of guessing at the shape.

## Managing fields

Field ids are scoped to an entity type, so every subcommand here takes `--entity-type`.

-   `clay audiences fields list --entity-type people`: Lists every field with its id, name, data type, field type, and whether it's hidden. Add `--include-system` for system fields, which are left out by default, or `--filter id=email` to narrow to specific ids.
-   `clay audiences fields create --entity-type people --name "Lead score" --data-type number`: Creates a field. `--data-type` accepts `text`, `number`, `email`, `url`, `date`, or `boolean`, and defaults to `text`.
-   `clay audiences fields update <fieldId> --entity-type people --hidden true`: Updates a field's name, description, data type, visibility, or sort order.
-   `clay audiences fields delete <fieldId> --entity-type people`: Deletes a field definition.
-   `clay audiences fields segments <fieldId> --entity-type people`: Lists the segments whose filter references that field.

Two habits save time here. Run `fields segments <fieldId>` before you change a field's data type or delete it, so you know which segments depend on it first. And read the `name` and `id` that `create` returns rather than assuming the name you passed — a name already in use comes back uniquified, as `Tier (2)`.

Default and system fields are more constrained: they reject `--name` and `--data-type` changes and can't be deleted. `--hidden`, `--order`, and `--description` still work on them.

## Reading records

-   `clay audiences records search-count --entity-type people`: Counts the records in a scope, server-side.
-   `clay audiences records search-ids --entity-type people`: Returns the matching record ids. `--limit` sets the page size, from 1 to 10,000, and defaults to 50.
-   `clay audiences records get --entity-type people --ids 1,2,3`: Returns field values for up to 100 ids per call, keyed by field id. Ids that don't resolve are left out rather than raising an error.

Both search commands take the same scope flags, and `--query`, `--audience-id`, and `--filter` are mutually exclusive:

-   No scope flag: every record of that entity type.
-   `--query <query>`: an Audiences DSL query, and the preferred way to search ad hoc. Its `from` root decides what gets searched, so leave `--entity-type` off — passing both is an error.
-   `--audience-id <id>`: the records in a saved segment.
-   `--filter <json|file|->`: a filter AST, the fallback for filtering without DSL. It matches exactly what a segment built from that filter would hold.

A DSL query reads close to plain language. Its root is `people`, `companies`, or `opportunities` for deals, and `search-count` also accepts `activities`:

`clay audiences records search-count --query 'count from people where email is_not_null'`

`clay audiences records search-ids --query 'select from opportunities where is_closed = false' --limit 10`

Run `clay audiences records search-ids --help` for the grammar, the operators, and what each root accepts.

Add `--archived` to either search command to look at archived records instead of live ones.

Start with `search-count` whenever you can. It answers "how many" in a single call, and a `NotEmpty` filter on a field turns it into a fill-rate check — which is the cheapest way to find out whether the data you need is already there before you spend anything enriching it.

### Ranking with a sorted search

Add `order by <field>` to a `select` query and Clay ranks the whole matching scope server-side, then hands back the top of it. Pair it with `--limit N` for a top-N and hydrate only those ids with `records get`, rather than paging through everything and sorting locally.

`clay audiences records search-ids --query 'select from opportunities where is_won = true order by amount desc' --limit 10`

Three things to know before you trust the order:

-   **Check the field's type first.** Number and currency fields rank by value, while text, email, and URL fields rank alphabetically — so a numeric-looking text field gives you `"10", "100", "2"`. `clay audiences fields list` reports each field's data type, so read it instead of inferring from the values.
-   **A sorted search never returns a cursor**, even when more records match, and passing `--cursor` alongside `order by` is rejected. Treat what comes back as the top of the ranking rather than the full match set, and run `search-count` on the same `from … where` clause when you want the real total.
-   **One field, on the records you're returning.** Multiple sort keys, ordering by a related record's field, and aggregates such as total won amount per account aren't supported, though you can still filter on related records.

Ascending is the default, and records missing the field come last in either direction.

### Size a read before you start it

Reads are metered, and the limits are worth knowing before you walk a large scope:

-   Each command has its own request budget, shared across the workspace. Most default to 60 calls per minute; `records get` gets 300. A `fields list` loop therefore can't starve `search-count`.
-   `records get` carries a second, hourly budget charged per record id it returns, defaulting to 100,000 records per hour. Batching doesn't reduce it, so a detail pass over a large scope costs roughly one call per 100 records no matter how you group them.
-   On a rate-limit rejection the CLI exits `4` and reports how long to wait in `details.retryAfter`. Read `details.limit` off the error rather than assuming a default, since a workspace can be raised above it.

When a full walk doesn't fit, narrowing the filter beats grinding through it. A shorter date window is usually the biggest win, followed by a single stage, owner, or segment.

## Working with deals

Deals — also called opportunities — are a third record type alongside people and companies, and they reach Clay through a CRM sync. They're read-only: there's no command to create, update, or delete one, so deal edits belong in your CRM.

`--entity-type deals` is accepted by all three `records` commands and by `fields list`. The segment commands and the other `fields` subcommands take `people` or `companies` only, and passing `deals` to those exits `2` with a `validation_error` — that's the expected answer, not a bug.

The modelling point that saves the most time: **ask deal questions with `--query` and root them at `opportunities`.** That's the DSL's name for deals, and it accepts filters and `order by` like any other root, so "the ten biggest won deals" is a single query. The older `--entity-type deals` path accepts no scope at all, so on its own it only answers whole-population questions like the total deal count.

Root the query at whatever you want back. `select from opportunities` returns deals, `select from companies where opportunities.exists(is_won = true)` returns the accounts those deals belong to, and a `people` root returns the contacts attached to them.

These deal field ids exist in every workspace, so you can filter on them without listing fields first:

-   `opportunity_name`: Deal name.
-   `stage`: Pipeline stage, as a string from your CRM.
-   `amount`: Deal value.
-   `close_date`: Close date — actual once the deal is closed, expected before that.
-   `opportunity_type`: Deal type, such as new business or renewal.
-   `is_closed`: Boolean, true once the deal reaches a terminal stage.
-   `is_won`: Boolean, true when that terminal stage was a win.

Clay also manages `created_at`, `updated_at`, and `origin_source_id`, which appear in the product as `Deal creation date`, `Deal last updated`, and `Deal source`. Anything beyond these is a CRM property mapped into your workspace, and `clay audiences fields list --entity-type deals` is how you discover those ids and their data types.

Build on `is_won` and `is_closed` rather than on `stage` where you can. Stage strings come straight from the CRM and vary between workspaces, while the two booleans are normalized.

**Note:** Two deal conditions in the same `And` group have to be satisfied by a single deal. An account with a small won deal and a separate large open one won't match "won and over 50,000" — that's two searches whose results you intersect yourself. Worth saying which reading you used when you report a number, because the difference changes it.

## Reading activities

An activity is a timestamped thing that happened to a record — an email sent, a call logged, a workflow run — carried into Audiences from whichever system it happened in. The `clay audiences activities` group reads those events for the records in a saved segment.

-   `clay audiences activities summary` returns counts for a segment, grouped by type and source. It's the quickest way to see whether there's anything worth reading before you pull it.
-   `clay audiences activities get` returns the activities themselves, a page at a time.

Both are scoped to a saved segment rather than to one record, and both take a time window that can reach back up to a year. You can narrow by activity type and by the system the activity came from — campaign and email events, calls, CRM activity, and workflow runs.

Run `clay audiences activities get --help` for the flags, the accepted values, and examples. The help output is generated from the CLI itself, so it stays correct as the commands change.

## Reading signal events

A signal event is one firing of a signal against one record. `clay audiences signals` reads those events.

-   `clay audiences signals summary` returns counts across a segment, grouped by signal.
-   `clay audiences signals get` returns the events themselves, with their data, a page at a time.

Unlike activities, signal events can be read for a **single person or company** as well as for a segment. Either way the lookback reaches up to a year.

One thing to get straight before you start: **`clay audiences signals` and `clay signals` are different command groups.** This one reads events — what fired, and against whom. `clay signals` manages the signal definitions themselves and whether they're running. If the question is "is this signal even on?", that's `clay signals`.

See `clay audiences signals get --help` for the flags, including which of them apply to a single record versus a segment.

## Current limitations

The command surface reads and segments Audiences; a few things sit outside it today.

-   **Writing a value onto a record isn't a CLI command.** That's the `upsert-audiences-record` workflow action's job, and it covers people and companies only.
-   **Activity reads are segment-scoped.** There's no way to pull one person's activity feed on its own — save a segment that selects them instead. Signal events are the exception: those can be read for a single record. Writing an activity isn't possible from the CLI either.
-   **There's no import command.** Records enter Audiences through the app or a sync.
-   **Counts follow the query's root.** Counting companies with a won deal tells you how many accounts qualify, not how many won deals exist — an account with three of them counts once. Count `from opportunities` when you want the deals themselves.
-   **Sorted searches can't be paged.** Ranking happens server-side and comes back bounded: you get the top N and no cursor, so there's no walking a sorted set page by page.
-   **Segments can't be built over deals.** Save the people or companies segment whose filter references deals instead; it stays live as those deals change, the same as any other segment.

## FAQs

### Does reading Audiences from the CLI cost credits?

No. Reading records, counting them, and listing fields or segments all query data your workspace already holds, so they're free and return immediately. Credits enter the picture only when you go on to enrich something — which is exactly why a fill-rate check with `search-count` is worth running first.

### Can I reach Audiences over MCP instead?

Not today — Audiences is CLI-only, and no MCP tool serves it. Reps who connect a chat app to Clay over MCP get people and company search plus any Functions your team has enabled, and admins can additionally let them query owned accounts and opportunity data from the CRM. See [**MCP in Clay**](https://university.clay.com/docs/mcp-settings) for how that access is configured.

### Do Clay's in-app agents really run the same commands?

Yes. All three surfaces load the same Audiences instructions from the Clay Agent Plugin, so a capability that lands in the CLI reaches Sculptor and the `Agent` surface with it. That's also why the limitations above apply everywhere rather than to the terminal alone.

### How do I copy a segment?

Pipe one segment's filter into a new one: `clay audiences get <audienceId> | jq .filter` returns an id-free filter that `clay audiences create --filter -` accepts on stdin. Give the copy its own `--name`, and remember the new segment needs the same `--entity-type` as the original.

### What happens to a segment if I delete a field its filter uses?

The delete rewrites those saved filters with the affected clauses removed, which changes what the segments match rather than breaking them. Run `clay audiences fields segments <fieldId> --entity-type people` first to see what's affected — an empty `data` array means nothing is.
