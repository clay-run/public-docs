---
title: Credit spend limits FAQ
description: Answering questions about the credit spend limits feature.
last_synced: 2026-04-26T01:39:48.764Z
---

# Credit spend limits FAQ

Answering questions about the credit spend limits feature.

**Credit spend limits** let workspace admins control credit usage by setting spending caps on workbooks and tables. This helps teams manage budgets, prevent overspending, and allocate resources across projects and users.

**Note:** This feature is only available for Enterprise Plan.

## Who can set and manage credit limits?

**Who can create and modify credit spend limits?**

Only workspace admins can create and modify credit spend limits. While Admins and Editors can both create workbooks and tables, only Admins can control the spending limits applied to them.

**Can Editors set limits on workbooks they create?**

No. To maintain clear governance, only Admins can set credit limits. If an Editor creates a workbook and no default limits exist, the workbook will operate without spending restrictions until an Admin applies one.

**How do limits apply to Viewers?**

Since Viewers can't create workbooks, an Admin must create one on their behalf and set a spending limit for their use.

## What can have credit limits?

**What resources can have credit limits applied?**

You can apply credit limits to:

-   Workbooks (primary level)
-   Standard tables
-   Signal tables
-   Campaigns

All of these exist within workbooks, making workbook-level limits the primary control mechanism.

**What about legacy tables created outside of workbooks?**

Credit limits aren't available for legacy tables created before the workbook architecture. To set a limit for a legacy table, move it into a workbook first.

## How do credit limits work?

**Can Admins set default limits for all workbooks?**

Yes. Admins can set a workspace default limit so that every new workbook created will automatically have that limit upon creation. You can change or update this default at any time.

To set a default limit:

1.  Go to `Settings` → `Usage` → `Workbook limits` tab.
2.  Click `Manage Default Limit`.
3.  Set your desired default credit limit.

Previously, admins had to manually set the limit for each individual workbook. With default limits, all new workbooks automatically inherit the workspace default limit, streamlining credit management across your workspace.

**Can limits be increased or decreased after they're set?**

Yes. Admins can adjust limits up or down at any time for both workbooks and legacy tables.

**How long does a credit limit last?**

Limits are designed with a monthly cadence in mind, aligning with how most enterprise customers plan their budgets and credit usage.

**Does past credit usage count towards the credit limit?**

No — credit limits only apply to usage that occurs after the limit has been set. Any credits spent before the limit was configured will not count towards it.

**What happens when a billing cycle resets?**

Limits don't automatically reset or reapply when billing cycles reset. Admins maintain full control and can modify limits as needed.

**Are limits set as a percentage or fixed number of credits?**

Limits are set as a fixed number of credits rather than a percentage. This provides clearer control since credits don't reset, and all new workbooks are automatically assigned predetermined limits by the Admin.

**Do function calls count against a workbook's credit limit?**

Yes. When a workbook calls a function that consumes credits, those credits are attributed to the calling workbook and count against its credit limit. If the workbook reaches its credit limit, the function will be blocked from running.

## What happens when limits are reached?

**What happens when a workbook hits its credit limit?**

When a limit is reached:

-   All credit-consuming processes stop
-   Cells that tried to run show a **Workbook credit limit reached** error
-   Any recurring spends are canceled
-   Users are notified of canceled processes

**To resolve it**, workspace admins on Enterprise plans will see a **Manage credit limit** button directly on the error and an **Increase spend limit** button on a banner at the top of any table in the workbook. Both open the credit limit editor, where you can raise the cap or remove it entirely by toggling off **Enable workbook credit limit**. Non-admins will see the error message with a prompt to contact their workspace admin.

**Can users request a limit increase?**

Workspace admins on Enterprise plans can raise a limit directly in Clay — either by clicking **Manage credit limit** on the **Workbook credit limit reached** error or from the workbook's settings panel. Non-admin users do not have an in-product way to request an increase; they should reach out to their workspace admin directly.

**What happens if an Admin lowers a limit below what's already been spent?**

If a workbook originally had a 200-credit limit with 100 credits spent, and an Admin lowers the limit to 80 credits, users will immediately see a message that the limit has been reached. Any recurring spends will be canceled, and users will be notified.

**What happens if a source is running when the limit is hit?**

It depends on whether the source itself consumes credits:

-   **Credit-consuming sources** (e.g., list builders like Find People or Find Companies): the source stops running and will not resume until the limit is increased or credits are replenished.
-   **Standard webhook sources**: data ingestion continues uninterrupted — incoming rows still appear in your table even when the limit is reached. Only the downstream enrichment columns that consume credits will stop processing those rows.

So if you use a webhook to bring data into Clay (for example, from RB2B or another integration), new rows will keep flowing in even after the credit limit is hit. The enrichment steps on those rows won't run until credits are available again.

## Notifications and communication

**Who receives notifications when a workbook approaches or hits its limit?**

Notifications are sent to:

-   Workspace Admins (who can modify limits)
-   Any users explicitly added to that specific workbook

Notifications will be delivered via both email and in-product UI across various surfaces.

**Is there an automated alert for my workspace's monthly Data Credit balance?**

No. The notifications above are for workbook-level credit spend limits only — they fire when a specific workbook reaches its configured cap. There is currently no automated alert when your workspace's overall monthly Data Credit allotment is running low or is exhausted.

To manually monitor your monthly credit balance, go to **Settings → Usage**. The Usage Dashboard shows your remaining Data Credits and your current billing period end date. For a detailed breakdown of credit consumption, see [Credit usage](/docs/credit-usage).

## Credit Budgets (open beta)

**What's the difference between credit spend limits and credit budgets?**

**Credit spend limits** (covered in this guide) set workbook-level spending caps — admins define a maximum credit amount for each workbook, and all tables and campaigns within it share that cap.

**Credit Budgets** is a related but separate feature currently in open beta for Enterprise customers. It lets admins create named budget pools, assign users or user groups to each budget, and associate workbooks, tables, and campaigns with a specific budget — providing more granular, shared credit governance as your organization scales Clay across multiple teams. To join the Credit Budgets open beta, contact your Growth Strategist.
