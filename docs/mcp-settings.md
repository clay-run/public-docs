---
title: MCP settings
description: Connect your Clay workspace to AI tools.
last_synced: 2026-04-26T01:40:20.821Z
---

# MCP settings

Connect your Clay workspace to AI tools.

MCP (Model Context Protocol) is how Clay connects your workspace to AI tools like ChatGPT, Claude, Codex, and Glean. Clay lets workspace admins set credit limits and monitor usage for team members who access Clay through these platforms.

Clay's MCP integrations are pre-built apps within each supported platform's native connector or app directory — not a generic server URL you configure manually.

Navigate to it from the Clay homepage by clicking `MCP` in the side nav. The MCP settings page is only visible to workspace admins — if you don't see it in your settings sidebar, ask your workspace admin.

**Note:**  

Credit controls and usage monitoring are available on all modern paid plans (Launch, Growth, Enterprise) and Legacy Enterprise.  

Audiences controls are available to workspaces with Clay Audiences enabled — contact support if you're unsure whether your workspace qualifies.  

The `Enable for MCP` option on Functions is available on modern Launch, Growth, Enterprise, and Legacy Enterprise plans.

Glean integration is available on Enterprise plans only.

## **Enabling a function for MCP**

Functions are reusable enrichment workflows built in Clay that reps can invoke directly from ChatGPT, Claude, or Glean with a single prompt. Admins build them once and enable them for MCP — reps never need to open Clay to use them.

1.  Go to the `Functions` tab in your workspace and find the function you want (or click `+ New function` to create a new one.)
2.  Click the function to open it's settings and toggle `Enable for MCP`.
    -   Set a name and description for the MCP app — this is what reps see when browsing available functions, so make it actionable (e.g., _"Company enrichment waterfall"_ or _"Outbound email generator"_).

