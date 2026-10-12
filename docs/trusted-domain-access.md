---
title: Trusted domain access
description: Allow teammates with your company email domain to join your Enterprise workspace in one click—no invite required. Configured in Settings → Workspace, with an admin-selectable default role.
last_synced: 2026-09-28T14:15:01.000Z
---

# Trusted domain access

Trusted domain access lets Enterprise workspace admins add their company email domain so that anyone who signs up for Clay with a matching email address can join the workspace in one click—no invite required. New teammates can get started in Clay immediately, and organizations can avoid workspace sprawl from employees accidentally creating separate personal workspaces.

**Trusted domain access is available on Enterprise plans only.** Workspace admins configure it in `Settings` → `Workspace` → **Trusted domain access**.

## Setting up trusted domain access

Only workspace admins can configure trusted domain access.

To add your company domain:

1. Go to `Settings` → `Workspace` → **Trusted domain access**.
2. Enter your company email domain (for example, `acme.com`). Clay verifies that the domain matches your own verified email address.
3. Choose a **default role** for teammates who join this way — **Editor** or **Admin**.
4. Save your changes.

Once a domain is added, any new Clay signup using a matching email address will see the option to join your workspace immediately — no separate invite step required.

## How teammates join via trusted domain access

When a new user signs up for Clay with an email address that matches your workspace's trusted domain:

1. Clay detects the domain match at signup.
2. The user is shown an option to join your workspace in one click — no invite email is sent or needed.
3. Clicking to join adds them to the workspace with the default role your admin configured.

The new teammate can start using Clay right away. There is no pending invite to manage on the admin's side, and no action required from the admin once the domain is configured.

## Default role

When setting up trusted domain access, admins select the default role assigned to everyone who joins through this path — **Editor** or **Admin**:

- **Editor** — can create and edit tables, workflows, and integrations, but cannot manage team members or billing settings.
- **Admin** — has full workspace access, including team and billing management.

After a teammate joins via trusted domain access, any workspace admin can update their role at any time from `Settings` → `Team`.

## When to use trusted domain access vs. direct invites

Use trusted domain access to allow any employee with your company email address to self-onboard into Clay without waiting for an invite. This is especially useful for large organizations where managing individual invites for every new hire is impractical.

Continue using direct invites (`Settings` → `Team` → `+ Invite`) when you need to:

- Give access to external contractors or partners whose email domain differs from your company domain.
- Control exactly who joins and review each addition individually.
- Assign a specific role that differs from the trusted domain default.

Trusted domain access and direct invites work together — both can be active at the same time. Teammates who join via trusted domain access appear in `Settings` → `Team` alongside teammates who were directly invited.
