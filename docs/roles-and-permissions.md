---
title: Roles and permissions
description: Roles, permissions, and access control tools available in Clay workspaces.
last_synced: 2026-04-26T01:40:33.352Z
---

# Roles and permissions

Understand roles and permissions in Clay.

## Roles in Clay

Clay offers three user roles with different permission levels to help manage your workspace effectively.

### Admins

Admins have full control over the workspace with these permissions:

-   Manage all workspace settings and resources.
-   Invite and remove team members.
-   Assign and update user roles.
-   Access billing and workspace configuration.

### Editors

Editors are standard users who can:

-   Create and edit tables, workflows, and integrations.
-   Update records in tables.
-   Delete tables they own.
-   Add or modify columns and data sources.

_They cannot:_

-   Add, remove, or change team members' roles.
-   Modify billing settings or purchase credits.

## Viewers (Enterprise only)

Viewers have limited access to protect sensitive data. By default, they can only view workspace content and **cannot create new tables or workbooks**.

### Granting Viewers additional access

Viewers can be granted Editor access to specific tables or workbooks, or added as workbook collaborators. When given this access, they can:

-   Update records
-   Add and edit columns or sources
-   Create tables within the workbook
-   Run actions and enrichments

**Limitations:**

-   Cannot create workbooks at the workspace level
-   Cannot manage workbook credit spend limits

**To add a Viewer as a workbook collaborator:**

1.  In the workbook, go to workbook settings on the right side.
2.  Under `Access permissions`, change `Edit access` to `Admins and invited collaborators only`.
3.  Click `+ Add collaborator` and select the Viewer.

## Sales rep _(Beta)_

**Note:** The Sales Rep role is currently in beta — contact support to request access for your workspace.

The sales rep role is designed for team members who need to set up email accounts for the Clay Sequencer and/or access Clay through AI tools (Claude, ChatGPT, or xAI) via the Clay MCP integration. Users with this role **cannot access the standard Clay workspace** — they have no access to tables, workbooks, or other workspace resources.

**Sales reps can:**

-   Set up and manage their own email accounts for use in the Clay Sequencer
-   Look up company and contact information on demand through their AI tool
-   Call Functions built centrally by Ops teams (for example, "find LinkedIn from email" or "generate outbound messages")
-   Run Ops-built workflows directly from their AI chat interface

**They cannot:**

-   Access tables, workbooks, or any other part of the standard Clay interface
-   Create or edit workflows directly in Clay

Admins control which Functions reps can access (via the Functions settings page) and can set per-user credit limits. See [MCP settings](https://university.clay.com/docs/mcp-settings) for details.
**If you were assigned the Sales Rep role but need access to the standard Clay workspace**, contact your workspace admin and ask them to change your role. Admins can update roles at `Settings` → `Team`.

**Note:** Currently, we do not support table-level view restriction. Members can view all tables/workbooks once invited to a workspace.

## Add workspace members

To invite a new member to your workspace:

-   Go to `Settings` → `Team`.
-   Click the `+ Invite` button, enter the email address of the person you want to invite, then press **Enter** (or type a comma) to confirm it. You can add multiple addresses this way.
-   Select the appropriate role from the dropdown and click `Send invite`.
-   The invited person will receive an email to join the workspace with the specified role.

### **Change a team member's role**

To update a member's role:

-   Go to `Settings` → `Team`.
-   Find the member's name and use the dropdown menu next to their name to select the desired role.
-   Changes are applied immediately.

### **Remove a team member**

To remove a member from your workspace:

-   Go to `Settings` → `Team`.
-   Find the member you wish to remove.
-   Click the `…` (three-dot) menu at the end of their row.
-   Select `Remove member`.
-   Confirm the removal in the dialog that appears.

**What happens when you remove a member:**

-   All tables, workbooks, and groups owned by the removed member are automatically transferred to the longest-tenured admin in the workspace (the admin whose admin role was granted earliest).
-   You cannot remove the last admin from a workspace — at least one admin must remain at all times.
-   Access is revoked immediately. If the removed member has an active browser session open, they are not logged out of the current page right away — but their workspace permissions are invalidated instantly, so any new action, page refresh, or navigation will return an access-denied error.

## Edit access levels in a workbook _(Enterprise only)_

**Note:** Workbook-level access restriction is available on Enterprise plan workspaces only. Non-Enterprise workspaces do not have the `Edit Access` settings shown below.

Workspace admins can edit access levels for specific workbooks. This helps prevent accidental changes to important tables.

1.  In a workbook, click the title → `Edit workbook settings`.
2.  Under `Edit Access`, select one of the following access levels:
    -   **Admins and editors in this workspace** — all admins and editors in the workspace can access the workbook.
    -   **Admins and invited collaborators only** — restricts access to admins and any collaborators you explicitly invite.
3.  If `Admins and invited collaborators only` is selected, an option to `+ Add collaborators` will appear.

## Related access controls

Beyond roles, workspace admins have additional tools to control what users can do:

**User groups** _(Enterprise, currently in beta)_

Group workspace members (for example, by team) to manage access at scale. Granting a group access to a connection or workbook instantly gives every group member that access — no need to add people one by one. See [User groups](https://university.clay.com/docs/user-groups).

**Connection restrictions** _(Enterprise, currently in beta)_

Restrict which users or groups can configure workflows using specific integrations (for example, limit who can build with your Salesforce or Google Sheets connection). Admins can also require approval before any member adds a new connection to the workspace. See [Access settings for connections](https://university.clay.com/docs/access-settings-for-connections).

**Credit spend limits** _(Enterprise)_

Set workbook-level credit caps to prevent overspending. Admins can configure a workspace default limit that automatically applies to all new workbooks. For members accessing Clay through AI tools (Claude, ChatGPT, or Glean) via the MCP integration, admins can also set per-user credit limits. See [Credit spend limits FAQ](https://university.clay.com/docs/credit-spend-limits-faq) and [MCP settings](https://university.clay.com/docs/mcp-settings).

**Credit budgets** _(Enterprise, open beta)_

Create named credit spending pools and assign them to users or groups, so spend can be tracked and governed by team or cost center. Workbooks are assigned to a budget, and any Data Credits they consume count against that budget's limit. Access via `Settings` → `Budgets`. See [Credit budgets](https://university.clay.com/docs/actions-data-credits#credit-budgets-enterprise-open-beta) in the Actions & Data Credits guide.

**Audiences**

There are currently no configurable workspace-level access controls specific to the Audiences feature — you cannot restrict which workspace members can view or filter audience data. However, **setting up data sources in Audiences requires Admin access**: Editors can view and filter audiences but cannot add or configure sources. If you're an Editor who needs to connect a source, ask a workspace Admin to do it, or have your role upgraded. Note that connection access controls do apply to enrichment columns within Audiences — see [Access settings for connections](https://university.clay.com/docs/access-settings-for-connections) for details.
