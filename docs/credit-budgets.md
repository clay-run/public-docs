---
title: Credit budgets
description: Create and manage named credit budgets to organize spend, prevent
  overspend, and govern how Clay credits flow across your organization.
---

# Credit budgets

**Note:** Credit Budgets is currently in beta and automatically available to all Enterprise plan workspaces.

If you need to allocate credits to specific workbooks, teams, or projects — tracking and capping each group's spend separately — credit budgets is the feature you need. Credit budgets give workspace admins a way to organize credit spend across teams and workflows — think company cards for GTM infrastructure. Instead of a single workspace-wide credit pool with no visibility, admins create named budgets (for example, "Sales Team" or "Marketing Ops"), assign workbooks and other resources to each budget, and set credit limits per budget. This helps prevent overspend, makes it easy to attribute costs to the right team or project, and gives enterprises the governance controls they need to expand Clay usage with confidence.

Credit budgets appear at `Settings` → `Budgets`. Only workspace admins can create and manage budgets.

## How credit budgets work

A **budget** is a named credit pool with:

-   A **credit limit** — the maximum number of credits the budget can spend in its lifetime (limits do not auto-reset on a billing cycle).
-   A **current balance** — how many credits remain (limit minus spend so far).
-   An **access rule** — whether all workspace members can draw from the budget by default, or only members explicitly granted access.
-   An optional list of **users** or **user groups** with explicit access.

When a workbook (or other resource) is assigned to a budget, all credit-consuming actions in that resource count against the budget's balance. If a budget runs out of credits, processing in assigned resources stops until an admin increases the limit or resets the spend.

**Function calls and budget attribution:** When a workbook assigned to a budget calls a Function, the credits consumed by that Function run count against the **calling workbook's budget** — not against the Function itself or the Function creator's workbook. For example, if a marketing team's workbook calls a Function built by RevOps, those credits count against the marketing workbook's budget. This means that assigning a user's workbook to a budget automatically captures all spend from that workbook, including any Function calls it makes. Note: this attribution is one level deep — if a Function calls another Function, the inner Function's spend is attributed to the outer Function rather than the original calling workbook.

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

## Assigning workflows to a budget

Workflow budgets are available to all Enterprise plan workspaces. Any workflow can be assigned to a credit budget, the same way workbooks can. Workspace admins and members who can create workflows can assign a budget to a workflow, subject to each budget's access rule (see "Managing budget access" below).

You can assign a budget to a workflow in any of these ways:

-   **When you create the workflow:** pick a budget as part of creating the workflow.
-   **From workflow settings:** open the workflow's settings, find the **Budget** field, and select the budget to assign. Use this to change a workflow's budget later.
-   **Bulk assignment from the Workflows list:** select one or more workflows (up to 100 at a time), choose **Assign budget**, and select the target budget.

**What a workflow budget pays for:** Everything a workflow calls spends that workflow's budget — including its own steps, plus any table functions and workflow functions the workflow calls.

**When a workflow's budget runs out:** Workflow runs stop, and the run shows this error: "The budget paying for this run has hit its credit limit. A workspace admin can raise the limit or assign a different budget."

### Setting workflow budgets from the Clay CLI and Clay's Agent

The Clay CLI and Clay's Agent have the same workflow budget controls as the Clay app, so workflows built by the agent carry the same spend guardrails.

-   **Create a workflow with a budget:** `clay workflows create --budget-id <budget-id>`
-   **Change an existing workflow's budget:** `clay workflows update <workflow-id> --budget-id <budget-id>`

## Tracking spend by resource on the Budgets page

Open a budget from `Settings` → `Budgets` to see its spend over time. Use the **Breakdown** option to see that budget's spend split by resource — **Workflows** and **Workbooks** — so you can tell how much of a budget's credits went to workflows versus workbooks.

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

## Deleting a budget

Only workspace admins can delete a credit budget. Go to `Settings` → `Budgets` and delete the budget. If workbooks, workflows, or other resources are still assigned to the budget, Clay asks you to choose where they go: reassign them to a different budget, or pick **No budget** to leave them without one. The confirm button reads **Reassign & delete** when resources need to be moved, or **Delete budget** when nothing is assigned.

### Will deleting a budget unpause my workflows?

No. Deleting (removing) a credit budget doesn't unpause, resume, or turn on anything. Workflows, workflow triggers, signals, and tables you paused stay paused until you turn them back on yourself.

### What happens to spend after a budget is deleted?

Deleting a credit budget removes that budget's credit limit. Anything that was assigned to the budget and is still active can start spending credits again:

-   Resources you reassigned to a different budget now count against that budget's credit limit.
-   Resources left with **No budget** spend from your workspace's credits, subject to any other limits (such as credit spend limits) that still apply.
-   Runs already in progress keep running. Any credits they use after the deletion are no longer capped by the deleted budget.

If a resource was stopped only because the budget ran out of credits, it can start processing again once the budget is deleted.

### Before you delete a budget to set up a new run

If you want everything to stay stopped while you delete a budget (for example, before setting up a new budget for a fresh run), check the following first:

1.  Every trigger on the workflows assigned to the budget is paused.
2.  No workflow runs are still in progress.
3.  Nothing else assigned to the budget — such as tables set to auto-run — is still on.

Once those are off, you can safely delete the budget and set up the new run.

## Credit budgets vs. credit spend limits

Clay has two distinct credit governance features for Enterprise workspaces:

| Feature | What it does | Where to find it |
|---|---|---|
| **Credit budgets** | Named credit pools — assign workbooks and workflows to a budget and track spend across teams. | `Settings` → `Budgets` |
| **Credit spend limits** | Per-workbook credit caps — set a maximum spend for a single workbook or table. | `Settings` → `Usage` → `Workbook limits` |

These features are complementary. You can use spend limits to cap individual workbooks while also assigning them to a budget for team-level cost attribution.

**Note:** Neither credit budgets nor credit spend limits can be applied directly to a Function. Credit limits apply to a workbook as a whole — including all Function calls that workbook makes. There is no per-Function credit cap. To limit how much a specific workbook spends (including its Function calls), assign it to a budget with a credit limit or set a per-workbook credit spend limit on it.