_For more information about functions, check out our_ [_full doc_](https://university.clay.com/docs/functions)_._

## Setting credit limits

Credit limits cap how many Clay credits a rep can spend through ChatGPT, Claude, or Glean in a given month. Credit spend resets on the 1st of each month at midnight UTC.

There are two levels of control:

-   **Default credit limit** — applies automatically to all new MCP users when they first connect ChatGPT, Claude, or Glean. Click `Set default limit` to configure. Reps without an individual override inherit this limit.
-   **Per-user override** — find the rep in the user table and click the pencil icon next to their `Credit limit` to set an individual amount. Their current usage tracks against this limit in real time (e.g., `0 / 1,000`). Reps showing `No limit` have no cap applied.

## Monitoring usage

The `MCP users` table gives a live view of every rep who has connected Clay to an external platform:

-   **Name** — rep's name and email address
-   **Platforms** — icons indicating which platforms the rep has connected (ChatGPT, Claude, Glean, or a combination)
-   **Credit limit** — the rep's current limit, either the workspace default or a per-user override
-   **Credits used** — live usage tracked against the rep's limit
-   **Salesforce ID** — populated automatically when `Sync user IDs from audiences` is enabled; shows  otherwise

Use the search bar at the top of the table to find a specific rep by name or email.

MCP credit usage also appears in the main credit usage dashboard at `Settings → Credit Usage`, alongside all other workspace credit consumption.

## Audiences controls

If your workspace uses Clay Audiences, two additional workspace-level toggles appear on the `MCP users` page:

-   **Sync user IDs from audiences** — continuously syncs audience data to match MCP users to the Salesforce accounts they own. Updates run incrementally every 15 minutes, with a full sync once a week.
-   **Restrict account querying by Salesforce owner** — when enabled (the default when Salesforce is connected), reps can only query accounts they own in Salesforce. When disabled, reps can query any account in the synced audience.

**Troubleshooting — error: "Contact queries are not available in this workspace":** If a rep using Clay through Claude or ChatGPT sees the error `Contact queries are not available when account ownership restriction is enabled. Disable "Restrict account querying by Salesforce owner" in workspace MCP settings to use contact queries`, the **Restrict account querying by Salesforce owner** toggle is on. Click `MCP` in the workspace sidebar and disable it. The MCP page is only visible to workspace admins — if you don't see it in the sidebar, ask your workspace admin to make the change.

**Troubleshooting — rep sees no results when querying Audiences:** When `Restrict account querying by Salesforce owner` is on, results are scoped to accounts the rep owns in Salesforce. A rep who owns no accounts (or whose Salesforce ownership hasn't synced yet) will receive empty results — which can look like the feature isn't working. To resolve: either disable `Restrict account querying by Salesforce owner` so the rep can see all workspace accounts, or ensure `Sync user IDs from audiences` is on and the rep's Salesforce account ownership is correctly mapped.

## FAQ

### Why does Clay MCP return different results than my Clay table?

The native Clay MCP contact enrichment — including the "Find and Enrich list of contacts" tool — runs a preset set of enrichment steps. It does not run the multi-provider waterfall you may have set up in your Clay tables. As a result, contacts that are only findable via a specific waterfall provider may return an email in your Clay table but not through MCP.

**To bring your waterfall coverage into MCP**, wrap the waterfall in a Clay Function and enable it for MCP. See [Enabling a function for MCP](#enabling-a-function-for-mcp) above for step-by-step instructions. Once enabled, you and your reps can invoke the waterfall function directly from Claude or ChatGPT.

The `Enable for MCP` option requires a modern Launch, Growth, Enterprise, or Legacy Enterprise plan.

### Does Clay provide an MCP server URL I can paste into any AI tool?

No. Clay's MCP integrations are pre-built apps within each supported platform's native connector or app directory. Connect through:

-   **Claude:** [claude.com/connectors/clay](https://claude.com/connectors/clay)
-   **ChatGPT:** Type `@Clay` (browser) or `/Clay` (desktop) in a prompt
-   **Codex:** Add the `clay-run/agent-plugins` marketplace in Codex, then install the `clay` plugin
-   **Glean:** Your Glean admin connects Clay through Glean's MCP Apps directory (Enterprise plans only)

Each connector uses Clay's OAuth flow for authentication — when you click through to connect, you're redirected to log in to your Clay workspace to complete the authorization.

There is no generic Clay MCP server URL to enter manually. The "Add MCP server" configuration screen in tools like Glean is for custom third-party servers — Clay's integration connects through Glean's built-in app directory, not that form.

**Note on `mcp.clay.earth`:** You may encounter `mcp.clay.earth/mcp` while searching for Clay's MCP endpoint. That URL belongs to a separate, unaffiliated product — a personal CRM tool previously called Clay.earth, now rebranded to Mesh. It is not Clay's MCP server.

### Can I connect Clay's MCP server through a third-party MCP gateway or client?

Not currently. Clay's MCP OAuth flow only accepts redirect URIs from supported platforms. If you try to register a client via Dynamic Client Registration through a third-party MCP gateway, you will see this error:

```
redirect_uris.0: redirect_uri must be from an allowed domain
```

There is no self-service way to add a custom redirect URI to Clay's OAuth allowlist. If your organization needs to connect Clay through a specific third-party MCP client or gateway, reach out to Clay support with the redirect URI(s) you require. Adding a new platform requires a code change on Clay's side.

### What role should I assign to team members who will only use Clay through MCP?

Any team member who needs to use Clay through an AI tool (Claude, ChatGPT, Glean, or xAI) must first be added to your Clay workspace. When inviting them, assign the **Sales Rep** role.

The Sales Rep role restricts access to the main Clay workspace: users can invoke functions and run enrichments from within their AI tool, but they cannot open or interact with the Clay interface (tables, workbooks, etc.). This makes it the right choice for team members who should use Clay through AI tools only — not build workflows directly in Clay.

To invite them: go to `Settings` → `Team`, click `+ Invite`, enter their email address, and select **Sales Rep** from the role dropdown.

**Important:** Team members must accept their workspace invite email *before* connecting Clay to Claude, ChatGPT, or Glean. If a rep goes through the Clay MCP connection flow before accepting the invite, they'll be routed into a new personal workspace instead of your team workspace — and they won't appear in your `MCP users` table or be eligible for credit allocation.

If this happens: have the rep disconnect Clay in their AI tool (remove and re-add the connector), then during re-authorization select your team workspace instead of "Personal Workspace." If invite links have expired, remove the user from `Settings → Team` and resend the invite before they reconnect.

**Note:** The Sales Rep role is currently in beta — contact support to request access for your workspace.

For a full breakdown of all roles, see [Roles and permissions](https://university.clay.com/docs/roles-and-permissions).

### How do I disconnect Clay from an AI tool?

Clay doesn't manage the MCP connection from its side — each AI platform controls its own connector integrations. To disconnect Clay, go to that platform's settings and remove the Clay connector:

-   **ChatGPT:** Open ChatGPT **Settings → Connectors**, find Clay, and remove it.
-   **Claude:** Go to [claude.com/connectors](https://claude.com/connectors/clay) and remove the Clay connector.
-   **Codex or other tools:** Find connected apps, MCP integrations, or connectors in that tool's settings and remove Clay from there.

Your Clay workspace data and workflows are unaffected — only the connection from that AI tool is removed.

### Can admins remove a rep's access to Clay in ChatGPT or Claude?

Yes, by removing them from your workspace. While admins cannot directly revoke a rep's MCP connection from the `MCP users` page, they can remove the rep from the workspace entirely. If a rep is not added to your workspace, they won't have access to the data and workflows in your Clay instance. Alternatively, to limit usage without removing access, set their credit limit to a low value.

### When do credits reset?

Credit spend resets on the 1st of each month at midnight UTC.

### What happens when a rep hits their credit limit?

Further actions through ChatGPT, Claude, or Glean are hard-blocked until the monthly reset — the rep won't be able to run enrichments or invoke Functions. Admins can increase the per-user limit at any time from the `MCP users` table to restore access immediately.

### Where else can I see MCP credit usage?

MCP usage appears in the main credit usage dashboard at `Settings → Credit Usage`, which tracks all credit consumption across your workspace broken down by table, integration, and time period.

### What's the difference between the default credit limit and a per-user override?

The default limit is a workspace-wide setting that applies automatically to any new rep who connects ChatGPT, Claude, or Glean. A per-user override replaces the default for a specific rep. Reps showing `No limit` have neither a default nor an override applied.