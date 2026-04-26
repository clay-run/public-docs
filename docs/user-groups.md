---
title: User groups
source_url: https://university.clay.com/docs/user-groups
description: User groups let you share Clay workbooks and connected accounts
  with multiple members at once.
last_synced: 2026-04-26T01:40:51.931Z
upstream_hash: e2e519cc72232ad1b3ae3115f1598114a5fa9d1cb275df7564ec487ce6943f21
---

# User groups

User groups let you share Clay workbooks and connected accounts with multiple members at once.

**Note:** This feature is currently in beta for Enterprise customers.

User groups let you share Clay workbooks and connected accounts with multiple members at once. Instead of adding people one by one to connections and tables, you can create groups and grant access to the entire group at once.

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

### Deleting a group

To delete a group:

1.  Navigate to `Settings` → `Teams` → `Groups` tab and click the group you want to delete.
2.  Click `Delete group`.
3.  Review the confirmation modal to acknowledge that this group will be permanently removed from all resources, revoking access for all members.
4.  Click `Delete group` to confirm.

Once deleted, the group loses any previous access to associated resources. This action cannot be undone.

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

Not yet. User groups in Clay are managed manually within the workspace. There is no SCIM or SSO sync with external identity providers at this time.

**Can groups be nested inside other groups?**

No. Groups are flat lists with no hierarchy or nesting.

**Can I bulk-create groups from a CSV?**

Not currently. Groups must be created individually through `Settings` → `Teams` → `Groups` tab.
