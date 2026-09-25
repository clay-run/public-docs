---
title: IP access restrictions
description: Restrict which IP addresses can reach your Enterprise workspace — configure separate allowlists for browser sessions and API traffic.
last_synced: 2026-09-22T19:00:00.000Z
---

# IP access restrictions

IP access restrictions let workspace admins on the Enterprise plan control which IP addresses can connect to their Clay workspace. Admins create named allowlists of approved IP addresses and CIDR ranges, and enable them independently for browser traffic and API traffic.

**IP access restrictions are available on the Enterprise plan.** Only workspace admins can view or edit this setting.

## How it works

IP access restrictions are enforced in two independent categories:

-   **Web app** — Browser sign-in and workspace access through Clay's web interface.
-   **API** — Clay API keys, OAuth tokens, and webhook integrations.

Each category can be restricted independently. Restricting the web app has no effect on API traffic, and vice versa. You can restrict one category while leaving the other open to everyone.

When a request arrives from an IP address that is not on the allowlist for a restricted category, it is blocked with a 403 error: *Your IP address is not on the allowlist for this workspace.*

**Clay support sessions are not affected by IP restrictions.** Clay's support team can still access your workspace to assist you even when restrictions are enabled.

Changes to IP access restrictions can take up to 10 minutes to take effect across all requests.

## Adding an allowlist

An allowlist is a named group of IP addresses or CIDR ranges. Before you can enable restrictions for a category, you must have at least one allowlist assigned to it.

To add an allowlist:

1.  Go to `Settings` → `Workspace settings`.
2.  In the **Security** section, find the **IP access restrictions** card.
3.  Click **Add allowlist**.
4.  Enter a name for the allowlist (for example, *Corporate VPN* or *NYC office*).
5.  In the **IP addresses** field, enter the addresses you want to allow — one IPv4 address, IPv6 address, or CIDR range per line. Each allowlist supports up to 50 entries.
6.  Under **Applies to**, select **Web app** or **API**. An allowlist covers one category — to cover both, create one allowlist for each.
7.  Click **Add allowlist** to save.

Clay displays your current connecting IP address at the bottom of the address field. Click **Add it** to include your current IP without typing it manually.

## Enabling restrictions for a category

After adding at least one allowlist to a category, you can turn on restrictions for that category:

1.  Go to `Settings` → `Workspace settings` → **Security** → **IP access restrictions**.
2.  Find the **Web app** or **API** section.
3.  Toggle the switch on.
4.  A confirmation dialog shows how many IP addresses the category will be limited to. Click **Turn on** to confirm.

You cannot enable restrictions for a category with no allowlists. Add at least one address first.

**Lockout protection:** Clay will not save a configuration that would block your own IP address from the web app. If your changes would lock you out, you will see an error and the action will not be saved.

## Managing allowlists

To **edit** an allowlist, click on it in the **IP access restrictions** card. You can update its name, IP addresses, and the category it applies to (Web app or API).

To **delete** an allowlist, click the delete icon next to it. If deleting an allowlist leaves a category with no allowlists, restrictions for that category are automatically turned off.

To **disable** restrictions for a category without removing allowlists, toggle the switch off. The allowlists remain saved and can be re-enabled at any time.
