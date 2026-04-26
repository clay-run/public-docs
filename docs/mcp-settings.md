---
title: MCP settings
source_url: https://university.clay.com/docs/mcp-settings
---

# MCP settings

Connect your Clay workspace to AI tools.

## Overview

MCP (Model Context Protocol) is how Clay connects your workspace to AI tools like ChatGPT or Claude. Clay lets workspace admins set credit limits and monitor usage for team members who access Clay through ChatGPT or Claude.

Navigate to it from the Clay homepage by clicking `MCP` in the side nav.

**Note:**

Credit controls and usage monitoring are available on all modern paid plans (Launch, Growth, Enterprise) and Legacy Enterprise.

Audiences controls are available to Enterprise customers enrolled in the Audiences Open Beta.

The `Enable for MCP` option on Functions is available on modern Launch, Growth, Enterprise, and Legacy Enterprise plans. **Legacy PLG plans (Pro, Explorer, Starter) can connect to MCP but cannot expose custom Functions — the toggle will not appear regardless of admin role.**

## Enabling a function for MCP

Functions are reusable enrichment workflows built in Clay that reps can invoke directly from ChatGPT or Claude with a single prompt. Admins build them once and enable them for MCP — reps never need to open Clay to use them.

1. Go to the `Functions` tab in your workspace and find the function you want (or click `+ New function` to create a new one.)
2. Click the function to open its settings panel on the right side of the screen, then toggle `Enable for MCP`.
   * This toggle is **only visible to workspace admins**. Non-admin workspace members who open the same function will not see it.
   * If you don't see the toggle even as an admin, confirm your plan is modern Launch, Growth, or Enterprise (or Legacy Enterprise). See [Why can't I find the Enable for MCP toggle?](#why-cant-i-find-the-enable-for-mcp-toggle) below.
   * Set a name and description for the MCP app — this is what reps see when browsing available functions, so make it actionable (e.g., *"Company enrichment waterfall"* or *"Outbound email generator"*).

*For more information about functions, check out our [full doc](https://university.clay.com/docs/functions).*

## Setting credit limits

Credit limits cap how many Clay credits a rep can spend through ChatGPT or Claude in a given month. Credit spend resets on the 1st of each month at midnight UTC.

There are two levels of control:

* **Default credit limit** — applies automatically to all new MCP users when they first connect ChatGPT or Claude. Click `Set default limit` to configure. Reps without an individual override inherit this limit.
* **Per-user override** — find the rep in the user table and click the pencil icon next to their `Credit limit` to set an individual amount. Their current usage tracks against this limit in real time (e.g., `0 / 1,000`). Reps showing `No limit` have no cap applied.

## Monitoring usage

The `MCP users` table gives a live view of every rep who has connected Clay to an external platform:

* **Name** — rep's name and email address
* **Platforms** — icons indicating which platforms the rep has connected (ChatGPT, Claude, or both)
* **Credit limit** — the rep's current limit, either the workspace default or a per-user override
* **Credits used** — live usage tracked against the rep's limit
* **Salesforce ID *(Enterprise Beta users only)*** — populated automatically when `Sync user IDs from audiences` is enabled; shows — otherwise

Use the search bar at the top of the table to find a specific rep by name or email.

MCP credit usage also appears in the main credit usage dashboard at `Settings → Credit Usage`, alongside all other workspace credit consumption.

## Audiences controls

**Note: This feature is in beta for Enterprise Plan.**

If your workspace uses Clay Audiences, two additional workspace-level toggles appear on the `MCP users` page:

* **Sync user IDs from audiences** — continuously syncs audience data to match MCP users to the Salesforce accounts they own. Updates run incrementally every 15 minutes, with a full sync once a week.
* **Allow querying all accounts** — when enabled, reps can query any account in the synced audience, not just accounts they own in Salesforce.

## FAQ

### Why can't I find the Enable for MCP toggle?

There are two requirements for the toggle to appear:

1. **You must be a workspace admin.** The toggle is hidden from non-admin workspace members. If you own the function but aren't an admin, ask a workspace admin to enable it for you.
2. **Your plan must support it.** The `Enable for MCP` option on Functions is only available on modern Launch, Growth, and Enterprise plans, and Legacy Enterprise. Legacy PLG plans (Pro, Explorer, Starter) can connect to MCP in general — meaning reps can still use Clay's built-in find/enrich tools in Claude and ChatGPT — but they cannot expose **custom** Functions through MCP. To unlock that capability, upgrade to a modern plan.

If both conditions are met and you still don't see it, confirm you are opening the function from the `Functions` tab on your Clay homepage (not from within a table view).

### What are "subroutines"? I see that term in Claude or ChatGPT.

"Subroutine" is the internal API name Clay uses for Functions in its MCP tool schema. When Claude or ChatGPT lists the Clay tools available to you, custom Functions appear as tools named `run_subroutine` or `list_subroutines`. These map directly to the Clay Functions your ops team has enabled for MCP.

If you see a reference to a subroutine in Claude or ChatGPT, it is the same thing as a Clay Function — there is no separate concept. To see which Functions (subroutines) are available, type `@Clay What functions do you have?` in ChatGPT or ask Clay directly in Claude.

### Can admins remove a rep's access to Clay in ChatGPT or Claude?

Yes, by removing them from your workspace. While admins cannot directly revoke a rep's MCP connection from the `MCP users` page, they can remove the rep from the workspace entirely. If a rep is not added to your workspace, they won't have access to the data and workflows in your Clay instance. Alternatively, to limit usage without removing access, set their credit limit to a low value.

### When do credits reset?

Credit spend resets on the 1st of each month at midnight UTC.

### What happens when a rep hits their credit limit?

Further actions through ChatGPT or Claude are hard-blocked until the monthly reset — the rep won't be able to run enrichments or invoke Functions. Admins can increase the per-user limit at any time from the `MCP users` table to restore access immediately.

### Where else can I see MCP credit usage?

MCP usage appears in the main credit usage dashboard at `Settings → Credit Usage`, which tracks all credit consumption across your workspace broken down by table, integration, and time period.

### What's the difference between the default credit limit and a per-user override?

The default limit is a workspace-wide setting that applies automatically to any new rep who connects ChatGPT or Claude. A per-user override replaces the default for a specific rep. Reps showing `No limit` have neither a default nor an override applied.
