---
title: Account settings
description: Update your Clay profile picture, name, password, and login method, manage your API key, and delete your account.
last_synced: 2026-04-26T01:40:56.525Z
---

# Account settings

Use this article to keep your personal Clay account details up to date — your profile picture, name, password, and login method — and to manage your API key or delete your account.

## Update your profile picture

To update your profile picture:

-   Go to `Settings` and select `Account` from the left-hand menu.
-   In the `Your details` tab under `Your profile`, click `Upload new picture` to upload an image or choose an icon.
    -   Please ensure the image is in png, jpg, jpeg, or gif format with a max size of 5MB.
-   Use the `Delete` button if you wish to remove your current profile picture.
-   Click `Save` to confirm your changes.

## Update your name

To update your account name:

-   Go to `Settings` and select `Account`.
-   Under the `Your details` tab, edit your name in the `Name` field.
-   Click `Save` to ensure your changes are updated.

## Change your display theme

Clay supports three display themes that you can switch at any time:

-   **Standard** — the default light theme.
-   **System** — follows your device or operating system's appearance setting, switching between light and dark automatically.
-   **Dark** — a dark color scheme for the entire Clay interface.

To change your theme:

-   Go to `Settings` and select `Appearance` from the left-hand menu.
-   Under **Theme**, select your preferred option. Your selection takes effect immediately.

**Note:** Your theme preference is saved per browser and device. It is not synced to your user profile, so you will need to set it separately on each browser or device you use to access Clay.

## Change your account email address

The email address field in `Settings` > `Account` is read-only and cannot be changed directly in the UI. To change the email associated with your Clay account, contact Clay support via the in-app chat.

**Who can request this change:** Email address changes are processed by Clay's support team and handled internally. Support will only honor requests that originate from the workspace admin's registered email address — if you are not the workspace admin, coordinate with them to submit the request.

**If the new email address is already linked to another Clay account:** That existing account must be resolved (for example, deleted) before the change can be made.

Changing your email address does not affect your workspace data or your password.

**If your Google account email changed externally and you now see a blank workspace**

If your Google account email was updated outside of Clay — for example, a Gmail address was migrated to a Google Workspace domain — signing into Clay with the new address creates a new empty workspace. Clay matches accounts by email address at sign-in and cannot automatically link the new email to your existing account. Your original workspace is not lost; it stays tied to your original email address.

To regain access with your new email:

1.  Sign into Clay using your **original email address**.
2.  In your original workspace, go to `Settings` > `Team` and invite your new email address as **Admin**, then click **Send invite**.
3.  Accept the invite from your new email address — you will have full Admin access to your original workspace and all your data.

If you no longer have access to your original email address, contact Clay support via the in-app chat — the support team can verify your identity and help restore access.

## Migrating your whole team to a new email domain

If your company is changing its email domain and every team member needs a new email address on their Clay account, use the following sequence. Clay matches accounts by email address at sign-in — signing in with a new address creates a new empty workspace rather than linking to the existing account — so coordinating the switch in the right order prevents anyone from losing access.

**Recommended sequence:**

1.  **Change the workspace admin's email first, before the old mailbox is disabled.** While your current email address is still active, email support@clay.com from your registered Clay address and request the change to your new address. Clay support will update the email on your account.

2.  **After the domain switch, sign in as admin with your new email address.** Your workspace data, tables, and settings will be exactly as you left them.

3.  **Remove and re-invite the remaining team members using their new addresses.** Go to `Settings` > `Team`, remove each member, and re-invite them using their new email address. As the workspace admin, you can do this yourself without opening a support ticket for each person.

**Your workspace data is not affected by this process.** Tables, enrichments, shared views, run history, and credits belong to the workspace itself — not to individual user accounts. Removing a member and re-inviting them on a new email address does not delete or move any of that data. Any tables or workbooks they owned automatically transfer to the longest-tenured admin until they re-join the workspace.

