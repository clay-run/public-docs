---
title: Account and workspace settings
source_url: https://university.clay.com/docs/workspace-administration-documentation
description: Manage account and workspace settings, integration accounts, and billing.
last_synced: 2026-04-26T01:40:56.525Z
upstream_hash: 537dcfe4ee76a84566688d5cf417288ffbf7ddbf2bcbb0cc750ef95629861714
---

# Account and workspace settings

Manage account and workspace settings, integration accounts, and billing.

# **Account settings**

Your account settings allow you to keep your personal data up to date and ensure your account remains secure. Below are the steps for updating key details like your profile picture, name, and password.

## **Update your profile picture**

To update your profile picture:

-   Go to `Settings` and select `Account` from the left-hand menu.
-   In the `Your details` tab under `Your profile`, click `Upload new picture` to upload an image or choose an icon.
    -   Please ensure the image is in png, jpg, jpeg, or gif format with a max size of 5MB.
-   Use the `Delete` button if you wish to remove your current profile picture.
-   Click `Save` to confirm your changes.

## **Update your name**

To update your account name:

-   Go to `Settings` and select `Account`.
-   Under the `Your details` tab, edit your name in the `Name` field.
-   Click `Save` to ensure your changes are updated.

## **Change your password**

To change your account password:

-   Visit your `Settings` and head to the `Account` section.
-   Open the `Security` tab under `Your profile`.
-   Click `Change password`. A magic link will be sent to your registered email address.
    -   _Note: This option is available only if you signed in using a password and not via an authentication service such as Google or SSO._
-   Follow the instructions in the email to securely update your password.

## **Clay API key access**

Your Clay API key enables Clay-specific integrations and external connections. To manage your API key:

-   Go to `Settings` >`Your profile` > `API key`.
-   Use the following options:
    -   `Copy` the key for application use.
    -   `Regenerate` the key if compromised.

## **Delete your account**

You can permanently delete your Clay account through your account settings. Before proceeding, please note:

**Requirements:**

-   You must be a **member** (not admin) of all your workspaces, OR
-   You must be the **only member** in your workspace

**To delete your account:**

-   Go to `Settings` and select `Account` from the left-hand menu.
-   Scroll to the `Account deletion` section at the bottom of the page.
-   Click the `Delete account` button.
-   Complete the email verification step to confirm your request.

**What happens when you delete your account:**

-   Your deletion request is processed and logged for audit purposes.
-   Your API keys are deleted.
-   Your account email is updated to a deleted variant.
-   For any workspaces affected by your account deletion, workspace admins will receive email notifications.
-   Your private app account and Stripe customer information are deleted to prevent unexpected charges.

**Important:** Account deletion is permanent and cannot be undone. While your data is marked for deletion and critical billing/authentication records are removed immediately, full data removal from our database may take additional time.

# **Workspace settings**

Workspace settings give you control over key aspects of your workspace, such as its name, profile picture, and billing email. These settings ensure your workspace is easily identifiable and that billing communications reach the correct contact. Below are the steps for updating key workspace details.

## **Workspace picture**

To update your workspace picture:

-   Navigate to `Settings` > `Workspace settings`.
-   Click `Upload new picture` to upload an image or choose an icon.
    -   Please ensure the image is in png, jpg, jpeg, or gif format with a max size of 5MB.
-   Use the `Delete` button if you wish to remove your current profile picture.
-   Click `Save` to apply your changes.

## **Workspace name**

To update your workspace name:

-   Go to `Settings` > `Workspace settings`.
-   Update the `Workspace name` field with your desired name.
    -   This name will be displayed across your workspace and should be accessible for team identification.
-   Click `Save` to confirm your changes.

## **Billing email**

To update your billing email:

-   In `Workspace settings`, edit the `Billing email` field to update the email address used for all billing-related communication.
-   Click `Save` to ensure the new email is recorded.

## **Delete your workspace**

You can permanently delete your Clay workspace through workspace settings. This action is permanent and cannot be undone.

**Requirements:**

-   The workspace must have **no pending invites**.
-   You must be the **only member** in the workspace.

**To delete your workspace:**

-   Navigate to `Settings` > `Workspace settings`.
-   Scroll to the `Delete workspace` section at the bottom of the page.
-   Click the `Delete workspace` button.
-   Complete the email verification step to confirm your request.

**What happens when you delete your workspace:**

