---
title: User groups
description: User groups let you share Clay workbooks, connected accounts, and
  credit budgets with multiple members at once, and can sync from your identity
  provider through SCIM provisioning.
last_synced: 2026-04-26T01:40:51.931Z
---

# User groups

User groups let you share Clay workbooks, connected accounts, and credit budgets with multiple members at once.

**Note:** This feature is currently in beta for Enterprise customers.

User groups let you share Clay workbooks, connected accounts, and credit budgets with multiple members at once. Instead of adding people one by one to connections and tables, you can create groups and grant access to the entire group at once.

Only admins can create and manage groups, but all workspace members can view them.

## Creating a user group

To create a user group:

1.  Go to `Settings` → `Teams` → `Groups` tab.
2.  Click `Create group`.
3.  In the modal, enter a `Group name`. Names must be unique across your workspace and cannot exceed 50 characters.
4.  Optionally, use the `Add members` field to search for and select workspace members. You can leave this empty and add members later — groups do not need members to be saved.
5.  Click `Create group`.

**Note:** Only admins can create user groups. Editors and viewers can view groups and their members but cannot create or edit them. Learn more about [roles and permissions](https://www.clay.com/university/guide/roles-and-permissions).

## Managing user groups

### Viewing groups

All workspace members — admins, editors, and viewers — can view the group directory at `Settings` → `Teams` → `Groups` tab. You can see each group's name and member count, and click into any group to see its full membership list. Use the search bar to filter groups by name.

You can also view groups from the member perspective by navigating to `Settings` → `Members`. From this view, you can see which groups each member belongs to. Clicking on a group name will take you to that group's detail page.

### Editing a group

To edit a group's name or members, navigate to `Settings` → `Teams` → `Groups` tab and click the group you want to edit. From the group detail page, admins can:

-   Update the group name or description.
-   Add new members by searching for workspace users in the `Add members` field.
-   Remove existing members by clicking the remove icon next to their name.

Changes take effect immediately. When you add someone to a group, they automatically gain access to all resources the group has been granted. When you remove someone, they immediately lose that access.

For SCIM-managed user groups, admins can only edit the description in Clay. See [SCIM-managed user groups](#scim-managed-user-groups).

### Deleting a group

To delete a group:

1.  Navigate to `Settings` → `Teams` → `Groups` tab and click the group you want to delete.
2.  Click `Delete group`.
3.  Review the confirmation modal to acknowledge that this group will be permanently removed from all resources, revoking access for all members.
4.  Click `Delete group` to confirm.

Once deleted, the group loses any previous access to associated resources. This action cannot be undone.

`Delete group` isn't available for SCIM-managed user groups. To remove one, delete the group in your identity provider.

## Adding a group to a resource

Only connection owners and admins can add a group to a resource. To do this, navigate to the resource's sharing or permissions settings and select the group you want to grant access to. When adding a group, you will see the number of members in that group.

To add a group to a resource, you'll do this from within the resource itself, not from the `Groups` page.

For example, to grant a group access to a connection:

1.  Navigate to `Settings` → `Connections`
2.  Find and edit the connection you want to manage
3.  Select `Specific users and groups`
4.  Add the user group (e.g., Engineering, RevOps) to grant access to all members of that group
5.  Click `Save`

When you add a user to a group, they automatically inherit access to all connections and resources that group has been granted access to.

## SCIM-managed user groups

If your workspace uses [SCIM provisioning](./scim-provisioning.md), groups you push from your identity provider (IdP), such as Okta or Azure AD, sync to Clay as SCIM-managed user groups. Group names and membership stay up to date automatically, so IT teams can manage these user groups in the IdP instead of creating and maintaining them by hand in Clay. SCIM provisioning and user groups are available on Enterprise plans.

### What syncs from your identity provider

This table shows what each group change in your identity provider does to the SCIM-managed user group in Clay.

| In your IdP | In Clay |
| --- | --- |
| Push a group | Clay creates a user group with the same name. |
| Rename a group | The user group's name updates to match. |
| Add a user to a group | The user is added to the user group and inherits access to every workbook, connection, and credit budget the group has been granted. |
| Remove a user from a group | The user is removed from the user group and loses the access granted through it. |
| Delete a group | The user group is deleted from Clay, and its members lose the access granted through it. |

A user is only added to a SCIM-managed user group once they're also assigned to Clay through SCIM. Users with a pending invite can be group members too.

For example, share a credit budget with a `Sales reps` group pushed from your IdP. When IT adds someone to that group in the IdP, they automatically get access to that budget in Clay.

### Identifying and editing SCIM-managed user groups

In `Settings` → `Teams` → `Groups` tab, SCIM-managed user groups show a `SCIM` badge next to the group name and list your identity provider as their source.

When an admin opens a SCIM-managed user group in Clay:

-   The group name and members are read-only, with the message "This group syncs from" followed by your identity provider's name. Change them in your IdP instead.
-   The description can be edited, up to 1,000 characters.
-   `Delete group` isn't available. Select `Manage SCIM` to manage the connection instead.

You share SCIM-managed user groups with workbooks, connections, and credit budgets the same way as any other user group.

## FAQs

### **Who can create and manage user groups?**

Only admins can create, edit, and delete groups. All workspace members can view groups and see their members, but editors and viewers cannot add or remove people from a group.

**Can a user belong to multiple groups?**

Yes. Users can belong to any number of groups at the same time. If multiple groups grant access to the same resource, the permissions simply overlap — there are no conflicts.

**What happens when someone is added to a group?**

They immediately gain access to all resources the group has been granted. No additional steps are needed.

**What happens when someone is removed from a group?**

Their access to all resources granted through that group is revoked immediately.

**What happens when a user is removed from the workspace?**

They are automatically removed from all groups and their access is revoked.

**Can non-admins see what resources a group has access to?**

Admins can see which connections a given group has access to use. However, editors and viewers can see group names and member lists, but cannot see which resources (like connections) a group has access to.

**Are groups synced from Okta, Azure AD, or other identity providers?**

Yes, through SCIM provisioning (available on Enterprise plans). Groups pushed from Okta, Azure AD, or another identity provider sync to Clay as SCIM-managed user groups, with names and membership kept up to date automatically. See [SCIM-managed user groups](#scim-managed-user-groups). Groups you create in Clay are still managed manually within the workspace. This is separate from workspace SSO authentication: Clay does support SSO login via WorkOS for Enterprise customers (and as a paid add-on for annual Pro and Growth plans). See [Single Sign-On (SSO)](./single-sign-on.md) for setup details.

**Can groups be nested inside other groups?**

No. Groups are flat lists with no hierarchy or nesting.

**Can I bulk-create groups from a CSV?**

Not currently. Groups must be created individually through `Settings` → `Teams` → `Groups` tab.
