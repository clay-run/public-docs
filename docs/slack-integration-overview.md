---
title: Slack integration
description: Team communication and collaboration platform boosting productivity
  with AI and integrations.
last_synced: 2026-04-26T01:40:41.499Z
---

# Slack integration

Team communication and collaboration platform boosting productivity with AI and integrations.

Slack is a communication platform that enables team collaboration through channels, direct messaging, and file sharing.

With this integration, you can retrieve Slack user information, send messages to channels, and get channel member lists directly from Clay.

## **Enriching data with Slack**

1.  While in a Clay table, click `Add enrichment` and search for `Slack`.
2.  Under `Integrations`, select one of the Slack options.
3.  In the modal, you will be asked to `Select Slack account`.
    -   If you haven't already connected your Slack account, click `+ Add account` and go through authentication.

### `Action` Find Slack user by email

Use this action to find a Slack user based on their email address.

**Inputs**

-   **User email**

### `Action` Send message to channel

Use this action to send messages to Slack channels through a bot directly from Clay.

**Inputs**

-   **Bot name (Optional):** Specify the name of the bot that will post the message.
-   **Emoji (Optional)**
-   **Slack channel**: Enter the name of the Slack channel where you want to post the message.
-   **Message (Optional):** The text body of the Slack notification (e.g., "A new lead has submitted a form"). Supports [Slack markdown](https://api.slack.com/reference/surfaces/formatting#basic-formatting).
-   **Form information (Optional):** Add structured form data to the message (e.g., "First Name → Kareem"). The form will be sorted alphabetically by field name.

> **Note:** Although both **Message** and **Form information** are displayed as optional in the UI, at least one of them must contain content for the action to run. Leaving both fields empty produces the error *"Missing input: You must include data for the person for this action to work."* Fill in the **Message** field with your notification text to resolve this.

### `Action` Find list of channel members

Use this action to retrieve a list of members from a specified Slack channel.

**Inputs**

-   **Slack channel**: Enter the name of the Slack channel (without the #) from which you want to retrieve members (e.g., "fun-and-random").

### `Action` Send for approval to Slack channel

**Inputs**

-   **Slack channel**: Select a public channel from the dropdown. The dropdown lists **public channels only** — private channels do not appear. For a private channel, switch the input to text mode and enter the channel **ID** (for example, `C04F8AWK44T`) instead of the channel name. To find a channel's ID: right-click the channel name in Slack → **Copy link** — the ID (starting with `C`) appears at the end of the copied URL.
-   **Message**

### **Run settings**

-   **Auto-update**
-   **Only run if:** The enrichment will only run if conditions are met. ([Learn more about conditional formulas here!](https://www.clay.com/university/lesson/ai-formulas-conditional-runs-clay-101))

## Permissions & security

When you connect Slack to Clay, Clay requests the following OAuth permissions from your Slack workspace:

**Required scopes** — always requested when connecting:

-   `channels:read` — View the list of public channels and their basic info (name, topic, member count).
-   `groups:read` — View basic info about private channels the Clay bot has been invited to.
-   `chat:write` — Send messages as the Clay bot.

**Optional scopes** — enabled by default, but you can decline them at the OAuth authorization screen:

-   `chat:write.customize` — Post messages with a custom bot name and profile picture. Used by the **Bot name** and **Emoji** inputs on the Send message action.
-   `chat:write.public` — Send messages to public channels the Clay bot has not explicitly joined.
-   `users:read` — Look up Slack users by their user ID.
-   `users:read.email` — Look up Slack users by email address. Required by the **Find Slack user by email** action.

Clay does **not** request access to message history, direct messages, file uploads, or workspace administration settings. Clay does not store or harvest Slack data for its own purposes — these scopes are used solely to execute the actions you configure in your tables.

For full security documentation — including SOC 2 Type II reports, data handling practices, and breach notification policies — visit [trust.clay.com](https://trust.clay.com/).

## Using Markdown with Slack messages

You can add Markdown to any Slack message, either in the Slack integration itself or with the Formula feature.

> **Using column data in your message:** To include values from your table (such as a contact's name or a custom headline) in the **Message** field, use the variable picker in the input field to insert column references. Typing `{{column_name}}` as literal text will not resolve to column values — it will be sent as-is. Alternatively, compose your full message in a Formula column and map that column's output to the **Message** field (steps below).

1.  Click `+ Add column` in the table, then `Formula`.
2.  Write your message (find formatting guidance below).
3.  Go to your Slack message column and set the `Message` input to the message you created.

### Formatting Slack messages

**Text formatting**

-   **Bold:** Put asterisks  around your text.
-   _Italic:_ Use underscores `_` on both sides.
-   Strikethrough: Surround text with tildes `~`.

**Code & blockquotes**

-   Inline code: Wrap it in backticks \`\`\`.
-   Multi-line code block: Enclose the text in triple backticks \`\`\`\`\`.
-   Blockquote: Start the line with a `>` character.

**Lists**

-   **Numbered list:** Start each line with a number and a period.Example:
    1.  First item
    2.  Second item
-   **Bulleted list:** Slack doesn't support bullets directly, but you can use the character (`Option` + `8`) → •
-   Example:
-   • Item one
-   • Item two

**Mentions & notifications**

-   Mention a user: `<@USERID>`
    -   If you want to tag people, you would need their Slack UserID, so you would want to use the enrichment `Find Slack user by email`.
-   Notify everyone: `<!everyone>`
-   Notify active members here: `<!here>`
-   Notify a user group: `<!subteam^GROUPID>`

**Links**

-   Simply pasting a URL will create a clickable link.
-   To display custom link text: use angle brackets, the URL, a pipe `|`, then your text.
-   Example: `<https://clay.com|Explore Clay>` → [Explore Clay](https://clay.com/)

**Emoji**

-   Wrap the emoji name in colons.
-   Example: `:tada:` → 🎉

## Security and permissions

When you connect Slack to Clay, Clay requests a minimal set of OAuth permissions from your Slack workspace. These are scoped to what the integration actually needs — Clay does not request permissions to read message history, send direct messages, or access files.

### Required scopes

These permissions are always requested and are required for Clay's Slack actions to function:

| Scope | What it allows |
|---|---|
| `channels:read` | View the list of public channels in your workspace |
| `groups:read` | View private channels the Clay bot has been invited to |
| `chat:write` | Send messages as the Clay bot |

### Optional scopes (enabled by default)

These permissions are requested by default but can be disabled during the connection flow if your security policy requires it:

| Scope | What it allows | Needed for |
|---|---|---|
| `chat:write.customize` | Set a custom display name and avatar per message | **Bot name** and **Emoji** inputs on Send message |
| `chat:write.public` | Send to public channels without the bot being a member first | Posting to channels the Clay bot hasn't joined |
| `users:read` | View basic profile information about workspace members | Find Slack user by email, Find list of channel members |
| `users:read.email` | View email addresses of workspace members | Find Slack user by email |

### What Clay cannot access

Clay's Slack connection does **not** include permissions to:

-   **Read message history** — no access to past messages in channels, group messages, or direct messages
-   **Send or read direct messages** — no DM access to individual users
-   **Read or upload files** — no file or attachment access
-   **Administer your workspace** — no admin-level or workspace-management permissions

Clay uses these permissions only to execute the workflows you configure. Clay does not harvest or store Slack data for its own purposes. For a comprehensive overview of Clay's security practices, see the [Clay Trust Center](https://trust.clay.com/).

## Troubleshooting

### New channels not appearing in the channel picker

Clay fetches your Slack channel list live each time you open the **Slack channel** dropdown, so newly created channels should appear automatically. If they still don't show up:

1. **Check whether the channel is public or private.**
   - **Public channels** are listed automatically as soon as they exist in your Slack workspace.
   - **Private channels** only appear if the Clay integration bot has been explicitly invited to them. Open the private channel in Slack, go to its member settings, and invite the Clay bot — then reopen the channel dropdown in Clay.

2. **Reconnect your Slack integration** to get a fresh OAuth token. This resolves cases where the token has become stale or lost permissions:
   - Go to **Settings → Connections** in Clay.
   - Find **Slack** in your connections list.
   - Click the **...** menu next to your Slack account and select **Edit**.
   - Re-authenticate your Slack account.

3. **Verify that your Slack connection has the required OAuth scopes.** If you re-authenticate and are prompted for permissions, make sure you grant:
   - `channels:read` — lists public channels
   - `groups:read` — lists private channels the bot has been invited to
   - `chat:write` — sends messages as the Clay bot

### `channel_not_found` error when posting to a private channel

If a Slack action returns `{"ok":false,"error":"channel_not_found"}` when targeting a private channel:

1. **Invite the Clay bot to the channel.** In Slack, open the private channel and type `/invite @Clay`, or add the Clay app through the channel's member settings. The Clay bot must be a member of any private channel it posts to.

2. **Use the channel ID, not the channel name.** The Slack API requires a channel **ID** for private channels — display names are not accepted. A channel ID starts with `C` and looks like `C04F8AWK44T`. To find it: right-click the channel name in Slack → **Copy link** — the ID is the segment at the end of the copied URL.

> **Note for "Send for approval":** The channel dropdown for this action shows only public channels. For a private channel, switch the **Slack channel** input to text mode and enter the channel ID directly.

### My Slack workspace requires admin approval and the Slack Marketplace link shows an error

If your Slack workspace requires admin approval before installing apps, Slack's approval email will tell you to complete the installation from the Slack Marketplace. However, Clay connects to Slack through a direct OAuth flow — it does not install as a Slack Marketplace app. That Marketplace link is a dead end for Clay, and clicking it will show an error.

Once your Slack workspace admin has approved the Clay app, complete the connection from within Clay:

1. Go to **Settings → Connections** in Clay (or, in a table: **Add enrichment → search "Slack" → click + Add account**).
2. Click to connect Slack and authorize.
3. Since your admin already approved Clay, you won't be prompted for workspace approval again — it will connect straight through.

Make sure you are logged into your Slack workspace in the same browser when you do this.

### Bot name or Emoji inputs have no effect

If you've filled in the **Bot name** or **Emoji** fields but the Slack message still arrives under the default Clay bot name and avatar, your Slack connection is most likely missing the `chat:write.customize` scope.

**Why this happens:** The `chat:write.customize` scope is required for Slack to honor a custom bot name and icon per message. This scope is enabled by default when you first connect Slack to Clay — but if you chose reduced permissions during the OAuth flow, it may not have been granted. When the scope is absent, Slack silently sends the message with the default bot identity and ignores the values you set for **Bot name** and **Emoji**.

**To fix it:**

1. Go to **Settings → Connections** in Clay.
2. Find **Slack** in your connections list.
3. Click the **...** menu next to your Slack account and select **Edit**.
4. Re-authenticate your Slack account and make sure to accept the `chat:write.customize` scope when prompted.

After reconnecting with the scope in place, new runs of the **Send message to channel** action will use the custom bot name and emoji you specified.

### Getting an `account_inactive` error from Slack

If Clay returns an error like `{"ok":false,"error":"account_inactive"}` when running a Slack action (such as **Send message to channel** or **Send for approval to Slack channel**), this means the Clay bot user is no longer active in your Slack workspace. This most commonly happens when the Clay app has been uninstalled or deactivated in Slack — for example, by a workspace admin. If you can no longer find the Clay bot in Slack, that confirms the same root cause.

**Why reconnecting in Clay alone doesn't fix this:**
The reconnect flow in Clay starts a fresh OAuth authorization — it does not reuse any existing token. However, OAuth still requires the Clay app to be installed in your Slack workspace. If the app has been removed, even a fresh connection attempt will fail until the app is reinstalled on the Slack side.

**To resolve this:**
1. In Slack, go to **Settings & Administration → Manage Apps** and check whether the Clay app is still listed as installed.
2. If it was removed or restricted by a workspace admin, reinstall it from Slack. If you're not a Slack workspace admin, ask whoever manages apps in your workspace to reinstall the Clay app.
3. Once the Clay app is reinstalled, go to **Settings → Connections** in Clay and reconnect your Slack account.
4. Re-run your Slack action.

### Slack message text shows formatting characters as plain text

If your message content appears with raw formatting syntax — for example, `**Company Name**` displays literally as `**Company Name**` in Slack instead of rendering as bold text — the cause is a syntax mismatch between standard Markdown and Slack's formatting language.

**Why this happens:** Clay sends message text to Slack using Slack's own format, called mrkdwn. Standard Markdown and mrkdwn look similar but differ in important ways. The most common difference is bold text: standard Markdown uses double asterisks (`**bold**`), while Slack's mrkdwn uses a single asterisk on each side (`*bold*`). When you use standard Markdown syntax in a Slack message, Slack renders the literal characters as plain text rather than applying the formatting.

**To fix it:** Use Slack's mrkdwn syntax in your messages. See the [Formatting Slack messages](#formatting-slack-messages) section above for the full reference, or consult the [Slack formatting guide](https://api.slack.com/reference/surfaces/formatting#visual-styles) for the complete specification.