-   Your deletion request is processed and logged for audit purposes.
-   The workspace owner is updated to prevent access.
-   Your private app account and Stripe customer information for the workspace are deleted to prevent unexpected charges.
-   Workspace admins receive email notifications about the deletion.

**Important:** Workspace deletion is permanent and cannot be undone. All workspace data, tables, and configurations will be permanently removed.

# **Managing team members**

## **Roles and permissions**

Clay offers three user roles with different permission levels to help manage your workspace effectively.

### **Admin**

**Admins** have full control over the workspace and can manage both resources and team membership.

**Capabilities:**

-   Manage all workspace settings and resources.
-   Invite and remove team members.
-   Assign and update user roles.
-   Access billing and workspace configuration.

### **Editor**

**Editors** are standard users focused on building and working within workspace resources.

**Capabilities:**

-   Create and edit tables, workflows, and integrations.
-   Update records in tables.
-   Delete tables they own.
-   Add or modify columns and data sources.

**Editors cannot:**

-   Add, remove, or change team members' roles.
-   Modify billing settings or purchase credits.

### **Viewer**

**Viewers** have read-only access to workspace content.

**Note:** The Viewer role is available on the Enterprise plan only.

## **Add a team member to your workspace**

To invite a new member to your workspace:

-   Go to `Settings` > `Team`.
-   Click the `+ Invite` button in the top-right corner.
-   Enter the email address of the person you want to invite.
-   Select the appropriate role (Editor or Admin) from the dropdown.
-   Click `Send invite`.

The invited person will receive an email to join the workspace with the specified role.

## **Change a team member's role**

To update a member's role:

-   Navigate to `Settings` > `Team`.
-   Locate the team member whose role you want to update.
-   Use the dropdown menu next to their name to select the desired role.
-   Changes are applied immediately.

## **Remove a team member**

To remove a member from your workspace:

-   Go to `Settings` > `Team`.
-   Find the member you wish to remove.
-   Click the `…` (three-dot) menu next to their name.
-   Select `Remove member`.
-   Confirm the removal in the dialog that appears.

# **Connections**

The `Connections` settings allow you to manage integrations with external services. Each integration is represented as an `account` with its own authentication and configuration.

You can connect multiple accounts to the same integration for added flexibility, designate default accounts for specific integrations, and modify, reconnect, or remove accounts as needed.

## **What is an integration account?**

An **integration account** is a configured connection between your workspace and an external service, such as an API or data provider. Each account enables your workspace to authenticate and interact with the service to perform specific tasks or access features.

-   `Account / Key Name`: A user-defined name to identify the account, such as "Marketing HubSpot Account" or "Development Anthropic Key." This helps distinguish it from other accounts in the same service.
-   `Account Credentials`: The authentication details (e.g., API keys or OAuth tokens) required to connect securely to the external service. Credentials can be tested or updated if they become invalid.
-   `Default Status`: An optional setting that makes the account the default choice for its service, streamlining its use in workflows.

## **Types of accounts**

**User-managed accounts:**

-   Configured by users with their own credentials, such as personal API keys or OAuth tokens.
-   Ideal for integrations that require team- or project-specific access.

**Clay-managed accounts:**

-   Provided by Clay and configured for public use.
-   These accounts use workspace credits instead.
-   Clearly labeled in the `Connections` section, and often pre-set as default.

## **Add a new integration account**

To add a new account for an integration:

-   Navigate to `Settings` > `Connections`.
-   Click `+ Add connection` in the top-right corner.
-   Use the search bar to locate the service you want to integrate with.
-   Follow the on-screen instructions to authenticate and configure the connection.
-   Once completed, the account will appear under the corresponding service in the `Connections` list.

## **Managing existing accounts**

### **View your integration accounts**

-   Navigate to `Settings` > `Connections`.
-   Select a service (e.g., HubSpot or Anthropic) to see all associated accounts.
-   Use the search bar to quickly locate a specific account.

### **Edit your integration accounts**

-   Select the service and click the `…` menu next to an account.
-   Choose `Edit` to:
    -   Update the `Key Name`.
    -   Modify or re-enter credentials.
-   Toggle `Set as Default` to make this account the default.
-   Click `Save` to apply changes.

### **Testing credentials**

To ensure your account credentials are valid and the integration is functioning correctly:

-   Navigate to `Settings` > `Connections`.
-   Select the service (e.g., Anthropic) to view its associated accounts.
-   Locate the account you want to test.
-   Click the `…` menu next to the account and select `Test Connection`.

### **Setting default accounts**

