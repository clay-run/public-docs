---
title: AgentMail integration
description: Use AgentMail with Clay to capture inbound emails as table rows in real time and draft or send replies directly from your workflows.
last_synced: 2026-07-07T19:36:40.211Z
---

# AgentMail integration

Use AgentMail with Clay to capture inbound emails as table rows in real time and draft or send replies directly from your workflows.

AgentMail is a programmable email infrastructure tool that gives AI agents and workflows a real, dedicated inbox — a live email address that can receive, draft, and send mail through an API. With this integration, you can use an AgentMail inbox as a real-time source in Clay and run actions to create drafts or send replies directly from your table.

**Note:** This integration is bring-your-own-API-key. Before connecting AgentMail to Clay, you need an AgentMail account with a verified domain, at least one inbox, and an API key. See the setup steps below.

## **Setting up AgentMail**

Complete the following steps in your AgentMail account before connecting to Clay.

1.  Sign up at [**agentmail.to**](https://agentmail.to/) and open the dashboard.
2.  **Add a domain.** In the AgentMail dashboard, add the domain or subdomain you want to send and receive from. AgentMail will generate DNS records (MX, SPF, DKIM, DMARC) for you to add to your domain manager.
    -   If your root domain already receives mail through Gmail (Google Workspace) or Outlook (Microsoft 365), its MX records already point to that provider. A domain's MX records can only point to one mail server, so you cannot also route it to AgentMail. Use a dedicated subdomain instead (e.g., `inbox.yourdomain.com`).
3.  **Add the DNS records.** Copy the records AgentMail generates into your domain manager exactly as shown — type, name/host, and value. DNS propagation can take a few minutes to a few hours. Once the records are in place, click `Verify Domain` in the AgentMail dashboard.
4.  **Create an inbox.** Once your domain is verified, create one or more inboxes (e.g., `sales@inbox.yourdomain.com`). This is the live address Clay will listen to.
5.  **Generate an API key.** In the AgentMail dashboard, generate an API key. This is the only credential you need to connect AgentMail to Clay.

For more detail on domain configuration, see [**AgentMail's custom domains guide**](https://docs.agentmail.to/custom-domains).

## **Creating a table with AgentMail**

1.  In a workbook, click `+ Add` at the bottom.
2.  Search for **AgentMail** and select it from the results.
3.  In the modal, you will be asked to `Select AgentMail account`.
    -   If you haven't already connected your AgentMail account, click `+ Add account` and enter the API key you generated.

### `Source` Import AgentMail message events

Imports a new row into your Clay table each time a selected message event fires in one of your AgentMail inboxes.

**Note:** Adding this source automatically creates a webhook in your AgentMail account — you don't need to configure one manually. The webhook will appear in your AgentMail dashboard subscribed to the inboxes and events you selected.

**Inputs**

-   **Forward messy GTM signals into Clay:** Forward newsletters, funding alerts, event attendee lists, or job-change emails to an AgentMail inbox. Each email lands as a new row, where Clay can enrich the people or companies and route them into the right workflow.
-   **Capture inbound replies from outbound campaigns:** When a prospect replies to an outbound sequence, AgentMail captures the response as a new row so Clay can classify it (positive, not interested, OOO, referral) and trigger next steps.
-   **CC an agent on live deal threads:** CC an AgentMail inbox on an active prospect or customer thread. Incoming messages appear as rows in Clay, where you can track context, surface relevant signals, or prepare follow-ups.
-   **Email-native meeting prep:** Forward a prospect or customer thread to an AgentMail inbox and have Clay generate an enriched account brief — company context, stakeholders, recent signals, and suggested talking points.
-   **Lightweight GTM command inbox:** A rep or operator emails a simple request (e.g., "enrich these companies" or "find similar accounts") to an AgentMail inbox. The message lands in Clay as a new row to kick off the enrichment workflow.

**Note:** Adding this source automatically creates a webhook in your AgentMail account — you don't need to configure one manually. The webhook will appear in your AgentMail dashboard subscribed to the inboxes and events you selected.

**Inputs**

-   Inboxes: The AgentMail inbox or inboxes to subscribe to. Displays as a dropdown populated from your AgentMail account. A single source can subscribe to up to 10 inboxes.
-   Message events: The event types that will trigger a new row. You can select a single event type or all of them. See [**AgentMail's webhook events reference**](https://docs.agentmail.to/api-reference/webhooks/create) for the full list of available events.

Each new row includes the full message payload from AgentMail — including fields such as subject, body text, sender, recipient, and timestamp. See [**AgentMail's events reference**](https://docs.agentmail.to/events) for the complete payload structure.

## **Enriching data with AgentMail**

1.  While in a Clay table, click `Add enrichment` and search for **AgentMail**.
2.  Under `Integrations`, select one of the AgentMail actions.
3.  In the modal, you will be asked to `Select AgentMail account`.
    -   If you haven't already connected your AgentMail account, click `+ Add account` and enter your API key.

### `Action` Create draft

Creates a draft email in an AgentMail inbox without sending it.

**Use cases:**

-   **Human-in-the-loop reply review:** After Clay classifies an inbound reply or generates a personalized response, stage it as a draft in AgentMail so a rep can review and send it manually — keeping a person in the loop before anything goes out.
-   **Email-native meeting prep:** Have Clay draft an enriched account brief reply and stage it as a draft so the rep can send it when ready.
-   **GTM command inbox responses:** When a rep emails a request to the inbox, use Clay to run the enrichment and draft the response back to them for review.

**Inputs**

Required:

-   Inbox ID: The AgentMail inbox where the draft should be created. At least one of the following optional fields must also be provided: To, CC, BCC, Subject, Plain text body, or HTML body.

Optional:

-   To: Comma-separated recipient email address or addresses.
-   CC: Comma-separated CC recipient address or addresses.
-   BCC: Comma-separated BCC recipient address or addresses.
-   Reply-to: Comma-separated reply-to address or addresses.
-   Subject: Subject line for the draft.
-   Plain text body: Plain text body for the draft. (Required if HTML body is not provided.)
-   HTML body: HTML body for the draft. (Required if Plain text body is not provided.)
-   In reply to: AgentMail message ID that this draft replies to, used to thread the draft into an existing conversation.
-   Send at: Scheduled send time for the draft, in ISO 8601 format.
-   Client ID: A client-defined identifier for the draft.
-   Labels: Comma-separated labels to apply to the draft.

**Outputs**

-   Draft ID: The unique ID of the created draft.
-   Thread ID: The ID of the thread the draft belongs to.
-   Inbox ID: The ID of the inbox where the draft was created.
-   Send status: The current send status of the draft (e.g., `scheduled`).
-   Send at: The scheduled send time, if set.
-   Created at: Timestamp when the draft was created.
-   Updated at: Timestamp when the draft was last updated.
-   Preview: A short preview of the draft body.
-   Subject: The subject line of the draft.
-   Plain text body: The plain text body of the draft.
-   HTML body: The HTML body of the draft.
-   Client ID: The client-defined identifier, if set.
-   In reply to: The message ID this draft is threaded to, if set.
-   Labels: Labels applied to the draft.

### `Action` Reply to message

Sends a reply to an existing message in an AgentMail inbox.

**Use cases:**

-   **Automated reply routing:** After Clay classifies an inbound reply as positive, an OOO, or a referral, automatically send the appropriate follow-up response without manual intervention.
-   **Agent-assisted deal threads:** When an AgentMail inbox is CC'd on a live prospect thread, use Clay to enrich context and have the agent send a reply with suggested next steps or a meeting link.
-   **GTM command inbox responses:** Automatically send enrichment results back to the rep who emailed the request — closing the loop without anyone leaving their inbox.

**Inputs**

Required:

-   Inbox ID: The AgentMail inbox that contains the message to reply to.
-   Message ID: The ID of the AgentMail message to reply to.
-   Plain text body: Plain text body for the reply. (Required if HTML body is not provided.)
-   HTML body: HTML body for the reply. (Required if Plain text body is not provided.)

Optional:

-   Reply all: Toggle to reply to all recipients of the original message.
-   To: Comma-separated recipient address or addresses.
-   CC: Comma-separated CC recipient address or addresses.
-   BCC: Comma-separated BCC recipient address or addresses.
-   Reply-to: Comma-separated reply-to address or addresses.
-   Labels: Comma-separated labels to apply to the reply.
-   Headers: Custom headers for the reply.

**Outputs**

-   Message ID: The ID of the sent reply message.
-   Thread ID: The ID of the thread the reply belongs to.

### **Run settings**

-   **Auto-update:** When enabled, the action re-runs automatically whenever its input values change.
-   **Only run if:** The enrichment will only run if conditions are met. [**Learn more about conditional formulas here.**](https://www.clay.com/university/lesson/ai-formulas-conditional-runs-clay-101)

## **Troubleshooting**

### **Domain won't verify**

Double-check each DNS record against what AgentMail shows in the dashboard. A common mistake is entering the full subdomain in the host field when your domain manager auto-appends the domain (e.g., entering `inbox.yourdomain.com` instead of just `inbox`). DNS propagation can take a few minutes to a few hours. Once records are in place, click `Verify Domain` again in the AgentMail dashboard. See [**AgentMail's custom domains guide**](https://docs.agentmail.to/custom-domains) for step-by-step instructions.

### **Can't add my root domain — mail conflict**

If your root domain already receives mail through Gmail (Google Workspace) or Outlook (Microsoft 365), its MX records point to that provider exclusively. A domain's MX records can only route incoming mail to one server, so you can't simultaneously route it to AgentMail. Use a dedicated subdomain (e.g., `inbox.yourdomain.com`) or a separate domain instead.

### **No rows appearing in Clay**

Confirm the source is subscribed to the correct inbox and to the expected event types. Send a test email to the inbox to trigger a new event. Also check that your API key is valid — if it was regenerated in AgentMail, re-authenticate in Clay by removing the existing account connection and adding it again.

### **Sent or delivered events not appearing**

Ensure the source is configured to listen to those event types — selecting all events is the simplest option. Also confirm the reply action ran successfully before expecting delivery events, since those events only surface after a message has actually been sent.

### **API key connection failure**

If the connection fails, verify the key is current in your AgentMail dashboard. If you've regenerated your key since first connecting, remove the existing AgentMail account in Clay and re-authenticate with the new key.
