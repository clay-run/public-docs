---
title: Account and workspace settings
description: Manage account and workspace settings, team members, SSO, integration accounts, and billing.
last_synced: 2026-04-26T01:40:56.525Z
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

## **Change your account email address**

The email address field in `Settings` > `Account` is read-only and cannot be changed directly in the UI. To change the email associated with your Clay account, contact Clay support via the in-app chat.

**Who can request this change:** Email address changes are processed by Clay's support team and handled internally. Support will only honor requests that originate from the workspace admin's registered email address — if you are not the workspace admin, coordinate with them to submit the request.

**If the new email address is already linked to another Clay account:** That existing account must be resolved (for example, deleted) before the change can be made.

Changing your email address does not affect your workspace data or your password.

## **Change your password**

_If you sign in with Google, the **Change password** option will not appear on your Security tab — it is only visible for email + password accounts. See [Switch from Google login to email and password](#switch-from-google-login-to-email-and-password) below instead._

To change your account password:

-   Visit your `Settings` and head to the `Account` section.
-   Open the `Security` tab under `Your profile`.
-   Click `Change password`. A magic link will be sent to your registered email address.
-   Follow the instructions in the email to securely update your password.

If you cannot log in because you have forgotten your password, use the **Forgot password?** link on the Clay login page, or go directly to [app.clay.com/forgot](https://app.clay.com/forgot). Enter your email address and follow the link in the email to set a new password.

If you do not receive a reset email, you likely signed up with Google rather than with email and password — there is no password on your account to reset. See [Switch from Google login to email and password](#switch-from-google-login-to-email-and-password) below if you want to create a password for your account.

## **Switch from Google login to email and password**

If you signed up with Google and want to create a password so you can log in with your email and password instead, this cannot be done through your account settings — it requires a support action.

To request the change:

-   Open the in-app chat and ask the support team to switch your login method from Google to password.
-   Once the change is made, go to [app.clay.com/forgot](https://app.clay.com/forgot), enter your email address, and follow the link in the email to set your new password.

After completing the password recovery steps, you can log in with your email and password. Note that Clay accounts support only one login method at a time — either Google OAuth or email + password, not both. After switching, you will no longer be able to sign in with Google on this account.

**Important:** Once switched, sign in using the **email and password fields** on the Clay login page — do **not** click `Continue with Google`. The `Continue with Google` button authenticates using whichever Google account is currently active in your browser. If you are signed into a different Google account (for example, a personal Gmail), clicking that button will sign you into that account's Clay workspace instead of yours, or may create a new Clay account.

If you regularly use multiple Google accounts in the same browser, using email and password directly is the most reliable approach. Alternatively, you can use a separate browser profile signed into only the correct Google account.

**If you already signed in with the wrong Google account**

If clicking `Continue with Google` used an unintended account (for example, your personal Gmail), Clay automatically creates a new workspace for that email address. You will be taken into an onboarding flow for the new workspace — there is no skip or exit button, and the onboarding screen does not show the regular Clay navigation bar or workspace switcher.

To get back to your correct workspace:

-   **Navigate directly to your existing workspace:** Type `https://app.clay.com/workspaces/<your-workspace-id>` in the address bar. This loads your real workspace without going through the onboarding flow for the unwanted one.
-   **Contact Clay support:** Use the in-app chat to ask support to stop the onboarding flow or delete the unwanted workspace. The support team can do this on your behalf even if you cannot reach that workspace's settings yourself.

## **Using a corporate identity provider (Entra ID, Okta, etc.)**

Individual Clay accounts support two login methods only: **Sign in with Google** (Google OAuth) or **email and password**. Microsoft Entra ID (Azure AD), Okta, and other corporate identity providers are not available as individual login options.

If your company wants all Clay users to authenticate through a corporate IdP, a workspace admin must contact Clay support to set up workspace-wide SSO. See [Single Sign-On (SSO)](#single-sign-on-sso) for details on eligibility (Enterprise plan or SSO add-on) and the setup process.

## **"Your session has expired" error**

If you see a **"Your session has expired"** message when trying to access Clay, follow these steps:

1.  **Log out of your account.**
2.  **Hard refresh your browser:**
    -   Mac: `Cmd + Shift + R` (Chrome/Firefox) or `Cmd + Option + R` (Safari)
    -   PC: `Ctrl + F5` (Chrome/Firefox/Microsoft Edge)
3.  **Log back in.**
4.  **If the issue persists, try an incognito or private browsing window** — this rules out cached session data or conflicting cookies.
5.  **If you use a Clay Chrome extension (Clay for Chrome or Clip to Clay), restart it** — close and reopen the extension, or disable and re-enable it from your browser's extensions page.

If none of these steps resolve the error, contact Clay support via the in-app chat icon in the bottom-right corner of Clay.

## **Clay API key access**

Your Clay API key enables Clay-specific integrations and external connections. To manage your API key:

-   Go to `Settings` >`Your profile` > `API key`.
-   Use the following options:
    -   `Copy` the key for application use.
    -   `Regenerate` the key if compromised.

## **Delete your account**

You can permanently delete your Clay account through your account settings. Before proceeding, please note:

**Requirements:**

-   You must be a **member** (not admin) in all your workspaces, OR
-   You must be an **admin** in a workspace where at least one other admin exists, OR
-   You must be the **only member** in your workspace

If you are the sole admin of a workspace with other members or pending invites, you must transfer admin rights to another member, remove remaining members, or cancel pending invites before deleting your account.

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
-   You will receive an email confirmation once your account has been deleted.
-   **If you want to sign up again with the same email address, you must wait 7 days after deletion.** If you need to re-register sooner, contact Clay support via the in-app chat to request an early clearance.

**Important:** Account deletion is permanent and cannot be undone. While your data is marked for deletion and critical billing/authentication records are removed immediately, full data removal from our database may take additional time.

# **Workspace settings**

Workspace settings give you control over key aspects of your workspace, such as its name, profile picture, and billing email. These settings ensure your workspace is easily identifiable and that billing communications reach the correct contact. Below are the steps for updating key workspace details.

## **Creating a new workspace**

Creating an additional workspace is not available through in-app settings for most accounts. To create a new workspace, sign up using a **different email address** at [app.clay.com](https://app.clay.com) — this starts a new workspace where you are the admin from day one.

You do not need to leave any workspaces you're already a member of. Your existing workspace memberships stay intact, and each workspace is independent with its own tables, credits, and billing.

## **Switching between workspaces**

Your Clay account can be associated with more than one workspace — for example, if you explored Clay during a free trial and later upgraded or joined a team's workspace. Each workspace has its own tables, credits, and billing.

To switch between workspaces:

-   Click your **profile picture or name in the top-right corner** of the Clay navigation bar.
-   In the dropdown that appears, look for the **Workspaces** section.
-   Click the workspace you want to open.

**If your tables seem to have disappeared** — for example, after upgrading your plan or returning to Clay after some time — check the workspace switcher first. Your data is not deleted; it's in the workspace where you originally created it.

**Note:** When you upgrade a plan, the upgrade applies to the specific workspace you are currently in. If you upgrade while viewing a different workspace than the one where you created your tables, those tables remain in the original workspace. Use the workspace switcher to navigate between them.

## **Using Clay as an agency**

If you're managing Clay for multiple clients, the recommended approach is to use a **separate workspace for each client**. Each workspace is fully independent — it has its own tables, data credits, billing, connections, and settings — so each client's work stays isolated and every configuration applies to that client only.

**Why separate workspaces work well for agencies:**

-   Each workspace has its own **AI Context** domain (configured in **Settings → AI Context**), so you can set the right company domain and business context per client rather than sharing a single workspace setup.
-   Credits and billing are tracked separately per workspace, making it easy to see exactly what each client is consuming.
-   When a project ends, you can hand the workspace over to the client by ensuring they have admin access and removing yourself — all tables, workbooks, and settings remain in place.

**Two common ways to set this up:**

1.  **Client creates the workspace and invites you** — the client signs up at [app.clay.com](https://app.clay.com) using their company email, then adds you as an admin. Their workspace has its own billing and credits from day one.
2.  **You create the workspace on their behalf** — by default, Clay accounts can only hold one workspace. To create additional workspaces for clients, contact Clay support to have this enabled on your account. Once enabled, an **Add workspace** option will appear in the workspace switcher. Workspaces you create this way start without trial credits; billing and credits are configured per workspace after creation.

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
-   Set a connection as the default in `Settings` → `Connections` — this is a workspace admin–only action.
-   Delete connections added by other workspace members — editors can only delete connections they personally added.

### **Viewer**

**Viewers** have read-only access to workspace content.

**Note:** The Viewer role is available on the Enterprise plan only.

## **Add a team member to your workspace**

Workspace access in Clay is invitation-only. When a new user signs up for Clay, they are automatically placed in their own workspace — they will not join yours unless you explicitly invite them. Your workspace remains private to you until you send an invite.

To invite a new member to your workspace:

-   Go to `Settings` > `Team`.
-   Click the `+ Invite` button in the top-right corner.
-   Enter the email address of the person you want to invite, then press **Enter** (or type a comma) to confirm it. You can add multiple addresses this way.
-   Select the appropriate role (Editor or Admin) from the dropdown.
-   Click `Send invite`.

The invited person will receive an email to join the workspace with the specified role. The person will appear in your team list with a **Pending** status until they accept.

**If the invitee sees the error "This invite was sent to a different email address"**

This error appears when the invitee is already logged into Clay with a different account than the one the invite was sent to. Clay verifies server-side that the logged-in account's email matches the invite email — if they don't match, the invite cannot be accepted from that session. To resolve it, have the invitee open the invite link in an **incognito or private browsing window** (where no Clay session is active) — they will be prompted to sign in or sign up with the correct email and can then accept the invite. Alternatively, they can log out of Clay first and then click the invite link again.

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
-   Click the `…` (three-dot) menu at the end of their row.
-   Select `Remove member`.
-   Confirm the removal in the dialog that appears.

**What happens when you remove a member:**

-   All tables, workbooks, and groups owned by the removed member are automatically transferred to the longest-tenured admin in the workspace (the admin whose admin role was granted earliest).
-   You cannot remove the last admin from a workspace — at least one admin must remain at all times.
-   Access is revoked immediately. If the removed member has an active browser session open, they are not logged out of the current page right away — but their workspace permissions are invalidated instantly, so any new action, page refresh, or navigation will return an access-denied error.

**Transferring ownership when a team member leaves**

If a former employee owns tables or workbooks in your workspace, there is no separate "transfer ownership" UI in Clay — removing the former member from the workspace is how you do it. All tables, workbooks, and groups they owned will automatically reassign to the longest-tenured admin (the workspace admin whose admin role was assigned earliest).

## **Cancel a pending invite**

If a team member hasn't accepted their invite yet, they appear in `Settings` > `Team` with a **Pending** status. There is no separate "cancel invite" button — use the same `Remove member` action:

-   Go to `Settings` > `Team`.
-   Find the pending entry (shown with a **Pending** badge).
-   Click the `…` (three-dot) menu at the end of their row.
-   Select `Remove member`.

Once removed, you can re-invite the same email address if needed. Only workspace admins can cancel pending invites.

# **Single Sign-On (SSO)**

Single Sign-On (SSO) is available to **Enterprise plan** customers at no additional cost. It is also available as a paid add-on for customers on an **annual Pro plan** or **annual Growth plan** — contact Clay support or your Growth Strategist to add it to your plan. SSO is not available on monthly plans, Launch plans, or free/trial plans. SSO lets your organization authenticate Clay users through your existing identity provider (IdP). Clay uses WorkOS to manage SSO and supports any IdP that uses SAML or OIDC protocols — including Okta, Azure AD (Entra ID), JumpCloud, Google Workspace, and others.

## **Setting up SSO**

SSO setup is managed by Clay's support team — there is no self-serve configuration in the Clay UI. To get started, contact Clay support.

The typical setup process:

1.  Contact Clay support to initiate SSO setup.
2.  Clay support creates your organization in WorkOS and sends a configuration link to your IT contact.
3.  Your IT team follows the link to connect your identity provider and complete the setup.
4.  Once your IT team confirms the WorkOS setup is complete, notify Clay support. **Note:** If you test by clicking the Clay tile in your IdP dashboard at this point, you may see `{"type":"BadRequest","message":"Unable to login","details":null}` — this is expected and means SSO activation is still pending on Clay's side.
5.  Clay support activates (enforces) SSO on your workspace.

**Note:** The email domain used for SSO authentication is configured on Clay's side. If you receive an error during the WorkOS setup stating that your domain is not recognized or not allowed, contact Clay support — only the support team can update the allowed domain setting.

## **What happens when SSO is enabled**

-   All users whose email address is on your verified domain are redirected to sign in through SSO when they type their email on the Clay login page. **Note:** This redirect is handled in the browser — users who have an existing email + password Clay account can still log in using their password directly, which bypasses the SSO redirect. Clay does not block password-based login at the backend for SSO-configured domains.
-   Google OAuth sign-in is disabled for users on your domain. Clicking the **Sign in with Google** button on the login page will return an error (`Google OAuth is disabled for this account`) — this button uses Google OAuth, which is a separate authentication path from SSO.
-   SSO is configured at the email domain level — if your organization uses multiple Clay workspaces, users on your domain will be routed through SSO for all of them.
-   Once SSO is activated, users can sign in from either the Clay login page or directly from your IdP dashboard (for example, clicking the Clay tile in your Okta launcher). If clicking the IdP tile returns `{"type":"BadRequest","message":"Unable to login","details":null}`, SSO has likely not yet been activated on Clay's side — contact Clay support to complete activation.

**How SSO users should sign in:** On the Clay login page, type your **email address** into the email field and click **Continue** — do **not** click the `Sign in with Google` button. Entering your email triggers domain detection, which redirects you to your SSO provider automatically.

**If your Clay account was originally created with Google (no password set):** Once SSO is enabled for your domain, the `Sign in with Google` button will return an error — Google OAuth is disabled for SSO domains. Because your account was created through Google, you have no Clay email + password; attempting to enter a password or trigger a password reset will not work (there is no Clay password on your account to reset). To sign in, simply type your **email address** into the email field and click **Continue** to be redirected to your SSO provider. If the redirect does not work after SSO has been activated by Clay support, contact Clay support to verify the configuration.

## **MFA enforcement and compliance requirements**

Clay does not have a workspace admin setting to require multi-factor authentication (MFA) for all users. When SSO is enabled, users on your domain are redirected to your identity provider in the browser — but this is not a backend login block. Users who have an existing email + password Clay account can log in via password and bypass the SSO redirect entirely, which means IdP-level MFA requirements are not enforced for those users.

If your security policy or compliance requirements (for example, SOC 2) mandate that all users authenticate through MFA, this is a current limitation: there is no workspace-level setting in Clay to disable password-based login or restrict authentication to SSO only. For Clay's security and compliance documentation, including the SOC 2 report, visit [trust.clay.com](https://trust.clay.com).

## **External collaborators (non-domain email addresses)**

SSO only applies to users whose email address matches your verified domain. Team members with email addresses outside your domain are not affected and continue to access Clay through their regular login (Google or password).

## **User provisioning**

**Clay does not currently support SCIM provisioning.** SSO (via WorkOS) is used for authentication only — Clay does not add users to your workspace automatically through SSO, and there is no JIT (Just-in-Time), SCIM, or domain-join provisioning for workspace membership. If an uninvited user with your email domain signs in via SSO, they will authenticate successfully and a Clay account will be created for them, but they will not be added to your enterprise workspace — instead, they will be directed to create a new personal workspace. To onboard a new team member:

1.  Invite them to your Clay workspace first via `Settings` > `Team` > `+ Invite`.
2.  Have them sign in using SSO — they will be authenticated and placed into the correct workspace.

**Important:** Always invite users to your workspace before they sign in with SSO. If a user signs in via SSO before receiving their workspace invite, they will be placed into a new standalone personal workspace instead of your enterprise workspace — creating a messy state that requires support to resolve.

SCIM directory sync is on Clay's roadmap — contact Clay support or your Growth Strategist for the latest status on this feature.

## **Disabling or re-enabling SSO**

If you need to temporarily disable SSO enforcement — for example, during an IdP migration, to allow a user to access their account outside of SSO, or for troubleshooting — contact Clay support. The support team can disable SSO on Clay's side without any changes to your IdP or WorkOS configuration.

Your identity provider setup and WorkOS organization remain intact when SSO is disabled, so re-enabling is equally straightforward: contact Clay support and they will turn it back on. No IT reconfiguration is required for either step.

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

**Note:** Some connection management actions are restricted by role:

-   **Set as Default** is a **workspace admin–only** action — only admins see this option in the `…` menu.
-   **Delete** is available to the member who added the connection and to workspace admins. If you need to delete a connection that was added by someone else, ask a workspace admin.

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

### **Workspace row limit**

All workspaces have a global row limit of **10 million rows** across all tables. This cap counts rows in every table in your workspace, regardless of plan. If you reach this limit, you may see the error **"Your Subscription Does Not Allow Any More Records."**

Deleting a table removes its rows from your workspace row count immediately — rows are freed as soon as the table is moved to Trash, without requiring permanent deletion from Trash.

**Finding tables to delete**

If you are approaching the workspace row limit, take stock of tables that are no longer needed:

-   On the Home page, sort by **Created at** or **Last opened by me** to surface older or less-recently-accessed tables that may no longer be in use.
-   Open `Settings` > `Usage` to view the credit usage dashboard. Filter by a recent time period and sort by `Credits used` ascending to identify tables with little or no recent credit activity — these are often good candidates for deletion.

For instructions on deleting tables and permanently removing them from Trash, see [Delete content within your workspace](delete-content-within-your-workspace.md).

## **Managing your plan**

To upgrade or downgrade your Clay workspace plan:

1.  Click on your profile picture in the top-right corner of the screen, and select `Settings`.
2.  In the left-hand sidebar, navigate to `Plans & billing`, then click the `Switch plan` button.
3.  Select the plan you want to switch to and review the details.
4.  Confirm your selection by clicking `Review change → Continue to payment`.

Your plan changes will be activated immediately, and any applicable charges will be applied.

## **Billing**

### **Update your billing address, payment method, and billing email**

To update your billing and payment information:

1.  Click on your profile picture in the top-right corner and select `Settings`.
2.  In the sidebar, navigate to `Plans & billing`.
3.  Click the `Edit` dropdown.
    -   Select `Edit billing info...` to update your name, billing email, country, address, and postal code.
    -   Select `Edit payment method...` to update your credit card or payment method.
4.  Enter the updated information and confirm your changes.

### **Trials**

Clay offers a 14-day free trial with 1,000 data credits, giving you access to key features like webhooks, CRM integrations, email sequencers, and HTTP API capabilities.

**Note:** Phone number enrichments are not available on free or trial plans — this restriction applies even if you have unused data credits. To access this feature, upgrade to a paid plan.

If your team wants to do a trial, each team member can create their own trial account to explore Clay independently.

Trial tables can hold up to **1,000 rows each**. The table view also displays only the first **50 rows** — rows beyond that are blurred in the UI until you upgrade to a paid plan.

## **Contacting support**

Clay's support team is available **Monday through Friday, 9 am–9 pm U.S. Eastern Time**. To reach support, use the in-app chat icon in the bottom-right corner of Clay.

# **Referrals**

Clay's referral program allows you to invite others to join and earn rewards. When someone signs up using your referral link and activates a **paying workspace**, both of you will earn **3,000 Clay credits**. These credits are not added immediately — they are typically applied around **30 days after the referred user upgrades to a paid plan**. Referral credits are not subject to the usual rollover rules — they stay in your account until you use them.

To access and share your referral link:

1.  Click on your profile picture in the top-right corner and select `Settings`.
2.  Navigate to `Referrals` in the sidebar.
3.  Copy your unique referral link displayed in the Referrals section.
4.  Share the link with friends, colleagues, or teams who might benefit from using Clay.

You can monitor your referral activity, including the number of leads, converted users, and credits earned, directly in the Referrals section.

**Note:** The Referrals section in Settings shows your activity as a referrer — the people you've invited and credits you've earned. If you signed up using someone else's referral link, your 3,000 bonus credits will appear in your account balance once the referral is confirmed; there is no separate tracker in Settings for your status as a referee.
