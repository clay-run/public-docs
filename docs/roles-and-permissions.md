---
title: Roles and Permissions
description: "Clay has three workspace roles: Admin, Editor, and Viewer. Admins have full access; Editors can create tables, workflows, and integrations but not audiences or CRM exports; Viewers are read-only. Enterprise workspaces can grant Viewers editor-level access to specific workbooks."
last_synced: 2026-07-02T20:01:45.311Z
---

# Roles and Permissions

Clay uses three workspace roles to control what each member can do. A user's role applies across the workspace unless they're explicitly granted elevated access to a specific workbook (Enterprise only).

## Roles overview

**Admin**

Full workspace access. Admins can:

-   Invite and remove team members, change their roles
-   Access all workspace settings (billing, integrations, team management)
-   Create, edit, and delete any table, workbook, workflow, or integration in the workspace
-   View and manage all workspace data and connections
-   Configure Audiences — connect data sources, create and edit segments, run enrichments, and export records

**Editor**

Can create and modify resources, but not manage the workspace itself. Editors can:

-   Create and edit tables, workbooks, workflows, and integrations
-   Use all data enrichment and lookup providers
-   Export audience segments to Clay workbooks or campaigns

Editors cannot: invite members, access billing, change workspace settings, or perform Audiences write operations (creating segments, running bulk enrichments, configuring data sources, or exporting records to Salesforce).

**Viewer** _(Enterprise only)_

Read-only by default. Viewers can open and view tables and workbooks but cannot create, edit, or run them. Enterprise workspaces can grant a Viewer editor-level access to specific workbooks (see [Workbook and table sharing](https://university.clay.com/docs/workbook-table-sharing-guide)) — that access applies only to the workbook it's granted for and does not extend to workspace-level resources or Audiences.

## Changing a member's role

1.  Go to **Settings** → **Team**.
2.  Find the member you want to update.
3.  Use the role dropdown next to their name to select the new role.

Changes apply immediately. The member does not need to log out or refresh.

## Feature-level access controls

Some features have finer-grained controls on top of the three workspace roles.

**Workbook and table sharing** _(Enterprise)_

Grant specific users or groups access to individual workbooks — useful for giving a Viewer edit access to one workbook without upgrading their workspace role. See [Workbook and table sharing](https://university.clay.com/docs/workbook-table-sharing-guide) for setup instructions.

**Connection restrictions** _(Enterprise, currently in beta)_

Restrict which users or groups can configure workflows using specific integrations (for example, limit who can build with your Salesforce or Google Sheets connection). Admins can also require approval before any member adds a new connection to the workspace. See [Access settings for connections](https://university.clay.com/docs/access-settings-for-connections).

**Credit spend limits** _(Enterprise)_

Set workbook-level credit caps to prevent overspending. Admins can configure a workspace default limit that automatically applies to all new workbooks. For members accessing Clay through AI tools (Claude, ChatGPT, or Glean) via the MCP integration, admins can also set per-user credit limits. See [Credit spend limits FAQ](https://university.clay.com/docs/credit-spend-limits-faq) and [MCP settings](https://university.clay.com/docs/mcp-settings).

**Credit budgets** _(Enterprise, open beta)_

Create named credit spending pools and assign them to users or groups, so spend can be tracked and governed by team or cost center. Workbooks are assigned to a budget, and any Data Credits they consume count against that budget's limit. Access via `Settings` → `Budgets`. See [Credit budgets](https://university.clay.com/docs/actions-data-credits#credit-budgets-enterprise-open-beta) in the Actions & Data Credits guide.

**Audiences**

Viewing and filtering audience data is available to all workspace roles. Most write operations require **Admin** access: creating and editing audience segments, running bulk enrichments, adding or configuring data sources, exporting individual records to Salesforce, and upserting records from a Clay table into Audiences are all Admin-only. Editors can export audience segments to Clay workbooks or campaigns. Viewers have read-only access. For the full breakdown, see [Audiences roles and permissions](https://university.clay.com/docs/audiences#roles-and-permissions). Note that connection access controls also apply to enrichment columns within Audiences — see [Access settings for connections](https://university.clay.com/docs/access-settings-for-connections) for details.
