---
title: Buying email accounts in Clay
description: Protect your domain reputation while scaling cold outreach — buy
  alternative domains and email accounts directly in Clay using Clay credits.
last_synced: 2026-10-20T16:40:27.633Z
---

# Buying email accounts in Clay

Protect your domain reputation while scaling cold outreach — buy alternative domains and email accounts directly in Clay using Clay credits.

Cold outbound often requires sending a high volume of emails to inboxes that may not engage — and over time, that can damage the reputation of the domain you're sending from. Buying email accounts in Clay lets you scale your sending capacity by purchasing alternative domains and email accounts directly with Clay credits, without sacrificing deliverability.

**Available on Growth and Enterprise plans.** Buying email accounts in Clay is available on the Growth and Enterprise plans. On other plans the `Buy managed accounts` option stays visible but locked, with an `Available on Growth+` badge and an `Explore upgrade options` button.

## ‍**Buying email accounts**

From the `Sequencer` homepage, go to the `Email accounts` tab and click `Add email account`. In the `Add email accounts` modal, select `Buy managed accounts` and click `Continue` to open the purchase flow.

1.  **Choose a provider and search for alt domains.** Use the `Gmail` / `Outlook` toggle at the top of the panel to set which provider your new inboxes will run on. Then search for available alternative domains and select the ones you want to add to your order — Clay automatically loads your workspace's company domain as a starting point.
    -   If you aren't sure how many domains to buy, open `How many domains do I need?` and enter a `Weekly sends` target. Clay turns it into a `Domains` count and adds a 5% availability buffer on top.
    -   Selecting a domain adds 5 sender accounts to your order — the maximum per domain.
    -   A single order covers up to 50 domains.
    -   The preview panel on the right shows your current order, including per-domain pricing (yearly) and per-account pricing (monthly).
2.  **Add personas.** Personas map directly to the reps who will manage replies coming into these inboxes.
    -   Each persona has to be linked to a workspace user through `Assign user`, which pulls in that user's name and profile picture. You can edit the first and last name from there, and a profile picture is required.
    -   `Auto-balance personas` is enabled by default and distributes email accounts evenly across personas. Turn it off to assign accounts manually per domain or to customize email prefixes.
3.  **Add contact details.** Enter the registration details that will be attached to the new accounts — email, first and last name, company name, full mailing address, and phone number.
    -   Set your `Forwarding domain` — this is the domain where purchased domains will redirect. Clay recommends using your company's primary domain (e.g., `clay.com`).
4.  **Review your order summary.** The summary shows the total credits you can expect to be charged annually and monthly. Confirm your purchase when you're ready.

