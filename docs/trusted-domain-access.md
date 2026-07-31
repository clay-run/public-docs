---
title: Trusted domain access
description: How workspace admins can configure trusted domain access so teammates can join a Clay workspace using their company email domain without an invitation.
last_synced: 2026-07-31T18:57:56.757Z
---

# Trusted domain access

Let teammates join your Clay workspace on their own by allowing your company email domain.

Trusted domain access lets a workspace admin allow a company email domain so teammates can join the workspace on their own. Anyone who signs up to Clay with an email at an allowed domain sees the workspace as a joinable option and can join in one click — no invite required.

**Note:** Trusted domain access is rolling out gradually, so the section may not appear in your workspace yet. Only workspace admins who can manage access are able to configure it.

## Adding a trusted domain

1.  Open `Settings` and go to the `Workspace` tab.
2.  Scroll to the `Trusted domain access` section.
3.  Click `Add [your domain]` — the button comes prefilled with the domain from your own verified email address.

You can only allow the domain of your own verified email address, and public email providers are excluded. If your email address isn't verified yet or uses a free provider, the button is replaced with `Only admins with a verified company email address can add a domain`. Once your domain is added the button disappears, so a workspace ends up with more than one allowed domain only when admins with different company domains each add their own.

Each allowed domain shows as a removable chip. To remove one, click the clear (`✕`) control on its chip and confirm in the `Remove [domain]?` dialog. Removing a domain stops new people from joining with it, but people who already joined keep their access.

## Setting the default role for people who join

On Enterprise workspaces, use the `Default role for users who join via an allowed domain` dropdown under the domain list to choose the role new joiners receive. New joiners get `Editor` unless you change it, the `Admin` role can't be assigned this way, and which other roles you can pick from depends on the roles enabled for your workspace. The role applies to everyone who joins through an allowed domain going forward.

On other plans the dropdown isn't available, and the section shows `Users who join will be given the Editor role` instead.

**Note:** Trusted domain access does not verify DNS ownership of a domain. Anyone who signs up with an email at an allowed domain will see your workspace as joinable, so allow only domains you control and review new members after they join.

## What people see when they join

When someone signs up to Clay with an email at one of your allowed domains and doesn't already belong to a workspace, they reach a `Join a Clay workspace` step. It lists the workspaces that match their email domain, each with its name and member count and a `Join` button. Clicking `Join` adds them to that workspace with the default role you set. A `Create new workspace instead` link lets them name and create their own workspace instead. If no workspace matches their domain, onboarding continues normally and this step doesn't appear.

## Requesting more access after joining

Anyone who joins through an allowed domain with the `Viewer` role sees a `You joined as a viewer.` banner prompting them to `Request editor access`. Clicking it emails your workspace admins, who can then change that person's role from the `Team` tab in `Settings`. The banner can be dismissed, and it stops appearing once the person requests access or dismisses it.

## FAQs

### Am I notified when someone joins through an allowed domain?

No. Joining through an allowed domain doesn't send you a notification or an email. New members appear in the `Team` tab in `Settings`, so check there to see who has joined.

### Will people who already have a Clay account at my domain be prompted to join?

No. The join step never lists workspaces someone is already a member of, and it doesn't reach people who are already working in a Clay workspace. Adding a domain also doesn't change anything for people already in your workspace.

### Is this the same as SAML SSO or SCIM?

No. Trusted domain access is a self-serve way for teammates to join. It doesn't require an identity provider, DNS verification, or automatic provisioning, and it doesn't change how existing members sign in.
