---
title: Credit budgets
description: Create and manage named credit budgets to organize spend, set limits, and govern credit usage across your enterprise workspace.
last_synced: 2026-06-25T00:00:00.000Z
---

# Credit budgets

**Note:** Credit budgets are currently in open beta for Enterprise plan workspaces. Contact your Clay account team to enable this feature.

Credit budgets help workspace admins organize credit spend across teams and projects. Think of them like company cards for GTM workflows: you create a named budget, set a credit limit, assign workbooks to it, and control which team members can charge spend against it. Budgets give you visibility into where credits are going and prevent any one project from running over.

This is distinct from [workbook-level credit spend limits](/docs/credit-spend-limits-faq), which cap how many credits a single workbook can consume. Budgets are the higher-level organizational layer — a workbook is assigned to a budget, and its spend counts against that budget's limit.

## Access and permissions

Only workspace admins can create, edit, and delete budgets. Non-admin members can be granted access to use a budget (so their workbooks can charge spend against it), but they cannot manage budget settings.

To reach the Budgets page, go to **Settings → Budgets**.

## Create a budget

1. Go to **Settings → Budgets**.
2. Click **Create**.
3. Enter a name for the budget.
4. Set a **credit limit** — the maximum number of credits this budget can spend before further credit-consuming actions are blocked.
5. Set **default access**: choose whether all workspace members can charge spend to this budget, or whether only specific members and groups you add explicitly can use it.
6. Optionally add specific users or user groups who should have access.
7. Save the budget.

Budgets do not reset automatically. Admins can manually reset a budget's spend or adjust its limit at any time.

## Assign workbooks to a budget

Once a budget exists, you can assign workbooks (and the tables inside them) to it so their credit spend is tracked and counted against that budget's limit.

**Assign a single workbook:**

1. Open the workbook.
2. In the workbook settings panel, find the **Budget** field.
3. Select the budget you want to assign.

**Bulk-assign from the homepage:**

1. On the Clay homepage, select multiple workbooks using the checkboxes.
2. Click the actions menu (the `…` or resource-management button).
3. Choose **Assign budget** and select the target budget.

## Filter by budget on the homepage

When credit budgets are enabled, a **Budget** filter appears on the Clay homepage. Use it to view only the workbooks assigned to a particular budget — useful for auditing spend or checking which resources a team is using.

## Email alerts for budget usage

Clay sends email alerts to workspace admins as a budget's credit limit is consumed:

-   **75% of limit used** — early warning to review spend.
-   **90% of limit used** — approaching the cap.
-   **100% of limit used (limit reached)** — further credit-consuming actions on workbooks assigned to this budget are blocked until the limit is increased or the budget's spend is reset.

Alerts are sent once per threshold crossing. If an admin resets the budget's spend, the alert cycle restarts.

## Related

-   [Credit spend limits FAQ](/docs/credit-spend-limits-faq) — set per-workbook credit caps (a complementary control that operates at the workbook level rather than the budget level).
-   [Credit usage](/docs/credit-usage) — track and analyze credit consumption across your workspace.
-   [Roles and permissions](/docs/roles-and-permissions) — understand admin vs. editor access in Clay.