![](https://cdn.prod.website-files.com/687e604972375496b891fe58/69c6b5ea48b4f4c966867201_Buying%20Email%20Accounts%20in%20Clay%20\(1\).png)

**Note:** After confirming your purchase, your order appears in the `Account orders` tab (`Sequencer → Account orders`) with a **Pending fulfillment** status — this is expected and means the order is being processed. Email accounts typically arrive within a few hours but may take up to 72 hours to be provisioned. Once they appear in your `Email Accounts` tab, warmup is automatically enabled — see [Ramping up new accounts](#ramping-up-new-accounts) for when you can start sending.

## **Ramping up new accounts**

**Automatic ramp-up for purchased accounts is currently rolling out and may not be enabled in your workspace yet.**

With automatic ramp-up, you can send from purchased accounts the day they arrive. Clay raises each account's daily send limit on a fixed schedule as the inbox ages, starting at 3 emails a day and reaching full capacity at 20. Day 1 is the day the order was fulfilled.

The following table shows the daily send limit for a purchased account at each inbox age:

| Inbox age | Daily send limit |
| --- | --- |
| Days 1 to 3 | 3 per day |
| Days 4 to 6 | 4 per day |
| Days 7 to 9 | 6 per day |
| Days 10 to 12 | 9 per day |
| Days 13 to 15 | 12 per day |
| Days 16 to 18 | 15 per day |
| Days 19 to 20 | 18 per day |
| Day 21 onward | 20 per day |

While a purchased account is below 20 emails a day, it shows a `Warming` badge in the `Email accounts` tab. Once it reaches 20, the badge changes to `Warm`.

With automatic ramp-up, `Update send limit` is greyed out for purchased accounts, in both the row's actions menu and the bulk actions menu, because Clay manages these limits for you. If you update the send limit across a mix of purchased and connected accounts, Clay applies the change to the connected accounts and tells you how many it skipped.

If automatic ramp-up isn't enabled for your workspace yet, purchased accounts show a `Warming` badge during their first 3 weeks and `Ready` after that, and you can change their limit with `Update send limit`. Allow 3 weeks of warmup before using them in campaigns.

## **Managing your orders**

Every purchase of email accounts gets its own row on the `Account orders` tab of the `Sequencer` homepage, one row per order. The `Status` column tracks where each order stands:

-   `Placing order` and `Pending fulfillment` — the order is going through, and the accounts aren't ready to use yet.
-   `Active` — the accounts are provisioned and waiting in your `Email accounts` tab.
-   `Failed fulfillment`, `Failed activation`, and `Billing failed` — the order didn't complete.
-   `Canceled` — the order was cancelled and its accounts removed.

Each order row also shows `Next billing`, the date of the next monthly charge, and `Lifetime payments`, the credits the order has cost you so far. Expand a row to see its `Status history` and `Payment history`.

To end an order, use `Cancel order` in the row's actions menu. `Cancel order` stops recurring billing and removes all of the order's email accounts immediately. If your workspace uses credit budgets, that menu also offers `Change budget`, which points the order's future charges at a different `Budget`.

## **FAQs**

### **What does "Pending fulfillment" mean?**

After placing an order, you can track its progress in the `Account orders` tab (`Sequencer → Account orders`). **Pending fulfillment** is the expected status shown while your accounts are being provisioned — it means your payment was processed and Clay is working to set up your accounts. Once complete, the status changes to **Active** and the accounts appear in your `Email Accounts` tab.

### **Can I add more email accounts to a domain after I've purchased it?**

No. Once a domain is purchased, you cannot add additional email accounts to it. Select your desired number of accounts (up to 5 per domain) before confirming your order.

### **What happens if I cancel a domain before the year is up? Will I get a refund?**

Clay does not offer partial refunds for domains cancelled before the end of their yearly billing period. Cancelling with `Cancel order` stops the recurring charge going forward, and remaining subscription days aren't refunded.

### **What happens if I delete one email account within a domain?**

Deleting a single email account from a domain will delete **all** email accounts in that domain. Proceed with caution.

The confirmation dialog lists every address that will be removed and asks you to acknowledge the total before it goes ahead. Deletion is permanent for purchased accounts — unlike accounts you connected yourself, they can't be re-added afterwards.

### **How are credit costs calculated?**

Credit costs are calculated using your workspace's cost-per-credit (CPC) against target prices of **$4.50/account/month** and **$15/domain/year**.

### **Are purchased domains pre-warmed?**

No. Purchased accounts are not pre-warmed when they arrive. Warmup is automatically enabled during provisioning — see [Ramping up new accounts](#ramping-up-new-accounts) for when you can start sending from them.

### **Do I need to warm up purchased accounts myself?**

No — and you won't find warmup controls for purchased accounts. Clay enables warmup on purchased accounts when it provisions them and owns it from then on, so the warmup settings in the `Email accounts` tab apply only to accounts you connected yourself.

### **What does Clay manage for purchased email accounts?**

For email accounts purchased directly through Clay, Clay manages the core sending infrastructure for you, including:

-   Provisioning the sending domains and mailboxes
-   Configuring DNS and email authentication, including SPF, DKIM, and DMARC
-   Automatically enabling warmup during provisioning
-   Monitoring domain deliverability and mailbox reputation — visible as the **Reputation** percentage next to each account in `Sequencer → Email Accounts`

As with any outbound email program, deliverability also depends on factors such as list quality, sending volume, bounce rates, and recipient engagement.

### **How do I change the sender name or other details on a purchased email account?**

From `Sequencer → Email Accounts`, find the mailbox you want to edit. Click the **⋯** button on the far right of the account row, select **Update sender variables**, and update the **From name** (the sender display name shown to recipients), **Signature**, or any custom sender variables your workspace has configured. Click **Save** to apply the changes.

### **Can I change the email address of a provisioned mailbox?**

No. The email address assigned to each mailbox at purchase (for example, `d.henriksen@cyberarkoselabs.com`) is permanent and cannot be changed after provisioning. You can update display-level details such as the **From name** and **Signature** using **Update sender variables** — see [How do I change the sender name or other details on a purchased email account?](#how-do-i-change-the-sender-name-or-other-details-on-a-purchased-email-account) for those steps — but the underlying email address is fixed.

If you need a different email address, purchase a new domain and select the desired email prefix during checkout.

### **Where are the purchased email accounts from?**

Clay fulfills orders through Smartlead, which in turn uses Zapmail to provision and manage the email accounts.

### **How can I look up the rep's details for a purchased account?**

Use the **Get rep data** enrichment in a Clay table. Provide the SmartSender account email address as the input — the action returns the rep's email address and full name (when available). This is useful for personalizing campaign messages with the sender's name.

### **Why does my sender's name appear with extra characters in Outlook?**

If a persona's first name is fewer than 4 characters (for example, "Sam"), Outlook recipients may see the name padded to 4 characters (for example, "Sama"). Zapmail, the email provisioning provider behind purchased Clay email accounts, requires all account sender names to be at least 4 characters long. Because Outlook does not allow the sender display name on a provisioned account to be updated after creation, the padded name persists for Outlook recipients.

Gmail and other email clients are not affected — they display the sender name exactly as entered in Clay.

To ensure the sender name appears as expected across all inboxes, use a first name of 4 or more characters when setting up personas for purchased email accounts.

### **Can I provision Clay inboxes on a domain I already own?**

No. The **Buy managed accounts** flow can only provision inboxes on new domains purchased through Clay — it cannot attach inboxes to a domain you already own.

If you want to send from an existing domain, create the mailbox through Google Workspace or Microsoft 365 and connect it to Clay under **Sequencer → Email Accounts** using Google OAuth, Microsoft Outlook OAuth, or SMTP. See the [Email sequencer guide](email-sequencer.md) for connection instructions.

### **Can I use email aliases (like name+eventname@example.com) to scale my sending?**

No. An alias such as `name+eventname@example.com` routes to the same underlying mailbox as your primary address — it is not a separate mailbox. Because aliases share the same inbox, they do not provide independent sending reputation, daily send capacity, or warmup. Using multiple aliases does not increase your total daily throughput or protect your primary domain's reputation the way separate mailboxes do.

To scale your campaign sending capacity, buy additional email accounts directly in Clay using the **Buy managed accounts** flow described above, or connect additional mailboxes via Google OAuth, Microsoft Outlook OAuth, or SMTP. Each connected account has its own independent daily sending budget and sender reputation. See the [Email sequencer guide](email-sequencer.md) for connection options.
