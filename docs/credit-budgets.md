---
title: Credit budgets
description: Create and manage team-level credit budgets to organize spend, prevent overspend, and govern Clay usage across your organization.
last_synced: 2026-06-25T22:00:00.000Z
---

# Credit budgets

**Note:** Credit budgets are available on the Enterprise plan and are currently in open beta. Contact your Growth Strategist or Clay account team to enable this feature for your workspace.

Credit budgets help workspace admins track, manage, and understand credit spend across their workspace. Create budgets and assign them to users to improve accountability, understand where credits are being used, and prevent overspend as adoption scales across the organization.

**How budgets differ from workbook credit spend limits:** Workbook credit spend limits cap a single workbook's spend. Credit budgets are shared pools that span multiple workbooks and users — useful for team- or department-level allocation. If a workbook has both a credit spend limit and an assigned budget, credits count against both independently. See [Credit spend limits FAQ](/docs/credit-spend-limits-faq) for details on workbook-level limits.

## How credit budgets work

Think of budgets like credit cards for Clay workflows:

1.  Admins create named budgets (e.g., "Marketing") and set a credit limit for each.
2.  Grant access to groups or individuals.
3.  Users tie their workbooks directly to a budget. Any credits consumed by those resources are tracked against the assigned budget. When a budget's limit is reached, executions stop.

## Getting started with credit budgets

**Tip:** User groups are the scalable path for team-based assignments. Individual user assignments work best for Clay power users who need cross-team access that doesn't map to any single group.

### Creating a budget

1.  Go to `Settings` → `Budgets`.
2.  Click `Create`.
3.  In the modal, fill in:
    -   **Name** — for example, "Marketing."
    -   **Credit limit** — maximum allowed spend for this budget.
    -   **Access** — who can spend from this budget: anyone in the workspace, or specific users and groups. While admins can see and edit all budgets, they must be given budget access to assign them to resources.
4.  Click `Create budget` to save.

Once enabled, spend tracking begins immediately — not retroactively. Existing users are not auto-assigned to any budget and will have unbudgeted spend until you configure explicit assignments.

### Assigning budgets to resources

Users apply budgets directly to resources (e.g., workbooks, bulk enrichment tables) upon creation of the resource. Any credits consumed by those resources are tracked against the assigned budget.

Once a user has access to budgets, all new workbooks they create must be assigned to a budget. If a user only has access to spend from one budget, that budget is assigned automatically. If multiple budgets are available, the user will be prompted to select one during workbook creation. If a user does not have access to budgets, new workbooks will be unbudgeted.

Anyone with edit access to a workbook can change its assigned budget to another budget they have access to. Budget changes only affect future usage — historical spend does not move between budgets.

Existing workbooks created before budgeting was enabled remain unbudgeted until manually assigned — only workbooks created after enabling require a budget assignment.

## Managing budgets

### Assigning budgets when inviting users

When inviting a new user to your workspace, admins can configure budget access directly in the invite flow — no need to update it separately after onboarding.

1.  Go to `Settings` → `Team` and click `Invite member`.
2.  Fill in the user's email and select their role (Admin, Editor, or Viewer).
3.  Optionally assign the user to one or more groups. Budget access pre-fills based on group selection — any budgets associated with those groups are automatically included.
4.  Optionally, grant the user access to additional budgets.
5.  Send the invite.

### Bulk-assigning budgets to existing workbooks

To assign a budget to multiple workbooks at once, use the bulk assignment tool on the homepage. Select multiple workbooks, then choose **Assign budget** from the action menu. This is especially useful when first enabling credit budgeting and you need to assign existing unbudgeted workbooks.

### Viewing budget usage

Go to `Settings` → `Budgets` to see your budgets. What you see depends on your role:

-   **Admins** can see all budgets in the workspace and update budget names, limits, and access settings. A workspace-level summary at the top shows total purchased credits and remaining credits.
-   **Editors and Viewers** see only the budgets they have access to, including each budget's name, limit, remaining balance, and assigned users and groups. Editors and Viewers cannot modify budgets.

You can also filter workbooks by budget from the homepage using the budget filter. The budgets usage widget in the top bar shows a progress bar for each budget you have access to.

### Editing a budget

Admins can select "…" on any budget row and select edit to change its name, limit, or access assignments. Changes take effect immediately for all future runs.

### Resetting a budget's usage

