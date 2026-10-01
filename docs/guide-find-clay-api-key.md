---
title: Find your Clay API key
description: Create a Clay API key via the API and CLI page or the Clay CLI to enable Clay-native integrations.
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

You can create an API key two ways:

-   With Clay's Agent Plugin installed, ask your coding agent to create one for you — or run `clay api-keys create --name "<key name>"` yourself using the Clay CLI.
-   In Clay, open `API and CLI` in the left sidebar (under `Orchestration`), select the `API keys` tab, and click `Add API key`.

The key is shown only once when you create it — copy it somewhere safe.

**Note:** Some older integrations, such as Zapier, still use the legacy single-token key. To find it, go to `Settings` → `Account` → `API key (legacy)`.

### Can't find "API keys (beta)" in Settings → Account?

The **API keys (beta)** tab that used to appear in `Settings` → `Account` has been retired. Clay API keys — including the workspace-scoped keys used with the Public HTTP API — are now created and managed on the **API and CLI** page, which lives in the main app's left sidebar rather than in Settings. If you open an old link to the API keys (beta) tab (one ending in `accountTab=api-keys-beta`), you'll see an empty page instead of your keys.

The API and CLI page is available to all workspaces. You don't need to join the Beta Program or request access to see it. Workspace Admins, Members, and Viewers can create API keys there; users with the Sales Rep role can't.

To find or create your API keys:

1.  Leave Settings and return to the main Clay app.
2.  In the left sidebar, under **Orchestration**, click **API and CLI**.
3.  Select the **API keys** tab. Your existing keys are listed here.
4.  To create a new key, click **Add API key**, enter a **Name**, choose the **Scopes** (which APIs the key can access), and click **Add API key**.

The **API key (legacy)** tab in `Settings` → `Account` is a separate personal key. It won't show keys you create on the API and CLI page.

### Using your API key with external tools

This personal API key is designed for use **within Clay** — specifically for Clay-native integrations such as cross-table lookups. It is not supported for use with external CLI tools, custom MCP clients, or direct REST API calls made from outside of Clay. If you attempt to use it in those contexts, you will receive an authentication error; this is expected behavior.

If you need programmatic access to Clay from an external tool or CLI, Clay offers a Public HTTP API (`api.clay.com`) that uses a separate workspace-scoped API key — this is distinct from the personal key described above. The Public HTTP API is in public beta and available on all plans. To get a workspace-scoped key, follow the setup instructions at [developers.clay.com](https://developers.clay.com) — the Clay agent plugin creates the key for you in one step, or open **API and CLI** in the left sidebar, select the **API keys** tab, and click **Add API key**.

**Note:** While the Public HTTP API is available on all plans, CLI table-inspection commands — `clay tables list`, `clay tables get`, `clay tables rows list`, and `clay tables rows get` — require an Enterprise plan. These commands use the public observability API; on non-Enterprise plans you receive the error: "The public observability API is not enabled for this workspace (available on Enterprise plans)." All other CLI features — running searches, running functions, and building or running workflows — are available on all plans. If you need a table ID without Enterprise access, find it in the table's URL: it is the segment after `/tables/` (for example, `t_0te5b6rGsW6WAJW22cD` in `app.clay.com/workspaces/.../tables/t_0te5b6rGsW6WAJW22cD/views/...`).

**Naming note:** The Public HTTP API (calling *Clay* from your own code) is unrelated to the [HTTP API integration](https://university.clay.com/docs/http-api-integration-overview), which is an enrichment column your Clay table uses to call *external* APIs. Neither the personal API key nor the workspace-scoped Public API key is used in the HTTP API integration — there you supply the external service's own credentials. For an overview of all the ways to interact with Clay programmatically, see [Does Clay have an API?](https://university.clay.com/docs/using-clay-as-an-api)

### Search usage on the API and CLI page

The **Search usage** section on the API and CLI page shows how many search results your workspace has returned through the Public API, CLI, and MCP server in the current quota period. The label below the progress bar tells you which window applies to your workspace:

-   **Counts the last 30 days** — your workspace is on a rolling 30-day window. The quota does **not** reset annually; there is no single hard reset date. Instead, usage ages out daily — results older than 30 days drop off each day, freeing up that portion of your quota.
-   **Resets on [date]** — your workspace is on a fixed window (monthly, 14-day, or annual) that resets on that specific date.

For the full quota by plan — including how many results each plan allows per period — see [Does Clay have an API?](https://university.clay.com/docs/using-clay-as-an-api). If you need a higher limit, [contact Clay support](https://www.clay.com/contact-form).
