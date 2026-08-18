---
title: Does Clay have an API?
description: Clay doesn't have a traditional API, but you can send data via
  webhooks, wrap Clay with Make or Zapier, use the Enterprise API for people &
  company lookups, connect AI tools via MCP, or build workflows via the CLI
  agent plugin.
last_synced: 2026-04-26T01:40:52.256Z
---

# Does Clay have an API?

Clay doesn't have a traditional API, but you can send data via webhooks, wrap Clay with Make or Zapier, use the Enterprise API for people & company lookups, or connect AI tools via MCP.

It's one of the most common questions we get — and the honest answer is: not in the traditional sense. Clay isn't built like a typical SaaS tool where you send a request to an endpoint and get data back in milliseconds. Instead, Clay is an enrichment and automation platform designed around tables, workflows, and integrations.

But that doesn't mean you're stuck. Depending on what you're trying to do, there are several ways to interact with Clay programmatically and get results that feel a lot like working with an API. You can pipe data into Clay automatically via webhooks, wrap Clay's functionality using tools like Make or Zapier, connect AI tools like Claude or ChatGPT directly to your Clay workspace via MCP, or — if you have beta access enabled — access Clay's native People and Company API directly.

**Don't confuse this with the HTTP API integration.** Clay's [HTTP API integration](https://university.clay.com/docs/http-api-integration-overview) is an enrichment column (or table source) that your Clay table uses to call **external** APIs — requests go from Clay out to another service. This page covers the opposite direction: calling **Clay** from your own systems — sending data in, searching Clay's data, or triggering Clay from code. If you want a Clay table to hit your CRM, data provider, or custom endpoint, use the HTTP API integration; if you want your app to talk to Clay, keep reading here.

Below, we'll walk through each approach, when to use it, and how to get started.

**Note:** If you purchase credits from us ("Clay Credits"), you agree not to sell or transfer your Clay Credits to any other user without our prior written approval. You also agree not to re-sell any data you obtain from Clay. [Learn more in our terms of service](https://www.clay.com/terms-of-service#:~:text=4.%20User%20Responsibilities).

### 1\. **Webhooks** (Best for sending data)

Every Clay table has a unique webhook endpoint. You can send data into a table programmatically—say from a form submission, CRM, or another app—and Clay will start processing it immediately.

After enrichments run, you can use Clay's native CRM actions (such as Salesforce's Update Record) or HTTP actions to push the data back out to your system of record. This is the most API-like workflow and is ideal for automating lead flow or enrichment jobs. [Click here for more information about webhooks in Clay!](https://www.clay.com/university/guide/webhook-integration-guide)

Webhook API Workflow in Clay

**Enriching Salesforce leads in real time**

A common use of this pattern is enriching new Salesforce leads or contacts automatically as they are created, without needing to manage Salesforce updates yourself:

1.  **In Clay:** Create a table using **Monitor webhook** as the source. Copy the webhook URL.
2.  **In Salesforce:** Set up a Record-Triggered Flow (`Setup → Flows → New Flow → Record-Triggered Flow`) that fires when a Lead or Contact is created. Add an **HTTP Callout** action that sends a POST request to your Clay webhook URL, with the relevant fields (Lead ID, name, email, company, etc.) as a JSON payload.
3.  **In Clay:** Add enrichment columns to process each incoming record.
4.  **In Clay:** Add an **Update record** Salesforce action column, mapping the enriched fields back to the Salesforce Lead or Contact using the ID from the webhook payload.
5.  **Enable auto-delete** on the webhook table so processed rows are deleted automatically after enrichment completes. This prevents the table from hitting the 50,000-row submission limit and lets it handle new leads continuously.

This is a simpler setup than calling the Clay API directly from Salesforce, because Clay handles the enrichment and writes the data back to Salesforce for you — no custom integration code required.

### 2\. **Wrap Clay in a third-party tool** (Best for light API proxying)

You can use tools like Replit or Make as a wrapper around Clay. These tools receive API requests, trigger Clay to do its thing, and return results once processing is complete.

This works if you absolutely need an endpoint, but be aware: Clay's enrichment model means responses might take a minute or more, and you'll need to build logic to handle that. [Click for a little tutorial on how to do that.](https://www.linkedin.com/posts/horacio-lopez_this-is-probably-the-only-enrichment-api-activity-7224062593689169923-cYg-/)

### 3\. **People & Company Search API** (Best for natural-language lookups)

Clay offers a fast API for searching its proprietary People and Company data. You submit a free-text, natural-language query (along with a `source_type` of `people`, `companies`, or `jobs`), and Clay's AI translates it into search filters and returns matching results.

**Note:** This API is currently in beta. Access is enabled per workspace on request — contact your GTM engineer or [our team](https://www.clay.com/contact-form) to have it enabled for your workspace.

-   It's useful for lightweight lookups and lead enrichment via natural-language search.
-   It doesn't include deep enrichment like emails, phone numbers, or revenue data.
-   **It returns enriched data to the caller — it does not write to Salesforce or any other CRM automatically.** Your system is responsible for taking the response and updating the CRM record. If you want Clay to handle the Salesforce write-back for you, use the webhook workflow described above instead.

[Contact our GTM engineers for more information.](https://www.clay.com/contact-form)

**Public HTTP API — Routines (open beta)**

Clay's Routines API lets you trigger enrichment functions programmatically — including contact enrichment workflows that find mobile phone numbers and personal email addresses. It is in open beta and available to all workspace members on any plan, with no per-workspace enablement required. This is the right approach when you want to run Clay enrichment from an external data pipeline (such as a Databricks notebook, a custom script, or any system-to-system integration) using your Clay workspace's credits:

-   `POST /routines/{routine_id}/run` — submit input records to a Clay function and start an enrichment run.
-   `GET /routines/run/{routine_run_id}/results` — poll for results once the run completes.

Authenticate by passing your workspace-scoped API key in the `clay-api-key` request header. Your workspace key is under **Settings → Account → API keys** and is distinct from the personal API key on your profile page.

**Note:** A 401 (`Authentication required`) from `api.clay.com/public/v0/routines` means your API key is invalid or does not belong to this workspace. Confirm you are using the workspace-scoped API key from **Settings → Account → API keys**, not the personal API key on your profile page. [Contact Clay support](https://www.clay.com/contact-form) if 401 persists after confirming your key.

**Note:** A `413` (`Payload Too Large`) from `POST /search/filters-mode/{search_id}/run` means the requested page of results exceeds the API's internal output cap. Reduce the `limit` parameter in your request and retry — the error is deterministic, so retrying at the same `limit` will always fail.

**Note:** Clay caps how many search results your workspace can return through the Public API, CLI, and MCP server per billing period. These quotas apply to Clay's People & Company Search API — they do not apply to in-app table enrichments or Routines API runs.

| Plan | Results per period | Period window |
| ---- | ------------------ | ------------- |
| Free | 100 | Monthly (resets on the 1st of each month, UTC) |
| Trial | 10,000 | 14 days from plan start |
| Paid | 1,000,000 | Annual (resets January 1 UTC) |
| Enterprise | 10,000,000 | Annual (resets January 1 UTC) |

When you exceed the period limit, Clay returns `400` with a message naming the limit and when it resets — for example: `"This request would exceed your workspace's annual limit of 1,000,000 results. You have already requested X results during the current period, which resets on January 1, [year] (UTC). Contact support to raise this limit."` There is no in-product usage meter for this quota — your workspace will not receive a warning before hitting it. If you need a higher limit, [contact Clay support](https://www.clay.com/contact-form).

**Note:** Credits consumed by Routines API runs appear in the **Workbooks** tab of the credit usage dashboard — not the **API** tab. Each run processes records in the function's table, and those credits are attributed to that table, the same as any other table enrichment. To see this credit spend, go to `Settings → Usage → Workbooks` and find the table associated with your routine. The **API** tab in the credit usage dashboard covers only direct People & Company Search API and Exportly calls — not Routines API enrichments.

**Note:** If you're using Clay as an API, **Auto-delete** helps keep things fast and lightweight. It automatically enriches incoming webhook data, sends results to your destination (like Salesforce or Google Sheets), then deletes the rows—so Clay streams data through rather than storing it. Perfect for high-volume or continuous enrichment jobs. [Learn more](https://www.clay.com/university/guide/auto-delete).

### 4\. **MCP / AI tool integration** (Best for AI assistants and agent workflows)

If you're using an AI tool like Claude or ChatGPT and want it to run Clay enrichments on your behalf, Clay supports MCP (Model Context Protocol). MCP lets AI assistants look up contacts, enrich data, and invoke custom Clay Functions — without anyone opening Clay directly.

Clay offers pre-built MCP connectors within each supported platform's app or connector directory (Claude, ChatGPT, Copilot, Gemini, Grok, Cursor). See the [MCP settings guide](https://university.clay.com/docs/mcp-settings) for the full list of supported platforms and setup instructions.

**Note:** Clay's MCP endpoint also supports Dynamic Client Registration (DCR), which lets third-party MCP clients not on the pre-built list connect to Clay's MCP server. Connections from unrecognized clients will appear as "Unknown" in OAuth. If you'd like to connect Clay through a third-party agent framework or MCP client via DCR, reach out to [Clay support](https://www.clay.com/contact-form) for the DCR setup guide.

### 5\. **CLI agent plugin** (Best for building workflows from a coding agent)

The Clay CLI is part of the Clay Agent Plugin — a developer tool that lets coding agents (Claude Code, Codex, or any terminal environment) build and run Clay workflows without opening the Clay UI. Install it from the [agent-plugins repository](https://github.com/clay-run/agent-plugins) and follow the setup instructions there.

**System requirements:** The Clay CLI runs on **macOS and Linux only**. Windows is not currently supported — if you're on Windows you'll see an error like "no native windows binary in the plugin." There is no workaround at this time; Windows support is not yet available.

When you run `clay routines list` or `clay routines get`, each function-type routine in the response includes a `source` field and a `createdBy` field. `source` is `"managed"` for Clay-built default functions and `"custom"` for functions built in your workspace. `createdBy` is an object with `id`, `name`, and `email` for custom functions, and `null` for managed defaults. Both fields are omitted for workflow-type routines.

**Note: `clay routines runs get --wait` terminates on `processing_failed`.** When polling a bulk routine run with `clay routines runs get --wait`, the command stops as soon as the run reaches any terminal status: `complete`, `validation_failed`, or `processing_failed`. `processing_failed` means the run failed after input validation passed — for example, an unexpected error occurred while processing the uploaded file — and retrying the same file may succeed. `clay routines runs list` also includes `processing_failed` as a valid `status` value alongside `in_progress`, `complete`, and `validation_failed`.

**Note: `clay functions list` and `clay functions get` give direct access to function schemas.** `clay functions list` lists all functions in your workspace (both Clay-managed and custom). `clay functions get <functionId>` returns a single function's full context: `id`, `name`, `description`, `source` (`"managed"` or `"custom"`), a prose `schema` description of the function's table written for a model to read, and JSON Schema objects for `inputSchema` and `outputSchema`. Both schema fields are always present — a function with no declared inputs or outputs returns an empty `properties` object, not a missing field. Both commands accept either a raw table id (e.g. `tbl_abc123`) or the `function:<tableId>` form, and require the `cli:all` scope on your API key. Common errors: `not_found` (exit 6) if no function with that id exists in the workspace; `auth_forbidden` (exit 3) if the key lacks the required scope.

**Note: Six `clay tables` read commands require an Enterprise plan.** The commands `clay tables list`, `clay tables get`, `clay tables rows list`, `clay tables rows get`, `clay tables columns list`, and `clay tables columns get` all require the public observability API — available on Enterprise plans only. On non-Enterprise workspaces, these commands exit with `auth_forbidden` (exit code 3) and the message: "The public observability API is not enabled for this workspace (available on Enterprise plans)." Routines, searches, and workflows via the CLI continue to work on non-Enterprise plans — only those six table read commands require Enterprise. If you only need a table's ID and are on a non-Enterprise plan, find it in the table's URL: it is the segment after `/tables/` (for example, `t_0te5b6rGsW6WAJW22cD` in `app.clay.com/workspaces/.../tables/t_0te5b6rGsW6WAJW22cD/views/...`). To read table structure or row data programmatically using these commands, an Enterprise plan is required.

**Note: `clay tables query-live` is an experimental command available without an Enterprise plan.** It queries a table's live Postgres data directly using ClayQL (no natural-language step), complementing `clay tables query` (which runs against the synced ClickHouse store and requires Enterprise). Results are capped at 100 rows; use `LIMIT n OFFSET m` in your query to page through more. To access it, set `CLAY_CLI_CHANNEL=experimental` before running the command. Available to workspace Admins, Members, and Viewers — not SalesRep-role users.

**Note: The `clay tables` commands and v0 REST API do not support writing data.** The CLI's `clay tables` surface includes commands for listing, getting, and querying tables and rows (`clay tables list`, `clay tables get`, `clay tables rows list`, `clay tables rows get`, `clay tables query`, and `clay tables query-live` [experimental]). Adding rows, updating cells, or deleting records is not available through the public developer platform — neither via the CLI nor the v0 REST API. The `clay tables update` command can toggle a table's query-sync configuration (`--query-enabled`), but does not write row data.

**Note: When using `group_by` in a tables query, every `select` column that is not the grouping key must use an aggregate function.** The `group_by` field accepts an array of up to 5 column-name strings. Grouping collapses many rows into one row per distinct group value, so every other column in `select` must resolve to a single value per group — either via `count`, `sum`, `avg`, `min`, or `max`. A plain column that is neither the group key nor an aggregate is ambiguous across the rows in a group: ClickHouse rejects the query at runtime and returns a 500 with the message `"Failed to execute table query"`. Clay does not return a structured validation error for this — the response looks the same as an unexpected server error. To get a row count per group, use: `"select": [{"field": "Column Name"}, {"fn": "count", "field": "*", "as": "row_count"}], "group_by": ["Column Name"]`. If you want the raw per-row values without a rollup, omit `group_by` entirely — that is why the query works without it. This behavior applies to both the REST API (`POST /public/v0/tables/query`) and the CLI (`clay tables query`).

**Note: Three `clay audiences records` commands let you read Audiences data from the CLI.** All three are available in the stable channel and require Audiences to be enabled for the workspace (available on Growth and Enterprise plans — see [Audiences](https://university.clay.com/docs/audiences)):

-   `clay audiences records get --entity-type <people|companies|deals> --ids <ids>` — bulk-fetch up to 100 records by id, returning each record's field values. `records get` is the only command that accepts `--entity-type deals`.
-   `clay audiences records search-ids --entity-type <people|companies> [--audience-id <id> | --filter <file>] [--cursor <cursor>]` — return matching record ids, cursor-paginated at 50 per page. Pass `--audience-id` to scope to a saved audience, `--filter` to apply an ad-hoc filter AST, or omit both to iterate all records of that entity type. Feed the returned ids to `clay audiences records get` in batches of 100 to retrieve field values.
-   `clay audiences records search-count --entity-type <people|companies> [--audience-id <id> | --filter <file>]` — return the count of records matching a scope without paging through ids.

All three return `auth_forbidden` (exit 3) if Audiences is not enabled for the workspace. `records get` additionally returns `rate_limited` (exit 4) if the workspace exceeds its hourly record budget or per-minute request rate — back off for `details.retryAfter` seconds before retrying.
