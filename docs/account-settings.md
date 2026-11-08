---
title: Account settings
description: Update your Clay profile picture, name, email address, password, and login method, manage your legacy API key, and delete your account.
last_synced: 2026-04-26T01:40:56.525Z
---

# Account settings

Use this article to keep your personal Clay account details up to date — your profile picture, name, email address, password, and login method — and to manage your API key or delete your account.

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

You can change your own login email in `Settings` > `Account` > `Security`, under `Change how you sign in`. You do not need a workspace admin or Clay support to make this change for an eligible account. The email field on the `Your details` tab is read-only; use `Change sign-in` on the `Security` tab instead.

**If you sign in with email and password:**

1.  Go to `Settings` > `Account` and open the `Security` tab.
2.  Click `Change sign-in`, select `Change your login email`, and click `Continue`.
3.  Enter the verification code sent to your **current email address** and click `Continue`.
4.  Enter your `New email` and click `Continue`. Leave `Also change your password` unchecked to keep your current password, or select it to set a new one.
5.  Enter the verification code sent to your **new email address** and click `Continue`.
6.  Review the change and click `Continue to sign in`. Clay signs you out of all current sessions. Sign back in with your new email and password.

**If you sign in with Google:** Open the same `Change sign-in` menu and select `Change your Google account`. Verify the code sent to your current email, then click `Continue with Google` and choose the Google account you want to use. Clay signs you out of all current sessions; sign back in with the new Google account. You can also [switch to email and password](#switch-from-google-login-to-email-and-password) and choose a new email during that process.

Changing your login email keeps your existing Clay account and workspace data.

**Requirements and troubleshooting:**

-   You need access to your current inbox and the new inbox or Google account. If you cannot access your current inbox, contact Clay support via the in-app chat.
-   The new email must not already belong to another Clay account. If you see `This email can't be used.`, try another address or contact support for help.
-   Complete the process within 30 minutes. If the request expires, restart it.
-   For accounts managed by an organization, sign-in changes are disabled. Contact an organization admin for help. If `Change sign-in` is missing, contact Clay support; self-service changes support email-and-password and Google accounts when the option is available.

**If your Google account email changed externally and you now see a blank workspace**

If your Google account email was updated outside of Clay — for example, a Gmail address was migrated to a Google Workspace domain — signing into Clay with the new address creates a new empty workspace. Clay matches accounts by email address at sign-in and cannot automatically link the new email to your existing account. Your original workspace is not lost; it stays tied to your original email address.

To regain access with your new email:

1.  Sign into Clay using your **original email address**.
2.  In your original workspace, go to `Settings` > `Team` and invite your new email address as **Admin**, then click **Send invite**.
3.  Accept the invite from your new email address — you will have full Admin access to your original workspace and all your data.

If you no longer have access to your original email address, contact Clay support via the in-app chat — the support team can verify your identity and help restore access.

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

If you signed up with Google, you can switch to email and password from your account settings using `Change sign-in`.

To switch:

1.  Go to `Settings` > `Account` > `Security` and click `Change sign-in`.
2.  Select `Switch to email and password` and click `Continue`.
3.  Enter the verification code sent to your current email address.
4.  Keep your current email or enter a new one, then enter and confirm your new password. Click `Continue`. If you chose a new email, verify the code sent to that inbox too.
5.  Click `Continue to sign in`. Clay signs you out of all current sessions; sign back in with your chosen email and new password.

The same [requirements and troubleshooting guidance](#change-your-account-email-address) applies, including restrictions for organization-managed accounts and what to do if `Change sign-in` is missing.

This change applies only to your individual user account — other users in your workspace are not affected.

Clay accounts support only one of these login methods at a time — either Google OAuth or email + password, not both. After switching, you will no longer be able to sign in with Google on this account.

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

## "Unable to login" error

If you see an **"Unable to login"** error on the Clay login page after entering your email address and password, the most likely cause is that your account was created using **Google authentication** rather than email and password. Clay accounts support only one login method at a time — if your account uses Google, the email and password fields will not work.

To resolve this:

1.  Return to the Clay login page at [app.clay.com](https://app.clay.com).
2.  Enter your email address and click **Continue**.
3.  Click **Continue with Google** instead of entering a password.
4.  Sign in with the Google account associated with your Clay email address.

If you also tried **Forgot password?** and did not receive a reset email, this confirms your account uses Google authentication — password reset emails are not sent for Google-auth accounts because there is no password on the account to reset.

To switch to email and password login instead, see [Switch from Google login to email and password](#switch-from-google-login-to-email-and-password) above for the steps in `Settings` > `Account` > `Security` > `Change sign-in`.

## Clay API key (legacy)

Your Clay API key (legacy) is a personal single-token key that enables Clay-native integrations and some older third-party connections such as Zapier. To manage this key, go to `Settings` > `Account` > `API key (legacy)`.

Your full API key is shown **once** immediately after it is generated or regenerated — copy it from the modal that appears and store it somewhere safe. After you close the modal, only a redacted version is visible in settings and the full key cannot be retrieved without regenerating.

-   **To create or replace your key:** click `Regenerate key`. The new key is shown once in the modal; your previous key is invalidated immediately.

**Note:** This personal key is for Clay-native integrations only. If you need a workspace-scoped key to authenticate with Clay's Public HTTP API, open **API and CLI** in the left sidebar, select the **API keys** tab, and click **Add API key**.

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
