---
title: Credit budgets
description: Create and manage named credit budgets to organize spend, prevent overspend, and govern how Clay credits flow across your organization. Available in open beta for Enterprise plan customers.
last_synced: 2026-06-25T00:00:00.000Z
---

# Credit budgets

**Note:** Credit budgets are currently in open beta for Enterprise plan customers.

**Credit budgets** give workspace admins a way to organize credit spend across teams and workflows — think company cards for GTM infrastructure. Instead of a single workspace-wide credit pool with no visibility, admins create named budgets (for example, "Sales Team" or "Marketing Ops"), assign workbooks and other resources to each budget, and set credit limits per budget. This helps prevent overspend, makes it easy to attribute costs to the right team or project, and gives enterprises the governance controls they need to expand Clay usage with confidence.

Credit budgets appear at `Settings` → `Budgets`. Only workspace admins can create and manage budgets.

## How credit budgets work

A **budget** is a named credit pool with:

-   A **credit limit** — the maximum number of credits the budget can spend. Limits do not auto-reset on a billing cycle.
-   A **current balance** — how many credits remain (limit minus spend so far).
-   An **access rule** — whether all workspace members can draw from the budget, or only members explicitly granted access.
-   An optional list of **users** or **user groups** with explicit access.

When a workbook (or other resource) is assigned to a budget, all credit-consuming actions in that resource count against the budget's balance. If a budget runs out of credits, processing in assigned resources stops until an admin increases the limit or resets the spend.

**Budgets vs. workbook credit spend limits:** Credit budgets are shared pools that span multiple workbooks and users. Workbook credit spend limits cap a single workbook's spend. These features are complementary — you can use spend limits to cap individual workbooks while also assigning them to a budget for team-level cost attribution. See [Credit spend limits FAQ](/docs/credit-spend-limits-faq).

## Creating a budget

1.  Go to `Settings` → `Budgets`.
2.  Click **Create**.
3.  Enter a budget **name** and set a **credit limit**.
4.  Choose a **default access** setting:
    -   **All workspace members** — any member can assign their workbooks to this budget.
    -   **Only specific users or groups** — only members you explicitly add can use the budget.
5.  Optionally, add specific **users** or **user groups** who should have access.
6.  Click **Create budget** to save.

Once a budget is created, spend tracking begins immediately — not retroactively. Existing workbooks created before budgeting was enabled remain unbudgeted until manually assigned.

## Assigning resources to a budget

Users assign a budget when creating a new workbook. Credits the workbook consumes are tracked against that budget.

-   If a user has access to only one budget, it is assigned automatically to all new workbooks they create.
-   If a user has access to multiple budgets, they are prompted to select one during workbook creation.
-   If a user has no budget access, new workbooks are unbudgeted.

Anyone with edit access to a workbook can reassign it to a different budget they have access to. Budget changes apply to future usage only — historical spend does not move between budgets.

**From a workbook:**

1.  Open the workbook overview panel (click the workbook name).
2.  Find the **Budget** section and select the budget to assign.

**Bulk assignment from the homepage:**

1.  On the workspace homepage, select one or more workbooks.
2.  Click the **Manage** button that appears in the action bar.
3.  Choose **Assign budget** and select the target budget.

**Filtering by budget on the homepage:**

Use the **Budget** filter on the workspace homepage to quickly see all workbooks assigned to a specific budget, making it easy to audit spend allocation across your org.

## Assigning budgets when inviting users

When inviting a new team member, admins can configure budget access in the invite flow:

1.  Go to `Settings` → `Team` and click `Invite member`.
2.  Fill in the user's email and select their role (Admin, Editor, or Viewer).
3.  Optionally assign the user to one or more groups — budget access pre-fills based on group selection.
4.  Optionally grant the user access to additional budgets.
5.  Send the invite.

## Managing budgets

### Viewing budget usage

Go to `Settings` → `Budgets` to see all budgets in your workspace. What you see depends on your role:

-   **Admins** can see all budgets and update their names, limits, and access settings. A workspace-level summary at the top shows total purchased credits and remaining credits.
-   **Editors and Viewers** see only the budgets they have access to, including each budget's name, limit, remaining balance, and assigned users and groups. Editors and Viewers cannot modify budgets.

A budgets usage widget in the top bar shows a progress bar for each budget you have access to.

### Editing a budget

Admins can click `…` on any budget row and select `Edit` to change its name, limit, or access assignments. Changes take effect immediately for all future runs.

### Email alerts for budget usage

Clay sends email alerts to workspace admins when a budget reaches specific usage thresholds:

-   **75%** of the credit limit used — early warning.
-   **90%** of the credit limit used — approaching the limit.
-   **100%** of the credit limit used — budget exhausted, processing in assigned resources has stopped.

Alerts fire once per threshold crossing. They reset when an admin increases the credit limit or resets the budget's spend.

### Resetting a budget's usage

Admins can restore a budget to its full limit by clicking `Edit` and then `Reset usage`. Resetting is disabled if there has been no spend against the budget. Budget history is retained indefinitely.

### Deleting a budget

Budgets with active workbook assignments cannot be deleted. Reassign those workbooks to another budget first.

## How budgets apply to different resources

### Audiences

Audiences uses a single budget for all signal runs and bulk enrichments.

-   By default, Audiences has no budget assigned until an admin sets one.
-   Only admins can configure the Audiences budget. Go to `Settings` → `Budgets` and select a budget under **Audiences budget**.
-   Clay validates that the Audiences budget has sufficient credits before starting any enrichment job. If the budget is depleted, enrichment jobs are blocked until an admin resets or increases the limit.

**Note:** Per-signal and per-enrichment credit limits within Audiences are separate from the Audiences budget — those are resource-level controls similar to workbook credit spend limits.

### MCP users

When setting up MCP access, users are prompted to select a budget from the list they have access to. MCP usage is then charged against that budget.

### Inbox purchases (Campaigns)

When purchasing inboxes for Campaigns, users select which budget to charge at the time of purchase.

### Functions and Claygents

When editing Functions or Claygents directly, users can attribute test spend to a budget. When Functions or Claygents are called from a workbook, spend is attributed to the calling workbook's budget.

## Important to remember

-   **Budgets are spending caps, not reserved credits.** The sum of all budget limits can exceed your total workspace credits — you can define limits without dividing your full credit pool upfront.
-   **Executions stop when a budget limit is reached.** Workbooks remain editable, but enrichment runs cannot start until the budget is reset, the limit is increased, or the workbook is reassigned to a budget with remaining credits.
-   **Budgets do not reset automatically.** Budget balances count down until an admin manually resets them or changes the limit.
-   **Unbudgeted resources.** If a workbook has no assigned budget, credits it uses are charged directly to the workspace credit balance.

## Credit budgets vs. credit spend limits

Clay has two distinct credit governance features for Enterprise workspaces:

| Feature | What it does | Where to find it |
|---|---|---|
| **Credit budgets** | Named credit pools — assign workbooks to a budget and track spend across teams. | `Settings` → `Budgets` |
| **Credit spend limits** | Per-workbook credit caps — set a maximum spend for a single workbook or table. | `Settings` → `Usage` → `Workbook limits` |

If a workbook has both a credit spend limit and an assigned budget, credits count against both independently.

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