Admins can restore a budget back to its full limit by clicking "edit" and then "reset usage." Resetting is disabled if there has been no spend against the budget. Budget history is retained indefinitely; contact your Growth Strategist to access historical data.

### Deleting a budget

Budgets with active workbook assignments cannot be deleted. Those workbooks must first be reassigned to another budget.

## Credit spend by resource

Credit budgets apply differently depending on where spend originates.

### Workbooks

Workbooks are the primary unit of budget assignment. When a workbook runs enrichments or signals, credits are charged to the workbook's assigned budget. If a workbook calls a Function or Claygent, credits still charge to the workbook's budget.

### Audiences

Audiences uses a single budget for all signal runs and bulk enrichments.

-   By default, Audiences will not have a budget until an admin explicitly sets one.
-   Only admins can configure the Audiences budget. To set or update the Audiences budget, go to `Settings` → `Budgets` and select a budget under "Audiences budget."
-   Clay validates that the Audiences budget has sufficient credits before starting any enrichment job. If the budget is depleted, enrichment jobs are blocked until an admin resets or increases the limit.

**Note:** Per-signal and per-enrichment credit limits within Audiences are separate from the Audiences budget — those are resource-level controls similar to workbook credit spend limits.

### MCP users

When initially setting up MCP usage with Clay, users are prompted to select a budget from the list they have access to.

### Inbox purchases

When purchasing inboxes for Campaigns, users select which budget to charge at the time of purchase. The selected budget is debited for the cost of the inbox.

### Functions and Claygents

When editing Functions and Claygents, users can attribute test spend to a budget. However, when Functions and Claygents are used in workbooks, spend is attributed to the calling workbook's budget.

## Important to know

-   **Budgets are spending caps, not reserved credits.** The sum of all budget limits can exceed your total workspace credits. You can define limits without needing to divide your full credit pool upfront.
-   **When a budget reaches its limit, credit-consuming actions are blocked.** Workbooks remain editable, but enrichment runs cannot start until either the budget is reset or the limit is increased, or a new budget is assigned to the workbook.
-   **Budgets do not reset automatically.** Budget balances continue counting down until an admin manually resets the remaining balance or changes the limit.
-   **Resources without a budget.** If a workbook isn't assigned to a budget, any credits it uses are charged directly to the workspace credit balance.
-   **Credit budgets track Data Credit spend only** — they do not apply to action credits.

## FAQs

**What happens when a budget's credit limit is reached?**

All credit-consuming processes for workbooks assigned to that budget stop. Users see an error indicating the limit has been reached, and enrichment runs cannot start until an admin resets the budget or increases the limit. Workbooks remain fully editable — only execution is blocked. Alternatively, you can reassign the workbook to a different budget with remaining credits.

**What happens if a run is cancelled mid-execution?**

Credits consumed up to the point of cancellation are charged and not refunded. Partial results are preserved where applicable.

**What happens if I add more credits to my workspace?**

Budget limits don't automatically change when credits are added. Admins can manually adjust limits as needed.

**Can an editor reassign a workbook to a different budget?**

Yes — anyone with edit access to a workbook can reassign its budget, as long as they have access to the target budget. Changes apply to future runs only.

**What happens if a user loses access to a budget after their workbook is already assigned to it?**

The workbook continues running from its assigned budget. Admins or editors with workbook access can reassign it to a different budget if needed.

**Can I set time-based budgets that reset monthly?**

No — budgets are persistent spending limits and don't reset automatically. Admins can manually reset a budget to restore its full balance at any time.

**How are budgets different from workbook credit spend limits?**

Workbook credit spend limits cap a single workbook's spend. Credit budgets are shared pools that span multiple workbooks and users — useful for team- or department-level allocation. If a workbook has both a credit spend limit and an assigned budget, credits count against both independently.

**What happens to existing workbooks when I first enable credit budgeting?**

Existing workbooks are not automatically assigned to any budget. Their credit usage will be unbudgeted until you manually assign them to a budget.

**What if a user is in multiple groups that each have different budget access?**

They'll have access to all budgets granted to any of their groups. When creating a new workbook, they'll be prompted to select which budget to use if they have access to more than one.

**Whose budget gets charged when a workbook uses a Function or Claygent?**

The calling workbook's budget is charged. When a workbook runs a Function, all credit spend from that execution is tracked against the workbook's assigned budget, even if the Function was created by a different user or team.
