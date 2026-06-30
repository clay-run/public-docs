---
title: Credit budgets
description: Create and manage named credit budgets to organize spend, prevent
  overspend, and govern how Clay credits flow across your organization.
---

# Credit budgets

**Note:** Credit Budgets is currently in open beta for Enterprise plan workspaces. Contact your Clay account team to enable it.

Credit budgets give workspace admins a way to organize credit spend across teams and workflows — think company cards for GTM infrastructure. Instead of a single workspace-wide credit pool with no visibility, admins create named budgets (for example, "Sales Team" or "Marketing Ops"), assign workbooks and other resources to each budget, and set credit limits per budget. This helps prevent overspend, makes it easy to attribute costs to the right team or project, and gives enterprises the governance controls they need to expand Clay usage with confidence.

Credit budgets appear at `Settings` → `Budgets`. Only workspace admins can create and manage budgets.

## How credit budgets work

A **budget** is a named credit pool with:

-   A **credit limit** — the maximum number of credits the budget can spend in its lifetime (limits do not auto-reset on a billing cycle).
-   A **current balance** — how many credits remain (limit minus spend so far).
-   An **access rule** — whether all workspace members can draw from the budget by default, or only members explicitly granted access.
-   An optional list of **users** or **user groups** with explicit access.

When a workbook (or other resource) is assigned to a budget, all credit-consuming actions in that resource count against the budget's balance. If a budget runs out of credits, processing in assigned resources stops until an admin increases the limit or resets the spend.

## Creating a budget

1.  Go to `Settings` → `Budgets`.
2.  Click **Create**.
3.  Enter a budget **name** and set a **credit limit**.
4.  Choose a **default access** setting:
    -   **All workspace members** — any member can assign their workbooks to this budget.
    -   **Only specific users or groups** — only members you explicitly add can use the budget.
5.  Optionally, add specific **users** or **user groups** who should have access.
6.  Click **Save**.

## Assigning resources to a budget

Once a budget exists, workbooks and other resources can be assigned to it. You can assign a single resource from its own settings, or use bulk assignment from the workspace homepage to move multiple resources to a budget at once.

**From a workbook:**

1.  Open the workbook overview panel (click the workbook name).
2.  Find the **Budget** section and select the budget to assign.

**Bulk assignment from the homepage:**

1.  On the workspace homepage, select one or more workbooks.
2.  Click the **Manage** button that appears in the action bar.
3.  Choose **Assign budget** and select the target budget.

**Filtering by budget on the homepage:**

Use the **Budget** filter on the workspace homepage to quickly see all workbooks assigned to a specific budget, making it easy to audit spend allocation across your org.

## Managing budget access

Each budget has an access rule that controls which workspace members can assign their workbooks to it:

-   **All workspace members (default):** Any member can use this budget. Useful for shared cost pools.
-   **Only specific users or groups:** Only the users or user groups listed on the budget can assign resources to it. Members not on the list will see "You don't have access to any budgets" when they try to assign a workbook. Useful for team-specific budgets.

To update access for an existing budget, open it from `Settings` → `Budgets`, click **Edit**, and adjust the access settings.

**Adding a member to a budget's access list only grants them permission to assign workbooks to that budget — it does not move any of their existing workbooks into it.** Workbook budget assignments are always an explicit, per-workbook action.

## Email alerts for budget usage

Clay sends email alerts to workspace admins when a budget reaches specific usage thresholds:

-   **75%** of the credit limit used — early warning.
-   **90%** of the credit limit used — approaching the limit.
-   **100%** of the credit limit used — budget exhausted, processing in assigned resources has stopped.

Alerts fire once per threshold crossing. They reset when an admin increases the credit limit or resets the budget's spend.

## Resetting and adjusting budgets

Admins can increase or decrease a budget's credit limit at any time from `Settings` → `Budgets`. If you need to restart tracking spend from zero, you can reset the budget's spend when editing it.

When a budget is deleted, you can reassign all of its resources to a different budget — or leave them without a budget.

## Credit budgets vs. credit spend limits

Clay has two distinct credit governance features for Enterprise workspaces:

| Feature | What it does | Where to find it |
|---|---|---|
| **Credit budgets** | Named credit pools — assign workbooks to a budget and track spend across teams. | `Settings` → `Budgets` |
| **Credit spend limits** | Per-workbook credit caps — set a maximum spend for a single workbook or table. | `Settings` → `Usage` → `Workbook limits` |

These features are complementary. You can use spend limits to cap individual workbooks while also assigning them to a budget for team-level cost attribution.
