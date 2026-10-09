---
title: Trusted domain access
description: Let teammates with a verified company email domain join your Enterprise workspace in one click — no invite required.
---

# Trusted domain access

Trusted domain access lets workspace admins add their verified company email domain to an allow-list. When a colleague signs up for Clay with an email address at that domain, they can join the workspace in one click — no invite needed.

**Trusted domain access is available on the Enterprise plan only.** Only workspace admins can configure it.

## Setting up trusted domain access

To add your company domain:

1. Go to `Settings` → `Workspace settings`.
2. Scroll to the **Trusted domain access** section.
3. Click **Add `yourdomain.com`** — Clay auto-detects your domain from your verified admin email address.

Once added, the domain appears as a chip in the Trusted domain access section. Any teammate who signs up for Clay with an email at that domain will see your workspace listed as one they can join.

**Requirements:**

-   You must be a workspace **admin**.
-   Your own Clay account email must be **verified** and on a company domain — Clay automatically offers your domain for you to add.
-   Public email providers (such as gmail.com or outlook.com) cannot be added as allowed domains. Only company domains are accepted.
-   You can only add a domain that matches your own verified email address. If your email is `name@yourcompany.com`, you can add `yourcompany.com` — you cannot add a domain you don't personally have.

## How teammates join

When a new user signs up at [app.clay.com/signup](https://app.clay.com/signup) with an email address at your allowed domain, Clay shows them your workspace as a workspace they can join. They click to join and are added immediately — no invite email required.

Teammates who join via trusted domain access are added to the workspace with the default role configured for your workspace (see [Default role for joining members](#default-role-for-joining-members) below).

## Default role for joining members

On Enterprise workspaces, admins can choose what role teammates receive when they join via a trusted domain. The available options are **Editor** and **Viewer** — the Admin role cannot be assigned automatically through this flow.

To set the default role:

1. Go to `Settings` → `Workspace settings` → **Trusted domain access**.
2. Under **Default role for users who join via an allowed domain**, use the dropdown to select **Editor** or **Viewer**.

If no role has been configured, the default is **Editor**.

## Removing an allowed domain

To remove a domain from the allow-list:

1. Go to `Settings` → `Workspace settings` → **Trusted domain access**.
2. Click the **×** on the domain chip you want to remove.
3. Confirm the removal in the dialog.

**Removing a domain does not affect existing members.** Everyone who already joined through that domain keeps their workspace access. Only future signups at that domain will no longer be able to join without an invite.

## FAQs

**Does trusted domain access replace invites?**

No — it's an additional option, not a replacement. You can still invite individuals one-by-one via `Settings` → `Team`. Trusted domain access is useful for large teams where sending individual invites is impractical.

**What if someone has already created their own Clay workspace with a company email?**

Users who already have a Clay account and workspace will see your workspace listed as joinable after they sign in. They can click to join without losing their existing workspace.

**Can I add more than one domain?**

You can only add domains that match your own verified email address. If your workspace needs to allow multiple company domains (for example, after an acquisition), contact Clay support.

**What happens to a member's tables and data when they join via trusted domain access?**

Nothing changes. The new member joins your workspace with the assigned role, the same as any invited member. Their own personal workspace (if they had one) remains unaffected.
