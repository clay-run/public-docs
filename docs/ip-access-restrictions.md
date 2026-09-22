---
title: IP access restrictions
description: Restrict which IP addresses can reach your Enterprise workspace — configure separate allowlists for browser sessions and API/MCP requests.
last_synced: 2026-09-22T19:00:00.000Z
---

# IP access restrictions

**Available on Enterprise plans. Currently in beta — contact your Growth Strategist or [Clay support](https://www.clay.com/support) if you have questions.**

IP access restrictions let workspace admins control which IP addresses can connect to a Clay workspace. When restrictions are enabled, requests from addresses not on the allowlist are blocked before reaching workspace data. Enterprise admins can configure restrictions separately for two access paths:

-   **Web app** — browser sign-in and table access
-   **API** — Clay API keys, webhooks, OAuth integrations, and MCP requests

Clay support sessions are not affected by IP access restrictions regardless of the allowlist configuration.

## How to set up IP access restrictions

Only workspace admins can view and edit these settings. The configuration is self-serve through the Clay app.

1.  Navigate to `Settings` > `Workspace settings`.
2.  Scroll to the **Security** section.
3.  On the **IP access restrictions** card, click **Add allowlist**.
4.  Enter a name for the allowlist (for example, "HQ network" or "VPN range").
5.  Enter IP addresses or CIDR ranges — one per line. IPv4, IPv6, and CIDR notation are all accepted (for example, `198.51.100.0/24`). The modal displays your current IP address and lets you add it with one click.
6.  Under **Applies to**, choose **Web app** or **API**. An allowlist covers one path — to restrict both, create a separate allowlist for each.
7.  Click **Add allowlist** to save.
8.  Back on the IP access restrictions card, toggle **Web app** and/or **API** to the **Restricted** state to begin enforcing the allowlist.

To add more allowlists — for example, separate entries for different office ranges or VPN providers — repeat steps 3–7. All active allowlists for a category are combined: a request is allowed if its IP address matches any allowlist in the set.

## What is covered

| Path | What is restricted |
| --- | --- |
| Web app | Browser sign-in and table access |
| API | Clay API keys, webhooks, OAuth integrations, and MCP requests |
| Clay support | **Not restricted** — Clay support sessions bypass IP restrictions |

## What members see when blocked

If a workspace member connects from an IP address that is not on the allowlist, they see an "Access restricted" screen with the message: *"You are not allowed to connect to this workspace from your current IP address. Please connect to your VPN or corporate network and try again, or contact a workspace admin if you believe this is a mistake."*

From the blocked screen, they can switch to another Clay workspace they have access to, or sign out.

## Allowlist limits and accepted formats

Each allowlist accepts up to **50** IP addresses or CIDR ranges. Allowlist names can be up to **100 characters**.

Accepted formats: individual IPv4 or IPv6 addresses, CIDRv4 ranges (for example, `198.51.100.0/24`), and CIDRv6 ranges. Enter one address or range per line.

## Allowlisting automation and agent IPs

The API restriction covers all non-browser access, including MCP requests, Clay API key calls, and webhook sources. If your workspace uses AI agents, automation tools, or Claygent running from external systems, the IP addresses those tools connect from must be included in the API allowlist. Requests from unlisted addresses will receive a `403` error.

## Propagation timing

Changes to allowlists take up to **10 minutes** to propagate across all requests. Plan ahead when modifying or removing IP ranges.

## Avoiding lockout

Before saving a configuration change, Clay checks whether the updated allowlist would block your current IP address from web access. If it would, the change is rejected with an error, and you must add your current IP or CIDR range before saving.

If you are already locked out and cannot reach the workspace UI, contact a workspace admin who can access the workspace from an allowlisted address to update the allowlist.
