---
title: Trusted domain access
description: Let teammates with a verified company email join your Enterprise workspace in one click — no invite required. Set up in Settings → Workspace → Trusted domain access.
last_synced: 2026-09-29T00:00:00.000Z
---

# Trusted domain access

Trusted domain access lets Enterprise workspace admins add their verified company email domain to their workspace settings. Once configured, any teammate who signs up for Clay with an email at that domain can join your workspace in one click — no individual invite required. This lets new teammates get started in Clay right away and helps organizations avoid unnecessary workspace sprawl.

**Trusted domain access is available on Enterprise plan workspaces.** Only workspace admins with a verified company email address can configure it.

## Set up trusted domain access

1. Go to `Settings` → `Workspace settings`.
2. Scroll to the **Trusted domain access** section.
3. Click **Add [your-domain.com]** — Clay detects and pre-fills your company domain from your verified admin email address.
4. Your domain is added. Teammates who sign up with an email at that domain will see a one-click option to join your workspace.

**If you don't see the Add button:** Your admin email address may not be verified, or it may be a public email provider (such as gmail.com or outlook.com). Only verified company email addresses can be used to add a domain.

## What new teammates experience

When a teammate signs up for Clay using an email that matches your allowed domain, they are shown a prompt to join your workspace in one click — no separate invitation email is required. Their email address must be verified before they can join via this path.

## Default role for new joiners

When a teammate joins through trusted domain access, they are automatically assigned a workspace role.

- **Enterprise workspaces:** Workspace admins can configure the default role. In the **Trusted domain access** section, use the **Default role for users who join via an allowed domain** dropdown to choose **Editor** or **Viewer**. The workspace-admin role cannot be set as the default join role.
- **Other workspaces:** New joiners are assigned the **Editor** role. This is not configurable.

## Remove an allowed domain

To stop allowing one-click joins from a domain:

1. Go to `Settings` → `Workspace settings` → **Trusted domain access**.
2. Click the **×** on the domain chip you want to remove.

Once removed, teammates with an email at that domain can no longer join without an explicit invite. **Existing workspace members keep their access** — removing a domain does not revoke access for anyone already in the workspace.

## Restrictions

- **Only verified company domains can be added.** Public email providers (gmail.com, outlook.com, and similar free providers) cannot be added.
- **Admins can only add their own verified domain.** You cannot add a domain that does not match your own verified email address.
- **Duplicate domains are not allowed.** Each domain can only be added once per workspace.

## Relationship to SSO and invites

Trusted domain access is separate from Single Sign-On (SSO). SSO controls how your team authenticates (through your identity provider), while trusted domain access controls workspace membership — whether someone can join without an individual invite. Both can be active at the same time on an Enterprise workspace.

For workspaces without trusted domain access, or for inviting specific individuals outside your domain, use the standard invite flow in `Settings` → `Team` → `+ Invite`. See [Managing team members](./managing-team-members.md) for details.
