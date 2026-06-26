---
title: Credit budgets
description: Create and manage named budget pools to organize and govern credit spend across your enterprise workspace.
last_synced: 2026-06-26T00:00:00.000Z
---

# Credit budgets

**Currently in beta — available on Enterprise plan workspaces.**

Credit budgets let workspace admins create named budget pools, assign them to workbooks, tables, and campaigns, and track credit allocation across teams and projects. Think of budgets like company cards for your GTM workflows: admins can allocate credits to specific users or teams, get visibility into how credits are being spent, and prevent overspend as Clay scales across your organization.

## Accessing budgets

Go to `Settings → Budgets` to manage your workspace's budgets. The **Budgets** tab lists all budgets in your workspace. Only workspace admins can create and modify budgets.

## Creating a budget

1.  Go to `Settings → Budgets`.
2.  Click **Create**.
3.  Enter a name for the budget and, optionally, set a credit limit.
4.  Configure who can access this budget and confirm.

Once a budget is created, it appears in the budget list and can be assigned to workspace resources.

## Assigning a budget

Budgets can be assigned to workbooks, tables, and campaigns from the workspace homepage.

**Assign a single resource:**

1.  On the workspace homepage, hover over a workbook or table and open its dropdown menu.
2.  Select **Assign budget** and choose a budget from the list.

**Bulk-assign multiple resources:**

Select multiple resources using their checkboxes, then use the bulk actions dropdown to assign all selected items to a budget at once.

## Filtering the homepage by budget

A **Budget** filter appears in the workspace homepage filter bar when budgets are enabled. Use it to scope the homepage view to workbooks and tables assigned to a specific budget — useful for reviewing spend for a particular team or project.

## Email alerts

When a budget's credit usage crosses a threshold, Clay sends email notifications to workspace admins and all users with explicit access to that budget:

-   **Warning** — sent when usage reaches 80% of the budget's credit limit
-   **Limit reached** — sent when usage hits 100% of the budget's credit limit

Alerts are sent once per threshold crossing. If you update the budget's credit limit, alert thresholds reset.

## Credit budgets vs. credit spend limits

Credit budgets and [credit spend limits](credit-spend-limits-faq.md) are two complementary credit governance features. Credit budgets help you _organize and attribute_ spend across teams and projects; credit spend limits _cap_ how much an individual workbook or table can consume.

For full details on setting per-workbook and per-table spending caps, see [Credit spend limits FAQ](credit-spend-limits-faq.md).