A **default account** is automatically selected for workflows or integrations where no specific account is specified. To set an account as default:

-   Navigate to `Settings` > `Connections` and select the desired service (e.g., Anthropic).
-   Locate the account you wish to set as the default.
-   Click the `…` menu next to the account, and select `Set as Default`.
-   The account will now display a `default` label to indicate its status.

### **Deleting accounts**

-   Navigate to the service in the `Connections` section.
-   Click the `…` menu next to the account and select `Delete`.
-   Confirm the deletion.

### **Clay-managed accounts**

Clay-managed accounts simplify access to external services by providing pre-configured integrations that use workspace credits instead of requiring individual credentials.

For some integrations, only Clay-managed accounts are supported. For others, you will need to provide your own API key.

# **Plans and billing**

## **Understanding actions and data credits**

Clay's pricing is built on two separate usage meters:

-   **Actions** measure the work Clay orchestrates on your behalf — enriching data, running AI research, syncing to a CRM, exporting to CSV, sending to a sequencer, and more. Each enrichment or execution task consumes 1 action. Actions are a background meter included in your plan; 90% of customers will never hit their actions limit.
-   **Data credits** are used to purchase data from Clay's marketplace of 150+ third-party providers — finding emails, phone numbers, company data, and AI enrichments. Costs vary by data type and provider. Bringing your own API key for a third-party provider costs actions but does not consume data credits.

## **Plans**

Clay offers three plans. For a full comparison of features and pricing, visit our [**pricing page**](https://www.clay.com/pricing).

### **Launch plan**

-   **Best for:** Teams enriching fewer than 1,000 records per month
-   **Actions:** 15,000 per month
-   **Data credits:** 2,500 to 10,000 per month
-   **Starting price:** $185/month (includes 2,500 credits and 15,000 actions)
-   **Table limit:** 50,000 rows per table
-   **Features:** Basic enrichment, list building

### **Growth plan**

-   **Best for:** Teams enriching 1,000 to 10,000 records per month
-   **Actions:** 40,000 per month
-   **Data credits:** 6,000 to 100,000 per month
-   **Starting price:** $495/month (includes 6,000 credits and 40,000 actions)
-   **Table limit:** 50,000 rows per table
-   **Features:** Everything in Launch, plus CRM integrations, HTTP API, web intent signals, advanced automation, and Audiences

### **Enterprise plan**

-   **Best for:** Teams enriching 10,000+ records per month
-   **Actions and data credits:** Custom
-   **Benefits:** Volume discounts on data credits, dedicated Growth Strategist, managed onboarding, data warehouse integrations, bulk enrichment, SSO, RBAC, and more

## **Managing your plan**

To upgrade or downgrade your Clay workspace plan:

1.  Click on your profile picture in the top-right corner of the screen, and select `Settings`.
2.  In the left-hand sidebar, navigate to `Plans & billing`, then click the `Switch plan` button.
3.  Select the plan you want to switch to and review the details.
4.  Confirm your selection by clicking `Review change → Continue to payment`.

Your plan changes will be activated immediately, and any applicable charges will be applied.

## **Billing**

### **Update your payment method and billing email**

To update your billing and payment information:

1.  Click on your profile picture in the top-right corner and select `Settings`.
2.  In the sidebar, navigate to `Plans & billing`.
3.  Click `Update credit card` to edit your payment method or `Update email` to change your billing email.
4.  Enter the updated information for your payment method or billing email.
5.  Confirm your changes and click `Update`.

### **Trials**

Clay offers a 14-day free trial with 1,000 data credits, giving you access to key features like webhooks, CRM integrations, email sequencers, and HTTP API capabilities.

**Note:** Phone number enrichments are not available during the trial period. To access this feature, upgrade to a paid plan.

If your team wants to do a trial, each team member can create their own trial account to explore Clay independently.

# **Referrals**

Clay's referral program allows you to invite others to join and earn rewards. When someone signs up using your referral link and activates a **paying workspace**, both of you will earn **3,000 Clay credits**. Referral credits are not subject to the usual rollover rules — they stay in your account until you use them.

To access and share your referral link:

1.  Click on your profile picture in the top-right corner and select `Settings`.
2.  Navigate to `Referrals` in the sidebar.
3.  Copy your unique referral link displayed in the Referrals section.
4.  Share the link with friends, colleagues, or teams who might benefit from using Clay.

You can monitor your referral activity, including the number of leads, converted users, and credits earned, directly in the Referrals section.
