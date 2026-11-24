---
title: Best practices before a member leaves your workspace
description: Audit admin access, billing, connections, automated work, and sequencer senders before you remove a departing member from your workspace.
last_synced: 2026-11-09T19:36:18.134Z
---

# Best practices before a member leaves your workspace

Audit admin access, billing, connections, automated work, and sequencer senders before you remove a member from your workspace.

Removing a departing teammate's account is the last step of offboarding, not the first. A member on their way out may hold the only `Admin` role, own tables and workbooks the rest of your team relies on, or have personal credentials attached to columns and workflows your team uses every day.

Work through the audit below before you remove them from your workspace.

**Note:** When you remove a member, the tables and workbooks they owned are not deleted — they transfer automatically to the admin whose admin role was granted earliest, and so do any user groups the member owned. Ownership may not land with the person who actually picks up their work, so reassign anything important before you remove them.

## Reassign the admin role

Clay blocks any removal that would leave your workspace without an admin, so start here.

1.  Go to `Settings` and select `Team` from the left-hand menu.
2.  On the `Members` tab, find the departing member and check the `Role` column.
3.  If their role is `Sales Rep` or `Editor`, no action is needed.
4.  If their role is `Admin` and at least one other `Admin` remains, no action is needed.
5.  If they are your only `Admin`, promote another member to `Admin` before you remove them.

The doc on [roles and permissions](https://university.clay.com/docs/roles-and-permissions) covers what each role can do. If no one else is in a position to take the role, contact Support through the help icon or at support@clay.com.

## Move billing off the departing member

Confirm the billing details on file don't belong to the person leaving.

1.  Go to `Settings` and select `Plan & billing`.
2.  Under `Payment method`, review the name, email, address, and card on file.
3.  If any of it belongs to the departing member, select `Edit`, then `Edit billing info...` or `Edit payment method...`.

## Replace personal connection credentials

Columns and workflows that run on someone's personal account stop working once that account is switched off at the provider. Swap the credentials rather than rebuilding the work that depends on them.

1.  Go to `Settings` and select `Connections`.
2.  Select `All` next to `Account type`, then choose `User-added` to set aside Clay-provided connections.
3.  Check the `Added by` column for the departing member. To narrow the list to just their connections, open `Filters` and turn on `Added by`.
4.  For each of their connections, open the three-dot menu and select `Reconnect`, then sign in with an account that will stay with your team.

Before you change a connection, select the icon in its `Resources` column to see everywhere it is used. From there you can sort by resource type and jump straight to each one.

A shared integration account isn't tied to one person, so it's worth considering for the connections your team depends on most. The doc on [managing integration accounts](https://university.clay.com/docs/managing-integration-accounts) covers the difference between personal and shared accounts.

## Review the automated work they set up

List the automated work set up under the departing member's account, so someone still on the team can pick it up.

-   Scheduled sources in `Workflows` or on a table
-   Signals they set up to monitor on an ongoing basis
-   Tables with `Auto-run` turned on

## Reassign sequencer senders

Review the email accounts tied to the departing member so sender names and replies reach someone still on your team.

1.  In the sidebar, go to `Sequencer` and open the `Email accounts` tab.
2.  Find the accounts belonging to the departing member.
3.  For an account purchased through Clay, open the three-dot menu and select `Update sender variables` to change the name recipients see, then `Assign to user` to route replies to someone still on the team. Updating the sender variables is the better move here than deleting the account or its domain.
4.  For an account you connected yourself, open the three-dot menu and select `Delete account` if the address is going away with the member.

## FAQs

### What happens if I try to remove my only admin?

Clay rejects the removal and tells you it can't remove the last admin from the workspace. Workspaces that provision members through a directory sync are the exception — deprovisioning there can remove a directory-managed admin even when no other admin would remain.

### Why don't I see `Remove member` for someone on my team?

Members provisioned through SCIM directory sync can't be removed in Clay directly. In `Settings` > `Team`, the `…` menu for a SCIM-managed member shows `View user access` but no `Remove member` option. When your workspace has an active directory sync, the `Managed via` column on the Team page shows `SCIM` for these members and `Clay` for members you can remove in Clay. Remove SCIM-managed members in your identity provider instead and let the sync deprovision the account.
