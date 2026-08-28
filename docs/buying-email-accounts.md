---
title: Buying email accounts in Clay
description: Protect your domain reputation while scaling cold outreach — buy
  alternative domains and email accounts directly in Clay using Clay credits.
last_synced: 2026-04-26T01:39:42.909Z
---

# Buying email accounts in Clay

Protect your domain reputation while scaling cold outreach — buy alternative domains and email accounts directly in Clay using Clay credits.

Cold outbound often requires sending a high volume of emails to inboxes that may not engage — and over time, that can damage the reputation of the domain you're sending from. Buying email accounts in Clay lets you scale your sending capacity by purchasing alternative domains and email accounts directly with Clay credits, without sacrificing deliverability.

**Available on Growth and Enterprise plans — currently in beta.** Free plan workspaces cannot purchase domains or email accounts in Clay. To request access, contact Clay support.

## ‍**Buying email accounts**

From the `Campaigns` homepage, go to the `Email Accounts` tab and click `Add Email Accounts`. Select `Buy email accounts` to open the purchase flow.

1.  **Search for alt domains.** Clay automatically loads your workspace's company domain as a starting point. Search for available alternative domains and select the ones you want to add to your order.
    -   Each domain supports up to 5 email accounts.
    -   The preview panel on the right shows your current order, including per-domain pricing (yearly) and per-account pricing (monthly).
2.  **Add personas.** Personas map directly to the reps who will manage replies coming into these inboxes.
    -   Each persona requires a first name, last name, and profile picture to appear as realistic as possible.
    -   **Auto-balance** is enabled by default and distributes email accounts evenly across personas. Turn it off to assign accounts manually per domain or to customize email prefixes.
3.  **Add contact details.** Enter the contact details that will be attached to the generated Google Workspace.
    -   Set your **forwarding domain** — this is the domain where purchased domains will redirect. Clay recommends using your company's primary domain (e.g., `clay.com`).
4.  **Review your order summary.** The summary shows the total credits you can expect to be charged annually and monthly. Confirm your purchase when you're ready.

![](https://cdn.prod.website-files.com/687e604972375496b891fe58/69c6b5ea48b4f4c966867201_Buying%20Email%20Accounts%20in%20Clay%20\(1\).png)

**Note:** After confirming your purchase, your order appears in the `Account orders` tab (`Campaigns → Account orders`) with a **Pending fulfillment** status — this is expected and means the order is being processed. Email accounts typically arrive within a few hours but may take up to 72 hours to be provisioned. Once they appear in your `Email Accounts` tab, warm them up for approximately two weeks before use — purchased domains are not pre-warmed.

## **FAQs**

### **What does "Pending fulfillment" mean?**

After placing an order, you can track its progress in the `Account orders` tab (`Campaigns → Account orders`). **Pending fulfillment** is the expected status shown while your accounts are being provisioned — it means your payment was processed and Clay is working to set up your accounts. Once complete, the status changes to **Active** and the accounts appear in your `Email Accounts` tab.

### **Can I add more email accounts to a domain after I've purchased it?**

No. Once a domain is purchased, you cannot add additional email accounts to it. Select your desired number of accounts (up to 5 per domain) before confirming your order.

### **What happens if I cancel a domain before the year is up? Will I get a refund?**

Clay does not offer partial refunds for domains cancelled before the end of their yearly billing period.

### **What happens if I delete one email account within a domain?**

Deleting a single email account from a domain will delete **all** email accounts in that domain. Proceed with caution.

### **How are credit costs calculated?**

Credit costs are calculated using your workspace's cost-per-credit (CPC) against target prices of **$4.50/account/month** and **$15/domain/year**.

### **Are purchased domains pre-warmed?**

No. You must still warm up purchased domains for approximately two weeks after provisioning before using them in campaigns.

### **How many emails should I send from each inbox per day?**

For best deliverability, send no more than approximately 20 emails per inbox per day — about 600 emails per inbox per month. Sending cold outreach at higher volumes before inboxes are established can trigger spam filters and damage your sender reputation. Clay does not enforce a per-inbox daily send limit; this is a best-practice recommendation for cold outreach.

### **Where are the purchased email accounts from?**

Clay fulfills orders through Smartlead, which in turn uses Zapmail to provision and manage the email accounts.

### **How can I look up the rep's details for a purchased account?**

Use the **Get rep data** enrichment in a Clay table. Provide the SmartSender account email address as the input — the action returns the rep's email address and full name (when available). This is useful for personalizing campaign messages with the sender's name.

### **Can I provision Clay inboxes on a domain I already own?**

No. The **Buy email accounts** flow can only provision inboxes on new domains purchased through Clay — it cannot attach inboxes to a domain you already own.

If you want to send from an existing domain, create the mailbox through Google Workspace or Microsoft 365 and connect it to Clay under **Campaigns → Email Accounts** using Google OAuth, Microsoft Outlook OAuth, or SMTP. See the [Email sequencer guide](email-sequencer.md) for connection instructions.
