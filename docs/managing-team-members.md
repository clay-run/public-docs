---
title: Managing team members
description: Understand Clay's Admin, Editor, and Viewer roles, how people get added to your workspace (invites, trusted domain access, SCIM), and how to invite, update, and remove team members.
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

## Give a colleague access to your tables instead of sharing your login

If a colleague needs access to your tables, workbooks, or other data in your Clay workspace, invite them to your workspace instead of having them log in with your email and password. Once they accept the invite, your colleague signs in with their own Clay account and can work in your workspace with the role you assign — Editor is the default role. Follow the steps in [Add a team member to your workspace](#add-a-team-member-to-your-workspace) below to send the invite.

## How do people get added to my workspace?

People can join your Clay workspace in only three ways:

-   **Email invite (all plans):** someone in your workspace invites a specific email address from `Settings` > `Team`. See [Add a team member to your workspace](#add-a-team-member-to-your-workspace).
-   **Trusted domain access (Enterprise plans):** anyone who signs up with an email at a domain your admin has allowed can join the workspace without an invite. See [Trusted domain access](#trusted-domain-access).
-   **SCIM provisioning (Enterprise plans):** people assigned to Clay in your identity provider are added to the workspace automatically. See [Is SCIM provisioning included with the SSO add-on?](./single-sign-on.md#is-scim-provisioning-included-with-the-sso-add-on).

**Connecting Clay to Claude or another app does not add anyone to your workspace.** If someone signs in to Clay through the Claude connector, or any other app that connects to Clay through MCP or OAuth, they are not added to your workspace. A person must already be a member of a workspace before they can connect an app to it.

**If people you didn't invite are showing up in your workspace:** check whether trusted domain access is turned on. Go to `Settings` > `Workspace` and look at the **Trusted domain access** section. Anyone who signs up with an email at a domain listed there can join your workspace without an invite.

**New members don't get a credit budget automatically.** Clay does not assign a credit budget to new members, no matter how they joined. To limit a new member's spend, an admin assigns them to a budget in `Settings` > `Budgets` after they join. See [Credit budgets](./credit-budgets.md).

### Trusted domain access

Trusted domain access is available on Enterprise plans. Only workspace admins can set it up. With trusted domain access turned on, anyone who signs up for Clay with an email at an allowed domain can join your workspace without an invite. After signing up, they see your workspace with a **Join** button and join in one click.

To set up trusted domain access:

1.  Go to `Settings` > `Workspace`.
2.  In the **Trusted domain access** section, add your company domain.

Things to know about trusted domain access:

-   **Which domains you can add:** you can only add a domain that matches your own verified company email. Public email providers such as gmail.com can't be added.
-   **Role for people who join:** people who join through trusted domain access get the **Editor** role by default. On Enterprise plans, admins can change this with the **Default role for users who join via an allowed domain** dropdown. The choices are Editor, Viewer, or Sales rep. Admin can't be selected.
-   **Who sees the Join option:** the **Join** button appears when someone with a matching email signs in and doesn't already belong to a workspace. This is usually a first-time signup. It works the same way for every sign-in method: email and password, Google, or SSO. People who already belong to another workspace are taken to it directly and don't see the Join option.

## Add a team member to your workspace

Outside of [trusted domain access](#trusted-domain-access) and SCIM provisioning, workspace access in Clay is invitation-only. When a new user signs up for Clay, they are automatically placed in their own workspace — they will not join yours unless you invite them, or unless one of those two Enterprise features applies to them.

**If your workspace uses SSO (such as Okta or another SAML identity provider):** Clay's SSO handles authentication only — it does not provision users or add them to your workspace. Adding a user in your identity provider does not create a Clay account or grant access to your organization's workspace. You must send a Clay workspace invite before a user can log in via SSO and be directed to your workspace. If a user clicks the SSO tile before receiving a Clay invite, they will be routed to a new, empty workspace of their own instead of your organization's workspace. Sending a Clay invite after the fact still works — once the user accepts the invite and logs in via SSO, they will be directed to the correct workspace.

**If an invited user logs in before clicking the invitation email:** When an invited user visits Clay directly (for example, by going to app.clay.com) before accepting their invitation, Clay has no invite code to act on and automatically creates a new free workspace for that user instead of routing them to your workspace. Once the free workspace exists, every subsequent login redirects the user there — they will not be able to access your workspace even after you re-send the invite. To prevent this, instruct invited users to always access Clay for the first time through the workspace invitation email link, not by logging in directly. If this has already happened, contact Clay support via the in-app chat to delete the erroneously created workspace. Once it is removed, re-send the invitation and have the user accept it through the email link.

To invite a new member to your workspace:

-   Go to `Settings` > `Team`.
-   Click the `Invite` button in the top-right corner.
-   Enter the email address of the person you want to invite, then press **Enter** (or type a comma) to confirm it. You can add multiple addresses this way.
-   Select the appropriate role (Editor or Admin) from the dropdown.
-   Click `Send invites`.

The invited person will receive an email to join the workspace with the specified role. The person will appear in your team list with a **Pending** status until they accept.

**If the invitee sees the error "This invite was sent to a different email address"**

This error appears when the invitee is already logged into Clay with a different account than the one the invite was sent to. Clay verifies server-side that the logged-in account's email matches the invite email — if they don't match, the invite cannot be accepted from that session. To resolve it, have the invitee open the invite link in an **incognito or private browsing window** (where no Clay session is active) — they will be prompted to sign in or sign up with the correct email and can then accept the invite. Alternatively, they can log out of Clay first and then click the invite link again.

**If the invitee sees the error "Email cannot be used"**

This error appears when the invitee tries to sign up using a password with a plus-addressed email — an address containing a `+` character, such as `alexis+hdb@domain.com`. Clay does not accept plus-addressed emails during password-based signup. To resolve it:

1. The inviter should go to `Settings` > `Team`, cancel the pending invite sent to the plus-addressed email, and send a new invite to the plain version of the address (for example, `alexis@domain.com` instead of `alexis+hdb@domain.com`).
2. The invitee should then sign up using that plain email address.

Alternatively, if the invitee has a Google account at that email address, they can sign up using **Continue with Google** instead — the plus-address restriction applies only to password-based signup, not to Google OAuth.

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

## Programmatic user management

Clay does not have a programmatic API for workspace member management. There is no API endpoint to invite users, update their roles, or remove or deactivate them from a workspace. All user management must be done manually through the workspace UI at `Settings` > `Team`.

For automated user lifecycle management through an identity provider (such as automatically adding or removing users when accounts are created or deactivated in Okta), use SCIM provisioning, available on Enterprise plans — see [Is SCIM provisioning included with the SSO add-on?](./single-sign-on.md#is-scim-provisioning-included-with-the-sso-add-on). SSO on its own handles authentication only and does not provision workspace membership automatically.
