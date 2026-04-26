---
title: Slack integration
source_url: https://university.clay.com/docs/slack-integration-overview
last_synced: 2026-04-26T01:40:41.499Z
upstream_hash: 3f6e0fed934fc93751fb1dd26b5e1784880c9296c00f370562d2c86c5f184c69
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
-   **Summary (Optional):** Text at the beginning of the message (e.g., "A new response has been submitted"). This field supports markdown.
-   **Form information (Optional):** Add structured form data to the message (e.g., "First Name → Kareem"). The form will be sorted alphabetically by field name.

### `Action` Find list of channel members

Use this action to retrieve a list of members from a specified Slack channel.

**Inputs**

-   **Slack channel**: Enter the name of the Slack channel (without the #) from which you want to retrieve members (e.g., "fun-and-random").

### `Action` Send for approval to Slack channel

**Inputs**

-   **Slack channel**: Enter the name of the Slack channel (without the #) from which you want to retrieve members (e.g., "fun-and-random").
-   **Message**

### **Run settings**

-   **Auto-update**
-   **Only run if:** The enrichment will only run if conditions are met. ([Learn more about conditional formulas here!](https://www.clay.com/university/lesson/ai-formulas-conditional-runs-clay-101))

## Using Markdown with Slack messages

You can add Markdown to any Slack message, either in the Slack integration itself or with the Formula feature.

1.  Click `+ Add column` in the table, then `Formula`.
2.  Write your message (find formatting guidance below).
3.  Go to your Slack message column and set the `Message` input to the message you created.

### Formatting Slack messages

**Text formatting**

-   **Bold:** Put asterisks  around your text.
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
-   **Bulleted list:** Slack doesn’t support bullets directly, but you can use the character (`Option` + `8`) → •
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
