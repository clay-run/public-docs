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
    -   **Anyone in the workspace** — any member can assign their workbooks to this budget.
    -   **Specific people and groups** — only members you explicitly add can use the budget.
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

-   **Anyone in the workspace (default):** Any member can use this budget. Useful for shared cost pools.
-   **Specific people and groups:** Only the users or user groups listed on the budget can assign resources to it. Members not on the list will see "You don't have access to any budgets" when they try to assign a workbook. Useful for team-specific budgets.

To update access for an existing budget, open it from `Settings` → `Budgets`, click **Edit**, and adjust the access settings.

**Adding a member to a budget's access list only grants them permission to assign workbooks to that budget — it does not move any of their existing workbooks into it.** Workbook budget assignments are always an explicit, per-workbook action.

### Is a credit budget's limit per user or shared?

A credit budget's limit is shared, not per user. Every user, workbook, workflow, and MCP user assigned to a budget draws from the same credit balance — like several people using one company credit card. For example, if a budget named "Sales Team" has a 1,000-credit limit and five reps are on it, the five reps together can spend 1,000 credits from that budget, not 1,000 credits each. Clay has no per-user sub-limit inside a credit budget.

When the shared balance reaches the limit, everything assigned to that budget stops spending credits, even if one person used most of it.

### How do I give each person their own credit budget limit?

To cap each person's spend individually with credit budgets, create a separate budget for each person:

1.  Go to `Settings` → `Budgets` and click **Create**.
2.  Name the budget after the person (for example, "Jane's budget") and set that person's credit limit.
3.  Set default access to **Specific people and groups** and add only that person.
4.  Click **Save**, then repeat for each person ("Joe's budget", and so on).
5.  Assign each person's workbooks and workflows to their own budget. For spend through AI tools, pick that person's budget in the **Budget** column of the `MCP users` table on the `MCP` page.

For spend through AI tools like Claude or ChatGPT, you can also set a per-user monthly MCP credit limit on the `MCP` page instead — see "How do credit budgets work with MCP credit limits?" below.

## How do credit budgets work with MCP credit limits?

Assigning credit budgets to MCP users is available to Enterprise workspaces with credit budgets (currently in beta). MCP credit limits on their own are available on all modern paid plans.

Workspace admins can assign a credit budget to each MCP user — a workspace member who uses Clay through an AI tool such as Claude, ChatGPT, or Glean. On the `MCP` page, use the **Budget** column in the `MCP users` table to pick a budget for that user, or **No budget**. The list shows budgets the user has access to. Credits that user spends through MCP then count against the assigned budget. There is no separate "MCP budget" type — any credit budget can be assigned to MCP users, so you can create a budget just for MCP spend if you want to throttle it separately from workbooks and workflows.

Every MCP call is checked against up to three independent limits at once:

1.  **Workspace credits** — your workspace's overall credit balance. All spend draws from this.
2.  **The user's MCP credit limit** — the per-user monthly cap set on the `MCP` page. See [MCP settings](https://university.clay.com/docs/mcp-settings).
3.  **The user's assigned credit budget** — the shared budget pool, if one is assigned.

All three must have enough credits remaining for an MCP call to go through. Whichever runs out first blocks the call. These limits are separate ceilings, not nested allowances: an MCP credit limit doesn't reserve part of a budget for that user. For example, a user with a 100-credit MCP credit limit on a shared 500-credit budget has two separate counters, and both go down with every MCP call. Other users and resources on the same budget also drain the 500 credits, so the budget can run out before the user reaches their 100-credit MCP limit.

To let a team spend more through MCP while still capping each person, increase the shared budget's limit and set an MCP credit limit for every user on the `MCP` page.

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
