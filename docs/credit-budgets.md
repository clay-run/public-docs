---
title: Credit budgets
description: Manage credit spend across your workspace with shared budget pools for teams and departments. Available in open beta for Enterprise plan customers.
last_synced: 2026-06-25T00:00:00.000Z
---

# Credit budgets

**Credit budgets** are shared spending pools that help workspace admins track, manage, and control credit spend across teams. Create named budgets, set credit limits, grant access to users or groups, and assign workbooks to budgets — so spend is attributed clearly and executions stop before overspend occurs.

**Note:** Credit budgets are currently in open beta for Enterprise plan customers.

## How credit budgets work

Think of budgets like company credit cards for Clay workflows:

1. Admins create named budgets (for example, "Marketing") and set a credit limit for each.
2. Admins grant access to specific users or groups.
3. Users assign their workbooks to a budget. Credits those workbooks consume count against the budget's limit.
4. When a budget's limit is reached, credit-consuming executions stop until an admin resets or increases the limit.

**Budgets vs. workbook credit spend limits:** Credit budgets are shared pools that span multiple workbooks and users — useful for team- or department-level allocation. Workbook credit spend limits cap a single workbook's spend. If a workbook has both a credit spend limit and an assigned budget, credits count against both independently. See [Credit spend limits FAQ](/docs/credit-spend-limits-faq) for details on per-workbook caps.

## Getting started with credit budgets

### Creating a budget

1. Go to `Settings` → `Budgets`.
2. Click `Create`.
3. Fill in the details:
   - **Name** — for example, "Marketing."
   - **Credit limit** — the maximum credits allowed for this budget.
   - **Access** — who can spend from this budget: anyone in the workspace, or specific users and groups. Admins can see and edit all budgets, but must be given budget access to assign them to resources.
4. Click `Create budget` to save.

Once a budget is created, spend tracking begins immediately — not retroactively. Existing workbooks created before budgeting was enabled remain unbudgeted until manually assigned.

### Assigning budgets to resources

Users assign a budget when creating a new workbook. Credits the workbook consumes are tracked against that budget.

- If a user has access to only one budget, it is assigned automatically to all new workbooks they create.
- If a user has access to multiple budgets, they are prompted to select one during workbook creation.
- If a user has no budget access, new workbooks are unbudgeted.

Anyone with edit access to a workbook can reassign it to a different budget they have access to. Budget changes apply to future usage only — historical spend does not move between budgets.

### Assigning budgets when inviting users

When inviting a new team member, admins can configure budget access in the invite flow:

1. Go to `Settings` → `Team` and click `Invite member`.
2. Fill in the user's email and select their role (Admin, Editor, or Viewer).
3. Optionally assign the user to one or more groups — budget access pre-fills based on group selection.
4. Optionally grant the user access to additional budgets.
5. Send the invite.

## Managing budgets

### Viewing budget usage

Go to `Settings` → `Budgets` to see all budgets in your workspace. What you see depends on your role:

- **Admins** can see all budgets and update their names, limits, and access settings. A workspace-level summary at the top shows total purchased credits and remaining credits.
- **Editors and Viewers** see only the budgets they have access to, including each budget's name, limit, remaining balance, and assigned users and groups. Editors and Viewers cannot modify budgets.

A budgets usage widget in the top bar shows a progress bar for each budget you have access to.

### Editing a budget

Admins can click `…` on any budget row and select `Edit` to change its name, limit, or access assignments. Changes take effect immediately for all future runs.

### Resetting a budget's usage

Admins can restore a budget to its full limit by clicking `Edit` and then `Reset usage`. Resetting is disabled if there has been no spend against the budget. Budget history is retained indefinitely.

### Deleting a budget

Budgets with active workbook assignments cannot be deleted. Reassign those workbooks to another budget first.

## Filtering and bulk-assigning budgets on the homepage

From the homepage, admins can:

- **Filter by budget** — use the budget filter to show only workbooks assigned to a specific budget.
- **Bulk-assign budgets** — select multiple workbooks and assign them to a budget at once using the bulk management menu.

## How budgets apply to different resources

### Workbooks

Workbooks are the primary unit of budget assignment. When a workbook runs enrichments, signals, Functions, or Claygents, credits are charged to the workbook's assigned budget.

### Audiences

Audiences uses a single budget for all signal runs and bulk enrichments.

- By default, Audiences has no budget assigned until an admin sets one.
- Only admins can configure the Audiences budget. Go to `Settings` → `Budgets` and select a budget under **Audiences budget**.
- Clay validates that the Audiences budget has sufficient credits before starting any enrichment job. If the budget is depleted, enrichment jobs are blocked until an admin resets or increases the limit.

**Note:** Per-signal and per-enrichment credit limits within Audiences are separate from the Audiences budget — those are resource-level controls similar to workbook credit spend limits.

### MCP users

When setting up MCP access, users are prompted to select a budget from the list they have access to. MCP usage is then charged against that budget.

### Inbox purchases (Campaigns)

When purchasing inboxes for Campaigns, users select which budget to charge at the time of purchase.

### Functions and Claygents

When editing Functions or Claygents directly, users can attribute test spend to a budget. When Functions or Claygents are called from a workbook, spend is attributed to the calling workbook's budget.

## Important to remember

- **Budgets are spending caps, not reserved credits.** The sum of all budget limits can exceed your total workspace credits — you can define limits without dividing your full credit pool upfront.
- **Executions stop when a budget limit is reached.** Workbooks remain editable, but enrichment runs cannot start until the budget is reset, the limit is increased, or the workbook is reassigned to a budget with remaining credits.
- **Budgets do not reset automatically.** Budget balances count down until an admin manually resets them or changes the limit.
- **Unbudgeted resources.** If a workbook has no assigned budget, credits it uses are charged directly to the workspace credit balance.

## FAQs

**What happens when a budget's credit limit is reached?**

All credit-consuming processes for workbooks assigned to that budget stop. Users see an error that the limit has been reached. Workbooks remain fully editable, but enrichment runs cannot start until an admin resets the budget, increases the limit, or the workbook is reassigned to a budget with remaining credits.

**What happens if a run is cancelled mid-execution?**

Credits consumed up to the point of cancellation are charged and not refunded. Partial results are preserved where applicable.

**What happens if I add more credits to my workspace?**

Budget limits don't automatically change when workspace credits are added. Admins can manually adjust limits as needed.

**Can an Editor reassign a workbook to a different budget?**

Yes — anyone with edit access to a workbook can reassign its budget, as long as they have access to the target budget. Changes apply to future runs only.

**What happens if a user loses access to a budget after their workbook is already assigned to it?**

The workbook continues running from its assigned budget. Admins or Editors with workbook access can reassign it to a different budget if needed.

**Can I set time-based budgets that reset monthly?**

No — budgets are persistent spending limits and don't reset automatically. Admins can manually reset a budget to restore its full balance at any time.

**Does this apply to Data Credits only, or Actions too?**

Credit budgets track **Data Credit** spend only.

**What happens to existing workbooks when I first enable credit budgeting?**

Existing workbooks are not automatically assigned to any budget. Their credit usage will be unbudgeted until you manually assign them.

**What if a user is in multiple groups with different budget access?**

They'll have access to all budgets granted to any of their groups. When creating a new workbook, they'll be prompted to select which budget to use if they have access to more than one.

**Whose budget gets charged when a workbook uses a Function or Claygent?**

The calling workbook's budget is charged. All credit spend from that execution is tracked against the workbook's assigned budget, even if the Function or Claygent was created by a different user or team.
