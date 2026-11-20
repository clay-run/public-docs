---
title: Find your Clay API key
description: Create a Clay API key via the API and CLI page or the Clay CLI, and learn how it differs from the legacy personal key in Settings → Account.
last_synced: 2026-04-26T01:40:06.072Z
---

# Find your Clay API key

Create a Clay API key to connect to Clay from outside the app — for example, to call Clay's Public HTTP API.

To get started, you'll need a Clay account.

You don't need a Clay API key for in-table features such as looking up a single row or multiple rows in another table, or writing to another table. Those columns run without an API key.

### Find your Clay API key

You can create an API key two ways:

-   With Clay's Agent Plugin installed, ask your coding agent to create one for you — or run `clay api-keys create --name "<key name>"` yourself using the Clay CLI.
-   In Clay, open `API and CLI` in the left sidebar (under `Orchestration`), select the `API keys` tab, and click `Add API key`.

The key is shown only once when you create it — copy it somewhere safe.

**Note:** Some older integrations, such as Zapier, still use the legacy single-token key. To find it, go to `Settings` → `Account` → `API key (legacy)`.

### Can't find "API keys (beta)" in Settings → Account?

The **API keys (beta)** tab that used to appear in `Settings` → `Account` has been retired. Clay API keys — including the workspace-scoped keys used with the Public HTTP API — are now created and managed on the **API and CLI** page, which lives in the main app's left sidebar rather than in Settings. If you open an old link to the API keys (beta) tab (one ending in `accountTab=api-keys-beta`), Clay opens the **Your details** tab of `Settings` → `Account` instead — your API keys aren't shown there. Go to the **API and CLI** page as described below to find them.

The API and CLI page is available to all workspaces. You don't need to join the Beta Program or request access to see it. Workspace Admins, Members, and Viewers can create API keys there; users with the Sales Rep role can't.

To find or create your API keys:

1.  Leave Settings and return to the main Clay app.
2.  In the left sidebar, under **Orchestration**, click **API and CLI**.
3.  Select the **API keys** tab. Your existing keys are listed here.
4.  To create a new key, click **Add API key**, enter a **Name**, choose the **Scopes** (which APIs the key can access), and click **Add API key**.

The **API key (legacy)** tab in `Settings` → `Account` is a separate personal key. It won't show keys you create on the API and CLI page.

### Using your API key with external tools

The **API key (legacy)** in `Settings` → `Account` → `API key (legacy)` is a personal single-token key used by some older integrations, such as Zapier, and early API automations. Clay's Public HTTP API doesn't accept the legacy key — if you use it there, you'll receive an authentication error; this is expected behavior. The legacy key also isn't used by in-table features such as looking up rows in another table.

**Sending data into a Clay table from Workato, Make, n8n, or another tool?** Use the table's webhook instead of an API key. Clay webhooks don't use an API key — only an optional `x-clay-webhook-auth` token. See [Connecting middleware tools](webhook-integration-guide.md#connecting-middleware-tools) for the steps.

If you need programmatic access to Clay from an external tool or CLI, Clay offers a Public HTTP API (`api.clay.com`) that uses a separate workspace-scoped API key — this is distinct from the personal key described above. The Public HTTP API is in public beta and available on all plans. To get a workspace-scoped key, follow the setup instructions at [developers.clay.com](https://developers.clay.com) — the Clay agent plugin creates the key for you in one step, or open **API and CLI** in the left sidebar, select the **API keys** tab, and click **Add API key**.

**Note:** CLI table-inspection commands — `clay tables list`, `clay tables get`, `clay tables rows list`, and `clay tables rows get` — require a paid or trial plan. These commands use the public observability API, which is available on all paid and trial plans but not on the Free plan; on Free workspaces you receive the error: "The public observability API is not enabled for this workspace (available on paid and trial plans)." All other CLI features — running searches, running functions, and building or running workflows — are not affected by this requirement. You can also find any table's ID in the table's URL: it is the segment after `/tables/` (for example, `t_0te5b6rGsW6WAJW22cD` in `app.clay.com/workspaces/.../tables/t_0te5b6rGsW6WAJW22cD/views/...`).

**Naming note:** The Public HTTP API (calling *Clay* from your own code) is unrelated to the [HTTP API integration](https://university.clay.com/docs/http-api-integration-overview), which is an enrichment column your Clay table uses to call *external* APIs. Neither the personal API key nor the workspace-scoped Public API key is used in the HTTP API integration — there you supply the external service's own credentials. For an overview of all the ways to interact with Clay programmatically, see [Does Clay have an API?](https://university.clay.com/docs/using-clay-as-an-api)

### Search usage on the API and CLI page

The **Search usage** section on the API and CLI page shows how many search results your workspace has returned through the Public API, CLI, and MCP server in the current quota period. The label below the progress bar tells you which window applies to your workspace:

-   **Counts the last 30 days** — your workspace is on a rolling 30-day window. The quota does **not** reset annually; there is no single hard reset date. Instead, usage ages out daily — results older than 30 days drop off each day, freeing up that portion of your quota.
-   **Resets on [date]** — your workspace is on a fixed window (monthly, 14-day, or annual) that resets on that specific date.

For the full quota by plan — including how many results each plan allows per period — see [Does Clay have an API?](https://university.clay.com/docs/using-clay-as-an-api). If you need a higher limit, [contact Clay support](https://www.clay.com/contact-form).
