---
title: IP access restriction
description: Restrict which IP addresses can reach your Enterprise workspace — configure separate allowlists for browser sessions and API keys, webhooks, and MCP requests.
last_synced: 2026-09-22T19:00:00.000Z
---

# IP access restriction

IP access restriction lets Enterprise workspace admins control which IP addresses are allowed to connect to their workspace. Browser sessions and API requests (API keys, webhooks, and MCP) are controlled independently, so you can lock down programmatic access without affecting your team's browser workflows — or restrict both at once.

IP access restriction is available on **Enterprise plans** and is visible only to workspace admins.

## Navigating to the setting

1. Go to `Settings` > `Workspace settings`.
2. Scroll to the **Security** section.
3. Find the **IP access restrictions** card.

## Adding an allowlist

Before you can enable restrictions for a category, add at least one allowlist that contains your allowed IP addresses or CIDR ranges.

1. In the **IP access restrictions** card, click **Add allowlist**.
2. Give the allowlist a name (up to 100 characters) — for example, "Corporate office" or "VPN range".
3. Choose whether this allowlist applies to **Web app** (browser sessions) or **API** (API keys, webhooks, and integrations).
4. Enter your allowed IP addresses or CIDR ranges, one per line or separated by commas. Both IPv4 and IPv6 are supported, and both plain addresses and CIDR notation are valid. You can include up to 50 entries per allowlist.
5. Click **Save**.

You can create multiple allowlists for the same category — their entries are merged into a single effective allowlist for that category.

## Enabling restrictions

After adding at least one allowlist for a category, use the toggle next to **Web app** or **API** to turn on restrictions for that category.

- **Web app** — restricts browser sign-in and table access. Only the IP addresses in your Web app allowlists can open Clay in a browser.
- **API** — restricts API key access, webhook calls, and MCP requests. Only the IP addresses in your API allowlists can reach Clay via API key, OAuth token, or MCP client.

Before a toggle takes effect, Clay checks whether your current IP address is included in the allowlist for that category. If enabling the restriction would lock you out, Clay shows a warning with your current IP address and does not apply the change — add your current IP to an allowlist first, then enable the restriction.

**Note:** Changes can take up to 10 minutes to fully propagate across all requests.

## What members see when blocked

When a workspace member tries to connect from an IP address that is not on the allowlist, they see an **Access restricted** screen:

> You are not allowed to connect to this workspace from your current IP address. Please connect to your VPN or corporate network and try again, or contact a workspace admin if you believe this is a mistake.

Members can switch to another workspace they belong to from this screen, or sign out and reconnect from an allowed network.

## Disabling restrictions

Toggle the switch next to **Web app** or **API** off to remove restrictions for that category. Existing allowlists are preserved — re-enabling the toggle re-applies the same allowlists.

Deleting all allowlists for a category automatically disables restrictions for that category.

## Notes

- **Clay support sessions are not affected.** Clay support agents can access your workspace regardless of your allowlist configuration.
- **Each category is independent.** Enabling Web app restrictions does not change API access, and vice versa.
- **IPv4 and IPv6 are both supported.** Allowlists accept plain IP addresses and CIDR ranges in either format.
- **Changes propagate within 10 minutes.** After saving a new allowlist or toggling a restriction, allow up to 10 minutes for the change to take effect across all requests.
- **Admins only.** Only workspace admins see the IP access restrictions card in Workspace settings.
