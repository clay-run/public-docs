---
title: MCP settings
source_url: https://university.clay.com/docs/mcp-settings
description: Connect your Clay workspace to AI tools.
last_synced: 2026-04-26T01:40:20.821Z
---

# MCP settings

Connect your Clay workspace to AI tools.

MCP (Model Context Protocol) is how Clay connects your workspace to AI tools like ChatGPT, Claude, Glean, and xAI. Clay lets workspace admins set credit limits and monitor usage for team members who access Clay through these platforms.

Clay's MCP integrations are pre-built apps within each supported platform's native connector or app directory — not a generic server URL you configure manually.

Navigate to it from the Clay homepage by clicking `MCP` in the side nav. The MCP settings page is only visible to workspace admins — if you don't see it in your settings sidebar, ask your workspace admin.

**Note:**  

Credit controls and usage monitoring are available on all modern paid plans (Launch, Growth, Enterprise) and Legacy Enterprise.  

Audiences controls are available to Enterprise customers enrolled in the Audiences Open Beta.  

The `Enable for MCP` option on Functions is available on modern Launch, Growth, Enterprise, and Legacy Enterprise plans.

## **Enabling a function for MCP**

Functions are reusable enrichment workflows built in Clay that reps can invoke directly from ChatGPT, Claude, Glean, or xAI with a single prompt. Admins build them once and enable them for MCP — reps never need to open Clay to use them.

1.  Go to the `Functions` tab in your workspace and find the function you want (or click `+ New function` to create a new one.)
2.  Click the function to open it's settings and toggle `Enable for MCP`.
    -   Set a name and description for the MCP app — this is what reps see when browsing available functions, so make it actionable (e.g., _"Company enrichment waterfall"_ or _"Outbound email generator"_).

