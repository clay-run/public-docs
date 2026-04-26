---
title: OAuth optional scopes
source_url: https://university.clay.com/docs/oauth-optional-scopes
last_synced: 2026-04-26T01:40:25.716Z
upstream_hash: 1e49fe9f634d5766dfda204960f5fc4014472e521d5493e5b82aa4e698435d47
---

# OAuth optional scopes

Control exactly which permissions you grant to integrations.

When connecting certain OAuth-based integrations (like HubSpot and Outreach), Clay allows you to control exactly which permissions you grant to the integration. This feature follows the **principle of least privilege**—you only enable the permissions your workflows actually need.

### Why use optional scopes?

**Security and compliance**: Limit data access to meet organizational security policies. Only grant the permissions your team truly needs.

**Read-only access**: Disable write permissions if you only need to pull data without modifying records.

**Advanced features on-demand**: Enable specialized permissions (like HubSpot sequence automation) only when needed.

## Scope types

### Required scopes

These permissions are essential for the integration to function. They **cannot be disabled** and are always requested when you connect an account. Required scopes typically include read permissions for core functionality.

**Visual indicator**: Lock icon 🔒.

**Example:** For HubSpot, required scopes include viewing contacts, companies, and leads—permissions needed for basic CRM operations.

### Optional (enabled by default)

These permissions are requested by default but **can be disabled** if you don't need them. They're pre-selected when you connect an account, but you can uncheck them if you prefer not to grant those permissions.

**Visual indicator**: Checked checkbox ☑️.

**Example:** Write permissions for contacts and companies are optional by default in HubSpot. If you only want to read data from HubSpot (not write to it), you can disable these scopes.

### Optional (disabled by default)

These permissions are available but **not requested by default**. You must explicitly enable them if you want to grant those permissions.

**Visual indicator**: Unchecked checkbox ☐.

**Example:** Sequence automation permissions in HubSpot are disabled by default. Enable them only if you need Clay to enroll contacts in HubSpot sequences.

## How to use optional scopes

### When connecting a new account

1.  Click `Add account` for your desired integration.
2.  In the connection modal, you'll see a `Scopes` section (if optional scopes are available for that integration).
3.  Review the scopes:
    -   **Required scopes** are shown with a lock icon and cannot be changed.
    -   **Optional scopes** have checkboxes you can toggle on or off.
4.  Select the scopes you need and click `Sign in with [Provider]`.
5.  Complete the OAuth flow in the provider's authentication window.

### When reconnecting an existing account

When you reconnect an account (e.g., to refresh credentials or update permissions):

1.  Go to `Settings` → `Connected accounts`.
2.  Find the account and click `Reconnect` from the menu.
3.  Your previously selected scopes will be preserved and pre-selected.
4.  Adjust the scopes as needed.
5.  Complete the reconnection flow.

## Best practices

### Follow the principle of least privilege

Only enable the scopes you actually need. This improves security by limiting what Clay can access in your connected accounts.

### Start with defaults

The default scope selections are designed to cover common use cases:

-   **Required scopes** cover essential read operations.
-   **Optional (enabled by default)** cover typical read/write workflows.
-   **Optional (disabled by default)** are for advanced features.

### Adjust as needed

If an action fails due to insufficient permissions, you can reconnect the account and enable additional scopes.

## Currently supported integrations

Optional scopes are available for the following OAuth integrations:

-   [**HubSpot**](https://www.clay.com/university/guide/hubspot-integration-overview) — Customer relationship management (CRM) platform for sales, marketing, and customer service.
-   [**Outreach**](https://www.clay.com/university/guide/outreach-integration-overview) — Sales engagement platform for automating and optimizing outreach campaigns.

## Troubleshooting

### "Insufficient permissions" error

If you see this error when running an action:

1.  Go to `Settings` → `Connected accounts`.
2.  Find the relevant account and click `Reconnect`.
3.  Enable the required scope.
4.  Complete the reconnection flow.
5.  Retry the action.

### Scope not appearing in the list

If you're looking for a specific scope that isn't shown:

-   It may be included in the required scopes (always enabled).
-   The provider may not support that scope through their OAuth API.
-   Contact Clay support if you need a scope that isn't available.

### Changes not taking effect

After updating scopes through reconnection:

1.  Ensure the OAuth flow completed successfully.
2.  Try running your action again.
3.  If issues persist, disconnect and reconnect the account completely.

## FAQs

### **Can I change scopes after connecting an account?**

Yes. Use the `Reconnect` option in `Settings` → `Connected accounts` to adjust your scope selections at any time.

### **Will my previously selected scopes be remembered?**

Yes. When you reconnect an account, Clay will pre-select the scopes you previously enabled.

### **Do optional scopes affect my existing connections?**

No. Optional scopes only affect new connections or when you explicitly reconnect an existing account.

### **What happens if I disable a scope I'm currently using?**

Enrichments or actions that require that permission will fail with an "insufficient permissions" error. You can re-enable the scope by reconnecting the account.

### **Are optional scopes available for all integrations?**

Currently available for HubSpot and Outreach, with more integrations being added over time.

### **Can different team members connect with different scopes?**

Yes. Each connected account can have different scope selections based on the team member's needs.
