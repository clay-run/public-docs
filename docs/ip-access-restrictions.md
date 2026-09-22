---
title: IP access restrictions
description: Restrict which IP addresses can reach your Clay workspace — control browser and API access separately using named allowlists.
last_synced: 2026-09-22T00:00:00.000Z
---

# IP access restrictions

IP access restrictions let Enterprise workspace admins limit which IP addresses can connect to their Clay workspace. Admins define named allowlists of IP addresses or CIDR ranges and can enforce them independently for browser sessions and for API keys, webhooks, and integrations.

**Available on Enterprise plans only.** Only workspace admins can configure IP access restrictions.

## Finding IP access restrictions

IP access restrictions are in the **Security** section of your workspace settings:

1.  Go to `Settings` → `Workspace settings`.
2.  Scroll down to the **Security** section.
3.  Find the **IP access restrictions** card.

The card shows two groups — **Web app** and **API** — each with its own toggle and list of allowlists.

## Understanding allowlists

An allowlist is a named set of IP addresses or CIDR ranges. Each allowlist applies to exactly one category:

-   **Web app** — covers browser sign-in and table access (session-based requests).
-   **API** — covers Clay API keys, OAuth tokens, webhooks, and MCP integrations.

To restrict both browser and API access, create a separate allowlist for each category. A workspace can have up to **50 allowlists in total** across both categories.

Each allowlist can contain up to **50 IP addresses or CIDR ranges**. Accepted formats: IPv4 addresses (e.g. `203.0.113.5`), IPv6 addresses, IPv4 CIDR ranges (e.g. `198.51.100.0/24`), and IPv6 CIDR ranges. Enter one address or range per line.

## Adding an allowlist

1.  In the **IP access restrictions** card, click **Add allowlist**.
2.  Enter an **Allowlist name** (for example, `NYC HQ` or `VPN range`).
3.  Enter IP addresses or CIDR ranges in the **IP addresses** field, one per line.
4.  Under **Applies to**, select **Web app** or **API**.
5.  Click **Add allowlist** to save.

The page shows your current IP address and offers a one-click button to add it to the list — use this to make sure you don't lock yourself out.

## Enabling restrictions

Adding an allowlist does not enforce restrictions automatically. Each category has a separate toggle:

-   **Web app** toggle — when on, only browser sessions from IPs in your web allowlists can access the workspace.
-   **API** toggle — when on, only API keys, webhooks, and integrations from IPs in your API allowlists can reach the workspace.

To turn on a restriction, click the toggle for that category. Clay will ask you to confirm before enabling — the confirmation dialog shows how many addresses will be allowed or that access will stay open if no allowlists exist.

**You cannot enable a toggle if the category has no allowlists.** Add at least one allowlist first.

**Lockout protection:** Clay checks whether your current IP is covered before saving any change. If a change would lock you out of the workspace, Clay blocks the save and shows an error with your current IP. This applies to toggling restrictions on, adding allowlists, and deleting allowlists.

## Editing and removing allowlists

To edit an allowlist, click its name or the edit icon in the allowlist row. To remove one, click the delete icon. Removing an allowlist that is the last one for a category automatically disables that category's restriction toggle.

## What blocked users see

When a user tries to access the workspace from an IP address that isn't on the allowlist, they see an **Access restricted** screen:

> You are not allowed to connect to this workspace from your current IP address. Please connect to your VPN or corporate network and try again, or contact a workspace admin if you believe this is a mistake.

The screen also shows any other workspaces the user belongs to, so they can switch to a workspace that isn't restricted. If the user has no other accessible workspaces, they can sign out from the same screen.

For API requests blocked by an IP restriction, Clay returns `HTTP 403` with error code `ip_not_allowed`.

## Propagation time

Changes to IP access restrictions can take **up to 10 minutes** to take effect across all requests. Expect a brief window where the new rules are not yet fully applied.

## Clay support access

Clay support sessions are not affected by IP access restrictions. If Clay support needs to troubleshoot your workspace, they can access it regardless of which IP rules are in place.
