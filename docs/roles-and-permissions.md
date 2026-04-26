---
title: Roles and permissions
source_url: https://university.clay.com/docs/roles-and-permissions
last_synced: 2026-04-26T01:40:33.352Z
upstream_hash: 4a677958cd278fc8e9aaa4b1f91222fda3146fba0d5d057f9fa702ecf90fd5cc
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

## Sales rep

The sales rep role is designed for users who access Clay through AI tools (Claude, ChatGPT, or xAI) via the Clay MCP integration. Users with this role **cannot access the standard Clay workspace**. When they log in, they'll see a page prompting them to connect their AI tool.

**Sales reps can:**

-   Use Clay's data enrichment and functions through their connected AI tool
-   Run Clay-powered lookups and workflows from within Claude, ChatGPT, or xAI

**They cannot:**

-   Access tables, workbooks, or any other part of the standard Clay interface
-   Create or edit workflows directly in Clay

**Note:** Currently, we do not support table-level view restriction. Members can view all tables/workbooks once invited to a workspace.

## Add workspace members

To invite a new member to your workspace:

-   Go to `Settings` → `Team`.
-   Click the `+ Invite` button and enter the email address of the person you want to invite.
-   Select the appropriate role from the dropdown and click `Send invite`.
-   The invited person will receive an email to join the workspace with the specified role.

### **Change a team member's role**

To update a member's role:

-   Go to `Settings` → `Team`.
-   Find the member’s name and use the dropdown menu next to their name to select the desired role.
-   Changes are applied immediately.

### **Remove a team member**

To remove a member from your workspace:

-   Go to `Settings` → `Team`.
-   Find the member you wish to remove.
-   Click the `🗑️`  next to their name.

## Edit access levels in a workbook

Workspace admins can edit access levels for specific workbooks. This helps prevent accidental changes to important tables.

1.  In a workbook, click the title → `Edit workbook settings`.
2.  Under `Edit Access`, select the desired access level.
3.  If `Workspace admins and specific collaborators` is selected, an option to `+ Add collaborators` will appear.
