---
title: Credit spend limits FAQ
source_url: https://university.clay.com/docs/credit-spend-limits-faq
description: Answering questions about the credit spend limits feature.
last_synced: 2026-04-26T01:39:48.764Z
upstream_hash: 64d96124ab54a60f6c196d9dc236c18dd3fb4c2d59dcdd667555dcbb8f2bed03
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

1.  Go to `Settings` → `Credit usage` → `Workbook limits` tab.
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
-   Users see a message that the limit has been reached
-   Any recurring spends are canceled
-   Users are notified of canceled processes

**Can users request a limit increase?**

Users can request higher limits from their Admin outside of Clay. Since Admins can modify limits directly, there's no in-product flow for requesting increases. Team members should reach out to their Admin directly.

**What happens if an Admin lowers a limit below what's already been spent?**

If a workbook originally had a 200-credit limit with 100 credits spent, and an Admin lowers the limit to 80 credits, users will immediately see a message that the limit has been reached. Any recurring spends will be canceled, and users will be notified.

**What happens if a source is running when the limit is hit?**

The process will stop, similar to how Clay handles other credit exhaustion scenarios. Future enhancements may include options to pause and resume later.

## Notifications and communication

**Who receives notifications when a workbook approaches or hits its limit?**

Notifications are sent to:

-   Workspace Admins (who can modify limits)
-   Any users explicitly added to that specific workbook

Notifications will be delivered via both email and in-product UI across various surfaces.
