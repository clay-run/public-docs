---
title: AgentMail integration
description: Connect an email inbox to a Clay table using AgentMail's Inbox-as-a-source integration — receive, enrich, and reply to emails entirely within Clay.
---

# AgentMail integration

AgentMail is a third-party service that gives AI agents real email inboxes. The Clay–AgentMail integration lets you use an email inbox as a Clay table source, so incoming emails arrive as rows in real time. Once a message is a row, you can enrich the sender, run Claygent to classify or draft a response, and send a reply — all from the same table.

**What this integration enables:**

- **Inbox as a source:** Incoming emails flow into a Clay table as rows the moment they land.
- **Enrich and qualify:** Run any Clay enrichment on the sender (company, title, LinkedIn profile, etc.) directly from the row.
- **Draft and send replies:** Use Claygent to compose a response and send it from the same inbox — with or without human review.

## Prerequisites

Before connecting AgentMail to Clay, you need:

1. An **AgentMail account** — sign up at [agentmail.to](https://www.agentmail.to).
2. A **domain or subdomain pointed at AgentMail** (via DNS MX records). If your root domain already runs Gmail or Outlook, use a subdomain like `inbox.yourdomain.com` to avoid disrupting existing mail.
3. At least one **inbox created** in your AgentMail dashboard.
4. An **AgentMail API key** generated from your AgentMail dashboard.

## Setting up AgentMail (one-time)

### Step 1: Point a domain at AgentMail

In your AgentMail dashboard, add your domain or subdomain. AgentMail generates the DNS records for you — paste them into your DNS provider and click **Verify**. AgentMail manages the MX records to get real-time access to incoming and outgoing mail on that domain.

**Use an isolated domain or subdomain.** Because AgentMail manages MX records, it is best to give it a dedicated domain or subdomain rather than your primary business domain, to avoid interfering with your existing email setup.

### Step 2: Create an inbox

Once the domain is verified, create an inbox address (for example, `sales@inbox.yourdomain.com`) in your AgentMail dashboard. You can create multiple inboxes for different workflows. Clay can listen to up to 10 inboxes per source.

### Step 3: Generate an API key

From your AgentMail dashboard, generate an API key. Copy it — you will need it when adding the source in Clay.

## Connecting AgentMail to Clay

1. In a Clay workbook, click **+ Add** to create a new table, or open an existing table and click **Tools → Import**.
2. Search for **AgentMail** and select **Import AgentMail message events**.
3. Paste your AgentMail API key and authenticate.
4. Select the inboxes you want Clay to listen to (up to 10 per source).
5. Choose which event types to capture — at minimum, select incoming mail events.
6. Click **Submit**. Clay creates the webhook on the AgentMail side automatically.
7. Send a test email to your inbox and watch a new row appear in real time.

Each incoming email becomes one row in the table, with the sender address, subject, body, and timestamps available as columns.

## Available actions

After connecting AgentMail as a source, you can add action columns to respond to emails from within the same table.

### Create draft

Stages a reply in the AgentMail inbox for human review before sending. Use this when you want a person to approve the response — for example, when Claygent has drafted a reply and you want a rep to confirm before it goes out.

**Inputs:**

- **Thread ID** — the thread to reply to (available from the source row data).
- **Body** — the reply text. Reference a Claygent or Use AI column to populate this dynamically.

### Reply

Sends a reply immediately from the same inbox, without a draft review step. Use this for fully automated responses — for example, an out-of-office acknowledgement or a routing confirmation.

**Inputs:**

- **Thread ID** — the thread to reply to.
- **Body** — the reply text (plain text or HTML).

Both actions run per row, so you can trigger them manually for individual rows or set them to fire automatically using run conditions.

## Example workflows

### Reply-based outbound qualification

A prospect replies to an outbound campaign. AgentMail captures the reply as a new row in Clay. Claygent reads the body, classifies it (interested, not interested, out of office, referral), enriches the account, and drafts a response. A rep approves the draft and sends it using the **Create draft** action.

### Speed-to-lead from inbound forms

A lead submits a web form that sends an email to your AgentMail inbox. The email arrives as a row in Clay. Clay enriches the sender's company, scores the lead, and — if they meet your ICP criteria — Claygent drafts a personalized reply that is sent automatically using the **Reply** action.

### CC an agent into a live deal thread

Add an AgentMail inbox address as a CC on an active customer email thread. AgentMail routes each message into Clay as a row, where Claygent can track context, suggest follow-up actions, or draft a reply for rep review.

## Limits

| Limit | Value |
|---|---|
| Inboxes per source | 10 |

You can create multiple AgentMail sources in the same table (subject to Clay's 20-source-per-table limit) to listen to more than 10 inboxes.

## Further reading

- AgentMail setup docs: [docs.agentmail.to](https://docs.agentmail.to)
- AgentMail blog post on the Clay integration: [agentmail.to/blog/email-is-now-a-column-in-clay](https://www.agentmail.to/blog/email-is-now-a-column-in-clay)
- Clay sources overview: [Sources](sources.md)
- Sending automated responses: [Claygent](ai-in-clay.md)
