---
title: Roles and permissions
source_url: https://university.clay.com/docs/roles-and-permissions
description: Understand roles and permissions in Clay.
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
2.  Under `Access permissions`, change `Edit access` to `Admin and invited collaborators only`.
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

Admins control which Functions reps can access (via the Functions settings page) and can set per-user credit budgets. See [MCP settings](https://university.clay.com/docs/mcp-settings) for details.

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
-   Click the `…` (three-dot) menu next to their name.
-   Select `Remove member`.
-   Confirm the removal in the dialog that appears.

**What happens when you remove a member:**

-   All tables, workbooks, and groups owned by the removed member are automatically transferred to the longest-tenured admin in the workspace (the admin whose admin role was granted earliest).
-   You cannot remove the last admin from a workspace — at least one admin must remain at all times.

## Edit access levels in a workbook

Workspace admins can edit access levels for specific workbooks. This helps prevent accidental changes to important tables.

1.  In a workbook, click the title → `Edit workbook settings`.
2.  Under `Edit Access`, select the desired access level.
3.  If `Workspace admins and specific collaborators` is selected, an option to `+ Add collaborators` will appear.