**API keys survive an email change.** Clay API keys are scoped to the account by internal user ID, not by email address. Changing an email — whether done by support or via the remove-and-re-invite method — does not invalidate existing API keys. Production integrations will continue working without regeneration.

**Important: prevent team members from signing in before they are re-invited.** If someone signs in with their new email address before you have re-invited them, Clay creates a new empty workspace for that email. Their data in the original workspace is not lost, but they will land in the wrong place. If this happens, invite their new address from `Settings` > `Team` > `+ Invite`, have them accept the invite, and they will regain full access to the original workspace and all its data.

## Update your country

Clay's account profile settings don't include a country field — there is no country selector in `Settings` > `Account`. If you need to update the country associated with your billing information, go to `Settings` > `Plans & billing`, click `Edit`, and select `Edit billing info...` — this lets you update your name, billing email, and country. US-based accounts can also update their address, city, state, and ZIP code there.

## Change your password

_If you sign in with Google, the **Change password** option will not appear on your Security tab — it is only visible for email + password accounts. See [Switch from Google login to email and password](#switch-from-google-login-to-email-and-password) below instead._

To change your account password:

-   Visit your `Settings` and head to the `Account` section.
-   Open the `Security` tab under `Your profile`.
-   Click `Change password`. A magic link will be sent to your registered email address.
-   Follow the instructions in the email to securely update your password.

If you cannot log in because you have forgotten your password, use the **Forgot password?** link on the Clay login page, or go directly to [app.clay.com/forgot](https://app.clay.com/forgot). Enter your email address and follow the link in the email to set a new password.

If you do not receive a reset email, you likely signed up with Google rather than with email and password — there is no password on your account to reset. See [Switch from Google login to email and password](#switch-from-google-login-to-email-and-password) below if you want to create a password for your account.

## Switch from Google login to email and password

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

## Using a corporate identity provider (Entra ID, Okta, etc.)

Individual Clay accounts support two login methods only: **Sign in with Google** (Google OAuth) or **email and password**. Microsoft Entra ID (Azure AD), Okta, and other corporate identity providers are not available as individual login options.

If your company wants all Clay users to authenticate through a corporate IdP, a workspace admin must contact Clay support to set up workspace-wide SSO. See [Single Sign-On (SSO)](./single-sign-on.md) for details on eligibility (Enterprise plan or SSO add-on) and the setup process.

## "Your session has expired" error

If you see a **"Your session has expired"** message when trying to access Clay, follow these steps:

1.  **Log out of your account.**
2.  **Hard refresh your browser:**
    -   Mac: `Cmd + Shift + R` (Chrome/Firefox) or `Cmd + Option + R` (Safari)
    -   PC: `Ctrl + F5` (Chrome/Firefox/Microsoft Edge)
3.  **Log back in.**
4.  **If the issue persists, try an incognito or private browsing window** — this rules out cached session data or conflicting cookies.
5.  **If you use a Clay Chrome extension (Clay for Chrome or Clip to Clay), restart it** — close and reopen the extension, or disable and re-enable it from your browser's extensions page.

If none of these steps resolve the error, contact Clay support via the in-app chat icon in the bottom-right corner of Clay.

## Clay API key access

Your Clay API key enables Clay-specific integrations and external connections. To manage your API key:

-   Go to `Settings` >`Your profile` > `API key`.
-   Use the following options:
    -   `Copy` the key for application use.
    -   `Regenerate` the key if compromised.

## Delete your account

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
-   Your account email, display name, and username are anonymized.
-   For any workspaces affected by your account deletion, workspace admins will receive email notifications.
-   Your private app account and Stripe customer information are deleted to prevent unexpected charges.
-   You will receive an email confirmation once your account has been deleted.
-   **If you want to sign up again with the same email address, you must wait 7 days after deletion.** If you need to re-register sooner, contact Clay support via the in-app chat to request an early clearance.

**Important:** Account deletion is permanent and cannot be undone. While your data is marked for deletion and critical billing/authentication records are removed immediately, full data removal from our database may take additional time.
