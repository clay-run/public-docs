---
title: Find your Clay API key
description: Utilize your Clay-native enrichments with your personal key.
last_synced: 2026-04-26T01:40:06.072Z
---

# Find your Clay API key

Utilize your Clay-native enrichments with your personal key.

A Clay API key is required for all Clay-native integrations.

To get started, you'll need a Clay account and your API key.

Your Clay API key enables you to:

-   Look up a single row in another table
-   Look up multiple rows in another table

### Find your Clay API key

1.  In the top bar, click your account name and select `Settings`
2.  Under `Account`, locate `API key`. You'll find your API key here for integrations.

### Using your API key with external tools

This personal API key is designed for use **within Clay** — specifically for Clay-native integrations such as cross-table lookups. It is not supported for use with external CLI tools, custom MCP clients, or direct REST API calls made from outside of Clay. If you attempt to use it in those contexts, you will receive an authentication error; this is expected behavior.

If you need programmatic access to Clay from an external tool or CLI, Clay offers a Public HTTP API (`api.clay.com`) that uses a separate workspace-scoped API key — this is distinct from the personal key described above. The Public HTTP API is in public beta and available on all plans. To get a workspace-scoped key, follow the setup instructions at [developers.clay.com](https://developers.clay.com) — the Clay agent plugin creates the key for you in one step. If your account shows an **API keys (beta)** tab under **Settings → Your profile**, you can also create and manage workspace-scoped keys there directly. For details on how API calls affect your Action and credit usage, see [Actions & Data Credits](./actions-data-credits.md).

**Note:** While the Public HTTP API is available on all plans, CLI table-inspection commands — `clay tables list`, `clay tables get`, `clay tables rows list`, and `clay tables rows get` — require an Enterprise plan. These commands use the public observability API; on non-Enterprise plans you receive the error: "The public observability API is not enabled for this workspace (available on Enterprise plans)." All other CLI features — running searches, running functions, and building or running workflows — are available on all plans. If you need a table ID without Enterprise access, find it in the table's URL: it is the segment after `/tables/` (for example, `t_0te5b6rGsW6WAJW22cD` in `app.clay.com/workspaces/.../tables/t_0te5b6rGsW6WAJW22cD/views/...`).

**Naming note:** The Public HTTP API (calling *Clay* from your own code) is unrelated to the [HTTP API integration](https://university.clay.com/docs/http-api-integration-overview), which is an enrichment column your Clay table uses to call *external* APIs. Neither the personal API key nor the workspace-scoped Public API key is used in the HTTP API integration — there you supply the external service's own credentials. For an overview of all the ways to interact with Clay programmatically, see [Does Clay have an API?](https://university.clay.com/docs/using-clay-as-an-api)
