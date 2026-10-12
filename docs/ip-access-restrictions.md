---
title: IP access restrictions
description: Restrict which IP addresses can access your Clay workspace, for web app sessions and API access. Available in beta on Enterprise plans.
last_synced: 2026-09-22T19:00:00.000Z
---

# IP access restrictions

**Currently in beta on Enterprise plans.** Contact Clay support to have IP access restrictions enabled for your workspace.

IP access restrictions let Enterprise workspace admins define which IP addresses are allowed to access the workspace. Once configured, any request from an IP address not on an allowlist is blocked and the user sees an explanation of why access was denied. If restrictions are enabled but no allowlists have been added, all connections are permitted as normal.

Workspace admins can access this setting at `Workspace Settings` > `Security` > **IP access restrictions**. The setting is not visible to workspace members or editors.

## What IP access restrictions cover

The feature applies to two categories of access, each toggled and configured independently:

- **Web app** — browser sessions from team members accessing Clay at [app.clay.com](https://app.clay.com)
- **API** — requests made using Clay API keys, OAuth access tokens, or user API tokens, including webhook integrations and MCP traffic

You can restrict one category without restricting the other. For example, you can require that browser users connect from corporate IP addresses while leaving API access unrestricted.

## Configuring allowlists

1. Go to `Workspace Settings` > `Security` > **IP access restrictions**.
2. Under **Web app** or **API** (or both), add a new allowlist.
3. Enter the IP addresses or CIDR ranges your organization uses. Both IPv4 and IPv6 addresses are accepted, in plain address or CIDR notation.
4. Save your changes.

**Limit:** Each allowlist supports up to 50 IP addresses or CIDR ranges.

**Before enabling restrictions:** Confirm that your allowlist includes every address your team connects from — including VPN exit addresses, corporate proxy IPs, and any automation or CI/CD addresses. Enabling restrictions against an incomplete allowlist will block legitimate users.

**Lockout protection:** Clay prevents you from saving a configuration that would block your own current IP address from web app access. If you see this error, add your current IP to the allowlist before saving.

## What happens when a connection is blocked

When a request comes from an IP address not on the allowlist, the user sees a 403 error page explaining that access is restricted. Directing users to connect through their VPN or corporate network resolves the issue if their organization uses one.

## Who can configure IP access restrictions

Only workspace admins can view and manage IP access restrictions. Workspace members and editors do not see this setting in Workspace Settings.