_For more information about functions, check out our_ [_full doc_](https://university.clay.com/docs/functions)_._

## Setting credit limits

Credit limits cap how many Clay credits a rep can spend through ChatGPT, Claude, Glean, or xAI in a given month. Credit spend resets on the 1st of each month at midnight UTC.

There are two levels of control:

-   **Default credit limit** — applies automatically to all new MCP users when they first connect ChatGPT, Claude, Glean, or xAI. Click `Set default limit` to configure. Reps without an individual override inherit this limit.
-   **Per-user override** — find the rep in the user table and click the pencil icon next to their `Credit limit` to set an individual amount. Their current usage tracks against this limit in real time (e.g., `0 / 1,000`). Reps showing `No limit` have no cap applied.

## Monitoring usage

The `MCP users` table gives a live view of every rep who has connected Clay to an external platform:

-   **Name** — rep's name and email address
-   **Platforms** — icons indicating which platforms the rep has connected (ChatGPT, Claude, Glean, xAI, or a combination)
-   **Credit limit** — the rep's current limit, either the workspace default or a per-user override
-   **Credits used** — live usage tracked against the rep's limit
-   **Salesforce ID _(Enterprise Beta users only)_** — populated automatically when `Sync user IDs from audiences` is enabled; shows  otherwise

Use the search bar at the top of the table to find a specific rep by name or email.

MCP credit usage also appears in the **MCP** tab of the credit usage dashboard at `Settings → Credit Usage`. The tab breaks spend down by user and function — expand any user row to see which functions they invoked.

## Audiences controls

**Note: This feature is in beta for Enterprise Plan.**

If your workspace uses Clay Audiences, two additional workspace-level toggles appear on the `MCP users` page:

-   **Sync user IDs from audiences** — continuously syncs audience data to match MCP users to the Salesforce accounts they own. Updates run incrementally every 15 minutes, with a full sync once a week.
-   **Allow querying all accounts** — when enabled, reps can query any account in the synced audience, not just accounts they own in Salesforce.

**Troubleshooting — error: "Contact queries are not available in this workspace":** If a rep using Clay through Claude or ChatGPT sees the error `Contact queries are not available in this workspace. Contact ownership scoping is not yet supported — enable "Allow querying all accounts" in workspace settings to use contact queries`, the **Allow querying all accounts** toggle is off. Click `MCP` in the workspace sidebar and enable it. The MCP page is only visible to workspace admins — if you don't see it in the sidebar, ask your workspace admin to make the change.

**Troubleshooting — rep sees no results when querying Audiences:** When `Allow querying all accounts` is off, results are scoped to accounts the rep owns in Salesforce. A rep who owns no accounts (or whose Salesforce ownership hasn't synced yet) will receive empty results — which can look like the feature isn't working. To resolve: either enable `Allow querying all accounts` so the rep can see all workspace accounts, or ensure `Sync user IDs from audiences` is on and the rep's Salesforce account ownership is correctly mapped.

## FAQ

### Why does Clay MCP return different results than my Clay table?

The native Clay MCP contact enrichment — including the "Find and Enrich list of contacts" tool — runs a preset set of enrichment steps. It does not run the multi-provider waterfall you may have set up in your Clay tables. As a result, contacts that are only findable via a specific waterfall provider may return an email in your Clay table but not through MCP.

**To bring your waterfall coverage into MCP**, wrap the waterfall in a Clay Function and enable it for MCP. See [Enabling a function for MCP](#enabling-a-function-for-mcp) above for step-by-step instructions. Once enabled, you and your reps can invoke the waterfall function directly from Claude, ChatGPT, Glean, or xAI.

The `Enable for MCP` option requires a modern Launch, Growth, Enterprise, or Legacy Enterprise plan.

### Does Clay provide an MCP server URL I can paste into any AI tool?

No. Clay's MCP integrations are pre-built apps within each supported platform's native connector or app directory. Connect through:

-   **Claude:** [claude.com/connectors/clay](https://claude.com/connectors/clay)
-   **ChatGPT:** Type `@Clay` (browser) or `/Clay` (desktop) in a prompt
-   **Glean:** Your Glean admin connects Clay through Glean's MCP Apps directory
-   **xAI (Grok):** Connect Clay from within [grok.com](https://grok.com) through Grok's MCP integrations

There is no generic Clay MCP server URL to enter manually. The "Add MCP server" configuration screen in tools like Glean is for custom third-party servers — Clay's integration connects through Glean's built-in app directory, not that form.

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

**Important:** Team members must accept their workspace invite email *before* connecting Clay to Claude, ChatGPT, Glean, or xAI. If a rep goes through the Clay MCP connection flow before accepting the invite, they'll be routed into a new personal workspace instead of your team workspace — and they won't appear in your `MCP users` table or be eligible for credit allocation.

If this happens: have the rep disconnect Clay in their AI tool (remove and re-add the connector), then during re-authorization select your team workspace instead of "Personal Workspace." If invite links have expired, remove the user from `Settings → Team` and resend the invite before they reconnect.

**Note:** The Sales Rep role is currently in beta — contact support to request access for your workspace.

For a full breakdown of all roles, see [Roles and permissions](https://university.clay.com/docs/roles-and-permissions).

### How do I disconnect Clay from an AI tool?

Clay doesn't manage the MCP connection from its side — each AI platform controls its own connector integrations. To disconnect Clay, go to that platform's settings and remove the Clay connector:

-   **ChatGPT:** Open ChatGPT **Settings → Connectors**, find Clay, and remove it.
-   **Claude:** Go to [claude.com/connectors](https://claude.com/connectors/clay) and remove the Clay connector.
-   **xAI (Grok):** In grok.com settings, find MCP integrations or connected apps and remove Clay.
-   **Other tools:** Find connected apps, MCP integrations, or connectors in that tool's settings and remove Clay from there.

Your Clay workspace data and workflows are unaffected — only the connection from that AI tool is removed.

### Can admins remove a rep's access to Clay in ChatGPT or Claude?

Yes, by removing them from your workspace. While admins cannot directly revoke a rep's MCP connection from the `MCP users` page, they can remove the rep from the workspace entirely. If a rep is not added to your workspace, they won't have access to the data and workflows in your Clay instance. Alternatively, to limit usage without removing access, set their credit limit to a low value.

### When do credits reset?

Credit spend resets on the 1st of each month at midnight UTC.

### What happens when a rep hits their credit limit?

Further actions through ChatGPT, Claude, Glean, or xAI are hard-blocked until the monthly reset — the rep won't be able to run enrichments or invoke Functions. Admins can increase the per-user limit at any time from the `MCP users` table to restore access immediately.

### Where else can I see MCP credit usage?

MCP usage appears in the **MCP** tab of the credit usage dashboard at `Settings → Credit Usage`. The tab shows spend broken down by user and function — expand any user row to see which functions they invoked and how many credits each consumed.

### What's the difference between the default credit limit and a per-user override?

The default limit is a workspace-wide setting that applies automatically to any new rep who connects ChatGPT, Claude, Glean, or xAI. A per-user override replaces the default for a specific rep. Reps showing `No limit` have neither a default nor an override applied.
