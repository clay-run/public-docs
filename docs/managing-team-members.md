---
title: Managing team members
description: Understand Clay's Admin, Editor, and Viewer roles, learn how to invite, update, and remove team members, export your member list as a CSV, and transfer ownership of workbooks and tables.
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

## Add a team member to your workspace

By default, workspace access in Clay is invitation-only. When a new user signs up for Clay, they are automatically placed in their own workspace — they will not join yours unless you explicitly invite them. Your workspace remains private to you until you send an invite.

**Enterprise workspaces** can also use [Trusted domain access](./trusted-domain-access.md) to let teammates with a verified company email address join in one click, without a per-person invite.

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

If a former employee owns tables or workbooks in your workspace, how you transfer ownership depends on your plan:

-   **All plans:** Removing the former member from the workspace transfers ownership automatically. All tables, workbooks, and groups they owned reassign to the remaining admin whose admin role was granted earliest — the member being removed isn't counted. For example, if you and the departing member are the only two admins, ownership transfers to you.
-   **Enterprise plans:** You can also transfer ownership of an individual workbook or table without removing anyone. See [Transfer ownership of a workbook or table (Enterprise only)](#transfer-ownership-of-a-workbook-or-table-enterprise-only).

On non-Enterprise plans there's no `Transfer ownership` option — removing the former member is how ownership changes.

## Transfer ownership of a workbook or table (Enterprise only)

**Note:** Manually transferring ownership of a workbook or table is available on the Enterprise plan only. Workspace admins and the current owner of a workbook or table can transfer its ownership.

To transfer ownership of a workbook or table to another workspace member:

1.  Open the settings panel:
    -   For a workbook, open the workbook, click the workbook name in the top bar, and select `Edit workbook settings`.
    -   For a standalone table (a table that isn't inside a workbook), click the `Table settings` gear icon in the table's title bar.
2.  Open the `Access permissions` section.
3.  Under `Owner`, open the `…` menu on the current owner's row and select `Transfer ownership`.
4.  Choose the new owner. Any workspace member can be selected, whatever their role.
5.  Click `Save changes`. Until you save, the panel shows a notice that ownership of the workbook or table "will be transferred to [new owner's name] when you save your changes."

**If you don't see the `Owner` row:** The `Owner` row and `Transfer ownership` option only appear when access is set to `Admins and editors in this workspace`. If the workbook or table is set to `Admins and invited collaborators only`, switch it to `Admins and editors in this workspace` first.

**Things to know about transferring ownership:**

-   Transferring ownership of a workbook also transfers every table inside it. Tables inside a workbook don't have their own `Access permissions` section — transfer the workbook instead.
-   Ownership transfers one workbook or table at a time. There's no bulk transfer — to move everything a former member owns at once, remove them from the workspace.

## Cancel a pending invite

If a team member hasn't accepted their invite yet, they appear in `Settings` > `Team` with a **Pending** status. There is no separate "cancel invite" button — use the same `Remove member` action:

-   Go to `Settings` > `Team`.
-   Find the pending entry (shown with a **Pending** badge).
-   Click the `…` (three-dot) menu at the end of their row.
-   Select `Remove member`.

Once removed, you can re-invite the same email address if needed. Only workspace admins can cancel pending invites.

## Export your team member list

Workspace admins can download the workspace team member list as a CSV file from `Settings` > `Team`. Only the Admin role sees the `Export CSV` button — Editors, Viewers, and Sales Reps don't.

To export your team member list:

1.  Go to `Settings` > `Team`. If your workspace shows `Members` and `Groups` tabs, stay on the `Members` tab.
2.  Optionally, narrow the list with the search box or the role, status, and `Managed via` filters, and sort the list the way you want it.
3.  Click `Export CSV` next to the search box (beside `Invite`).

The CSV file downloads immediately — no dialog opens — and you'll see a "CSV exported" confirmation. The file is named `workspace-members-YYYY-MM-DD.csv`, using today's date.

The exported team member CSV contains the following columns:

-   **Name** — the member's full name. For pending invitations, the email address is used instead.
-   **Email** — the member's email address.
-   **Role** — Admin, Editor, Viewer, or Sales Rep.
-   **Groups** — the names of the [user groups](./user-groups.md) the member belongs to, separated by a semicolon and a space (for example, `Analysts; Revenue`). This column is blank for members who aren't in any group.

**What's included in the export:** The CSV contains exactly the members shown in your current view, in the order they're displayed. Your current search, role, status, and `Managed via` filters all apply, and pending invitations are included when they appear in the list. To export every member, clear all filters and the search box before clicking `Export CSV`.

**If the `Export CSV` button is disabled:** The button is disabled when no members match your current search or filters — clear them to show members again. In workspaces that use user groups, the button is also disabled until members' group memberships finish loading.

## Programmatic user management: API and SCIM provisioning

Clay doesn't have a public API for workspace member management. There's no API endpoint to invite users, update their roles, or remove them from a workspace, and the Clay CLI can only list and view users.

To automate user provisioning and deprovisioning, Enterprise workspaces can use [SCIM provisioning](./scim-provisioning.md). SCIM provisioning adds members to your Clay workspace when they're assigned to Clay in your identity provider (such as Okta), removes them from the workspace when they're unassigned or deactivated, and sets their workspace roles from your identity provider groups. Workspace admins set it up in `Settings` > `Workspace` > `SCIM provisioning`.

On plans without SCIM provisioning, manage members manually in `Settings` > `Team`. [Single Sign-On (SSO)](/docs/single-sign-on) handles sign-in only and doesn't add or remove workspace members.