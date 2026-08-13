---
title: Managing team members
description: Understand Clay's Admin, Editor, and Viewer roles and learn how to invite, update, and remove team members in your workspace.
last_synced: 2026-04-26T01:40:56.525Z
---

# Managing team members

Use this article to understand Clay's user roles and permissions and to invite team members to your workspace, change their roles, remove members, and cancel pending invites.

## Roles and permissions

Clay offers three user roles with different permission levels to help manage your workspace effectively.

### Admin

**Admins** have full control over the workspace and can manage both resources and team membership.

**Capabilities:**

-   Manage all workspace settings and resources.
-   Invite and remove team members.
-   Assign and update user roles.
-   Access billing and workspace configuration.

### Editor

**Editors** are standard users focused on building and working within workspace resources.

**Capabilities:**

-   Create and edit tables, workflows, and integrations.
-   Update records in tables.
-   Delete tables they own.
-   Add or modify columns and data sources.

**Editors cannot:**

-   Add, remove, or change team members' roles.
-   Modify billing settings or purchase credits.
-   Set a connection as the default in `Settings` → `Connections` — this is a workspace admin–only action.
-   Delete connections added by other workspace members — editors can only delete connections they personally added.
-   Create new **Workflows** _(currently in limited access)_ — creating workflows requires workspace admin access.

### Viewer

**Viewers** have read-only access to workspace content.

**Note:** The Viewer role is available on the Enterprise plan only.

## Add a team member to your workspace

Workspace access in Clay is invitation-only. When a new user signs up for Clay, they are automatically placed in their own workspace — they will not join yours unless you explicitly invite them. Your workspace remains private to you until you send an invite.

**If your workspace uses SSO (such as Okta or another SAML identity provider):** Clay's SSO handles authentication only — it does not provision users or add them to your workspace. Adding a user in your identity provider does not create a Clay account or grant access to your organization's workspace. You must send a Clay workspace invite before a user can log in via SSO and be directed to your workspace. If a user clicks the SSO tile before receiving a Clay invite, they will be routed to a new, empty workspace of their own instead of your organization's workspace. Sending a Clay invite after the fact still works — once the user accepts the invite and logs in via SSO, they will be directed to the correct workspace.

To invite a new member to your workspace:

-   Go to `Settings` > `Team`.
-   Click the `+ Invite` button in the top-right corner.
-   Enter the email address of the person you want to invite, then press **Enter** (or type a comma) to confirm it. You can add multiple addresses this way.
-   Select the appropriate role (Editor or Admin) from the dropdown.
-   Click `Send invite`.

The invited person will receive an email to join the workspace with the specified role. The person will appear in your team list with a **Pending** status until they accept.

**If the invitee sees the error "This invite was sent to a different email address"**

This error appears when the invitee is already logged into Clay with a different account than the one the invite was sent to. Clay verifies server-side that the logged-in account's email matches the invite email — if they don't match, the invite cannot be accepted from that session. To resolve it, have the invitee open the invite link in an **incognito or private browsing window** (where no Clay session is active) — they will be prompted to sign in or sign up with the correct email and can then accept the invite. Alternatively, they can log out of Clay first and then click the invite link again.

**If the invitee sees the error "Email cannot be used"**

This error appears when the invitee tries to sign up with a plus-addressed email — an address that contains a `+` character, such as `alexis+hdb@domain.com`. Clay does not accept plus-addressed emails for account creation. To resolve it:

1. The inviter should go to `Settings` > `Team`, cancel the pending invite sent to the plus-addressed email, and send a new invite to the plain version of the address (for example, `alexis@domain.com` instead of `alexis+hdb@domain.com`).
2. The invitee should then sign up using that plain email address.

## Change a team member's role

To update a member's role:

-   Navigate to `Settings` > `Team`.
-   Locate the team member whose role you want to update.
-   Use the dropdown menu next to their name to select the desired role.
-   Changes are applied immediately.

## Remove a team member

To remove a member from your workspace:

-   Go to `Settings` > `Team`.
-   Find the member you wish to remove.
-   Click the `…` (three-dot) menu at the end of their row.
-   Select `Remove member`.
-   Confirm the removal in the dialog that appears.

**What happens when you remove a member:**

-   All tables, workbooks, and groups owned by the removed member are automatically transferred to the longest-tenured admin in the workspace (the admin whose admin role was granted earliest).
-   You cannot remove the last admin from a workspace — at least one admin must remain at all times.
-   Access is revoked immediately. If the removed member has an active browser session open, they are not logged out of the current page right away — but their workspace permissions are invalidated instantly, so any new action, page refresh, or navigation will return an access-denied error.

**Transferring ownership when a team member leaves**

If a former employee owns tables or workbooks in your workspace, there is no separate "transfer ownership" UI in Clay — removing the former member from the workspace is how you do it. All tables, workbooks, and groups they owned will automatically reassign to the longest-tenured admin (the workspace admin whose admin role was assigned earliest).

## Cancel a pending invite

If a team member hasn't accepted their invite yet, they appear in `Settings` > `Team` with a **Pending** status. There is no separate "cancel invite" button — use the same `Remove member` action:

-   Go to `Settings` > `Team`.
-   Find the pending entry (shown with a **Pending** badge).
-   Click the `…` (three-dot) menu at the end of their row.
-   Select `Remove member`.

Once removed, you can re-invite the same email address if needed. Only workspace admins can cancel pending invites.

## Export your team member list

Clay does not currently offer a built-in option to export your workspace team members as a CSV. Your team member list can only be viewed and managed directly in `Settings` > `Team`. To contact support for assistance with bulk user management tasks, reach out via the in-app chat.
