---
title: Workspace settings
description: Create, switch between, and manage Clay workspaces — including workspace name, picture, billing email, SSO setup, agency setups, deletion, and recovering a previous workspace.
last_synced: 2026-04-26T01:40:56.525Z
---

# Workspace settings

Use this article to create and switch between Clay workspaces, manage workspace details like the name, picture, and billing email, set up workspaces for agency work, and delete a workspace.

## Creating a new workspace

Creating an additional workspace is not available through in-app settings for most accounts. To create a new workspace, sign up using a **different email address** at [app.clay.com](https://app.clay.com) — this starts a new workspace where you are the admin from day one.

You do not need to leave any workspaces you're already a member of. Your existing workspace memberships stay intact, and each workspace is independent with its own tables, credits, and billing.

## Switching between workspaces

Your Clay account can be associated with more than one workspace — for example, if you explored Clay during a free trial and later upgraded or joined a team's workspace. Each workspace has its own tables, credits, and billing.

To switch between workspaces:

-   Click your **profile picture or name in the top-right corner** of the Clay navigation bar.
-   In the dropdown that appears, look for the **Workspaces** section.
-   Click the workspace you want to open.

**If your tables seem to have disappeared** — for example, after upgrading your plan or returning to Clay after some time — check the workspace switcher first. Your data is not deleted; it's in the workspace where you originally created it.

**Note:** When you upgrade a plan, the upgrade applies to the specific workspace you are currently in. If you upgrade while viewing a different workspace than the one where you created your tables, those tables remain in the original workspace. Use the workspace switcher to navigate between them.

## Can't find a previous account or workspace

If you log in and find yourself in a blank new workspace with none of your tables, or feel like Clay created a brand new account for you, this almost always means you signed in with a different identity than the one you used originally:

-   **Different Google account:** Clicking **Continue with Google** while a different Google account was active in your browser (for example, a personal Gmail instead of a work account) signs you into that Google account and automatically creates a new workspace for it. Your original workspace is untouched.
-   **Different email address:** Signing in with a different email address creates a separate Clay account and workspace. Each email address has its own account.

**To get back to your original workspace:**

1.  **Sign out and sign back in with your original credentials:** Go to [app.clay.com](https://app.clay.com), sign out, and then sign in with the email address or Google account you originally used. Your workspace and tables will be there.
2.  **Use the workspace switcher if you have multiple workspaces under the same account:** Click your **profile picture or name in the top-right corner** and look for the **Workspaces** section in the dropdown. The switcher shows all workspaces the currently-signed-in account belongs to — it cannot show workspaces from a different Clay account (different email or Google account).
3.  **Invite your other account to your paid workspace (permanent fix for multiple Google accounts):** If your browser regularly auto-signs you into a Google account that is not your paid workspace's account — for example, Chrome keeps signing you into your personal Gmail while your paid workspace lives under a different email — you can invite that Google account to your paid workspace as a member. Once accepted, your secondary account will see your paid workspace in the workspace switcher every time it signs in, without needing to sign out or use incognito. To set this up: from your paid workspace, go to `Settings` > `Team`, click `+ Invite`, enter your secondary email address, and click `Send invite`. Accept the invite from your secondary email address. From that point on, the paid workspace appears in the workspace switcher whenever you are signed in as your secondary account.

**If you cannot find your original workspace** or you are not sure which email address or Google account you originally used, contact Clay support via the in-app chat. Having the following details ready will help the team locate your account quickly: the email address you originally signed up with, the login method you used (Google or email and password), and anything you remember about the workspace — its name, roughly when you created it, or the names of tables in it.

For step-by-step guidance on recovering access after signing in with the wrong Google account, see [Account settings](./account-settings.md).

## Using Clay as an agency

If you're managing Clay for multiple clients, the recommended approach is to use a **separate workspace for each client**. Each workspace is fully independent — it has its own tables, data credits, billing, connections, and settings — so each client's work stays isolated and every configuration applies to that client only.

**Why separate workspaces work well for agencies:**

-   Each workspace has its own **AI Context** domain (accessible via **AI context** in the left sidebar of your workspace), so you can set the right company domain and business context per client rather than sharing a single workspace setup.
-   Credits and billing are tracked separately per workspace, making it easy to see exactly what each client is consuming.
-   When a project ends, you can hand the workspace over to the client by ensuring they have admin access and removing yourself — all tables, workbooks, and settings remain in place.

**Two common ways to set this up:**

1.  **Client creates the workspace and invites you** — the client signs up at [app.clay.com](https://app.clay.com) using their company email, then adds you as an admin. Their workspace has its own billing and credits from day one.
2.  **You create the workspace on their behalf** — by default, Clay accounts can only hold one workspace. To create additional workspaces for clients, contact Clay support to have this enabled on your account. Once enabled, an **Add workspace** option will appear in the workspace switcher. Workspaces you create this way start without trial credits; billing and credits are configured per workspace after creation.

## Workspace picture

To update your workspace picture:

-   Navigate to `Settings` > `Workspace settings`.
-   Click `Upload new picture` to upload an image or choose an icon.
    -   Please ensure the image is in png, jpg, jpeg, or gif format with a max size of 5MB.
-   Use the `Delete` button if you wish to remove your current profile picture.
-   Click `Save` to apply your changes.

## Workspace name

To update your workspace name:

-   Go to `Settings` > `Workspace settings`.
-   Update the `Workspace name` field with your desired name.
    -   This name will be displayed across your workspace and should be accessible for team identification.
-   Click `Save` to confirm your changes.

## Billing email

To update your billing email:

-   In `Workspace settings`, edit the `Billing email` field to update the email address used for all billing-related communication.
-   Click `Save` to ensure the new email is recorded.

## Single Sign-On (SSO)

SSO is not configured through the Clay workspace settings UI — there is no self-serve configuration panel. To set up SSO for your workspace, contact Clay support. SSO is available on **Enterprise** plans at no additional cost, and as a paid add-on on annual Pro and annual Growth plans.

See [Single Sign-On (SSO)](./single-sign-on.md) for full details on eligibility, the setup process (handled by Clay's support team via WorkOS), how login behavior changes once SSO is enabled, and important notes on user provisioning.

## Beta Program

The Clay Beta Program gives your workspace early access to experimental and cutting-edge features before they reach general availability. Beta features are marked throughout the app with a **Beta** tag.

**Joining the Beta Program is self-serve and available to all workspaces.** Only a workspace admin can enroll or leave — non-admins can see the option but cannot toggle it.

To join the Beta Program:

-   Go to `Settings` > `Workspace settings`.
-   In the **Beta program** section, click **Join beta program**.
-   Your workspace immediately gains access to all current beta features.

To leave the Beta Program, return to the same section and click **Leave beta program**.

Once enrolled, beta feature announcements and discussions are shared in the [**#clay-beta-program**](https://clayrunhq.slack.com/archives/C08T0RDMBBR) channel in the Clay community Slack.

## Delete your workspace

You can permanently delete your Clay workspace through workspace settings. This action is permanent and cannot be undone.

**Requirements:**

-   The workspace must have **no pending invites**.\n-   You must be the **only member** in the workspace.

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
