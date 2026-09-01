---
title: Connect your own email accounts
description: How to connect Google Workspace, Microsoft 365, or SMTP mailboxes you already own as sending accounts for Clay campaigns.
last_synced: 2026-09-01T03:30:29.936Z
---

# Connect your own email accounts

Connect email accounts you already own — Google Workspace, Microsoft 365, or any mailbox that supports SMTP — and use them as sending accounts for your campaigns.

Clay can sell you managed sending accounts, and it can also send from mailboxes you already own. Bringing your own accounts means you keep the domain, the DNS, and the mailboxes, and you connect each one to Clay once. Two paths cover almost everything: OAuth for Google Workspace and Microsoft 365, and SMTP for other providers or for migrating a batch of accounts in one go.

**Note:** Campaigns send through Clay's email integration partner, Smartlead, so the credentials you connect are shared securely with Smartlead. Accounts you connect sit at the workspace level, which means any campaign in the workspace can select them as senders. The connection modal links both the Smartlead privacy policy and Clay's trust center if you want the detail on how that data is handled.

## When to bring your own

Two situations make connecting your own accounts the right call:

-   Sending from your real main domain — a good fit when the people you're writing to already recognize your company, and worth watching closely on bounce and spam rates.
-   Migrating mailboxes you already bought from another vendor, so you can keep using accounts that are already warmed and paid for.

Bringing your own accounts also means the surrounding infrastructure stays with you. DNS records (SPF, DKIM, and DMARC), the warmup decision, and domain-level health are yours to manage, because Clay doesn't control the accounts.

Domain deliverability monitoring is available for accounts purchased through Clay. For your own accounts, keep an eye on the bounce rate in campaign analytics and keep daily volume conservative per mailbox. [Deliverability and domain health](https://university.clay.com/docs/sequencer-deliverability) covers the numbers to watch and where to find them.

| Method | Best for | Admin authorization |
| --- | --- | --- |
| Gmail (OAuth) | Google Workspace mailboxes on a domain you administer | Yes — once per Workspace |
| Outlook (OAuth) | Microsoft 365 mailboxes on a domain you administer | Yes — once per organization |
| Manual SMTP setup | A single mailbox on any provider that supports SMTP and IMAP | No |
| Bulk CSV upload | Migrating many mailboxes you already bought elsewhere | No |

Every method starts in the same place:

1.  Open `Campaigns` in the sidebar and go to the `Email accounts` tab.
2.  Click `Add email account`.
3.  Under `How do you want to set up your sending accounts?`, choose `Bring your own accounts`, then click `Continue`.
    -   This step only appears if managed accounts are enabled for your workspace. If they aren't, the modal opens straight to the list of connection methods and you can skip it.
    -   If managed accounts are enabled but your plan doesn't include them, `Buy managed accounts` appears locked with an `Available on Growth+` prompt, and `Bring your own accounts` is already selected for you.
4.  On the `Connect your email accounts` step, select a method and click `Continue`.

## Connect with Google OAuth

Before the first mailbox on a domain can connect, a Google Workspace admin authorizes the Clay Sequencer app in the Admin panel. It's a one-time step per Workspace, so if a colleague has already done it for your domain, go straight to connecting the account.

1.  Select `Gmail (OAuth)` and click `Continue`.
2.  On `Is your Google Workspace already configured?`, pick the answer that matches your situation.
    -   `Yes, it's already set up` — the app was authorized previously, and clicking `Continue` takes you to sign-in.
    -   `No, I need to configure it now` — reveals the admin steps below. You'll need Workspace admin access, and the modal also links a video walkthrough.
3.  In the `Search for Clay Sequencer` step, copy the Clay Sequencer Client ID with the copy button next to it. Your admin needs it to find the app.

### Authorize the Clay Sequencer app in Google Workspace

1.  Open your Google Workspace Admin panel — the modal links directly to it — and go to `Security` → `API Controls` → `App Access Control`.
2.  Click `Configure new app`.
3.  Paste the Client ID into the search bar and click `Search`.
4.  Select `Clay Sequencer (Web)` from the results.
5.  Choose which organizational units the authorization covers — either `All in [your org] (all users)` or the specific units holding the domains you want to send from — then click `Continue`.
6.  Under Access to Google Data, select `Trusted`, then click `Continue`.
7.  Review the summary and click `Finish`.

Google can take up to 24 hours to apply the change across the Workspace. If a connection attempt returns an access-denied error in that window, the authorization is fine — it just hasn't reached every account yet, so wait and try again.

If connecting still fails more than 24 hours after your admin finished, reach out through the `Help` button with the address you're trying to add and Clay support can look into it.

### Connect the account

1.  Back in the modal, click `Continue` to reach the `Connect your email account` step.
2.  Decide who can see the account using the `Only show to me and workspace admins` toggle. On — the default — means `This email account will only be visible to you and workspace admins`; switching it off means `This email account will be visible to all workspace editors`.
3.  Click `Connect your Google account`, sign in, and grant access.
4.  The last step is `Enable email warming to improve deliverability`. The accounts you just added are listed with warmup already checked, so clicking `Enable warming` turns it on for all of them. Unchecking every account changes that same button to `Continue without warming`. [Email warmup](https://university.clay.com/docs/email-warmup) builds sender reputation before you send at volume, so leaving it on is the recommendation for almost every account.

## Connect with Microsoft OAuth

Microsoft follows the same shape, with one difference: instead of configuring the app in an admin console, Clay generates an admin consent URL for you to pass to your Microsoft 365 admin. Consent is granted once for the whole organization.

1.  Select `Outlook (OAuth)` and click `Continue`.
2.  On `Is your Microsoft 365 already configured?`, choose `Yes, it's already set up` or `No, I need to configure it now`.
3.  Under `Copy the admin consent URL`, copy the URL Clay has generated.
4.  `Share with your admin` — send the URL to whoever administers your Microsoft 365 tenant.
5.  `Admin grants consent` — the admin opens the URL and grants consent on behalf of the organization.
6.  Click `Continue`, set the `Only show to me and workspace admins` toggle, then click `Connect your Microsoft account` and sign in.
7.  Finish on the `Enable email warming to improve deliverability` step — the same last screen as the Google path, and the same choice between `Enable warming` and `Continue without warming`.

If the consent page returns a server error, that's usually a temporary hiccup rather than a sign the consent failed. Try connecting through OAuth anyway — and if the connection doesn't go through either, have your admin open the URL again a few minutes later.

## Connect via SMTP

SMTP is the most hands-on of the four methods and the one to reach for when OAuth isn't an option: a provider without an OAuth path, or a batch of mailboxes you're migrating in. There's no admin authorization step, because you supply the mail server details and credentials yourself. Where Google or Microsoft OAuth is available, it's the easier route.

### Add one account manually

1.  Select `Manual SMTP setup` and click `Continue`.
2.  Fill in the `SMTP settings` and `IMAP settings` sections with the fields below.
3.  Click `Add account`, then choose whether to enable warmup on the `Enable email warming to improve deliverability` step.

| Section | Field | What goes in it |
| --- | --- | --- |
| SMTP settings (sending) | Sender name | The sender name recipients see |
| SMTP settings (sending) | Sender email | The address campaigns send from |
| SMTP settings (sending) | Username | The username the mail server expects, often the address itself |
| SMTP settings (sending) | Password | The mail server password, or an app password for Gmail mailboxes |
| SMTP settings (sending) | SMTP host | Your provider's outgoing mail server |
| SMTP settings (sending) | SMTP type | SSL, TLS, or None. The SMTP port is set from the type you choose: 465, 587, and 25 respectively. |
| IMAP settings (receiving) | IMAP host | Your provider's incoming mail server |
| IMAP settings (receiving) | IMAP type | SSL and TLS both use port 993, and None uses 143. |

Two provider-specific details to watch for:

-   Gmail mailboxes need an app password for SMTP access rather than the normal account password. You can create one in your Google account security settings, under 2-step verification.
-   If you enter an Outlook or Office 365 hostname, the modal points you back to Microsoft OAuth. Outlook retired IMAP access in 2022, so OAuth is the path that works for those mailboxes.

### Upload accounts in bulk

1.  Select `Bulk CSV upload` and click `Continue`.
2.  On the `Upload a CSV` step, click `Download example CSV` to get a file with the exact structure, fill it in, and upload it. A file with a column missing returns `The uploaded CSV has missing or incomplete data`, and the example file is the quickest way to check the shape.
3.  On `Select accounts to import`, tick the addresses you want — everything is ticked by default — and click `Add accounts`.
4.  Choose whether to enable warmup on the `Enable email warming to improve deliverability` step.

Your CSV needs one row per mailbox, with these columns:

| Column | What goes in it |
| --- | --- |
| from_email | The address campaigns send from |
| from_name | The sender name recipients see |
| user_name | The username the mail server expects, often the address itself |
| password | The mail server password, or an app password for Gmail mailboxes |
| smtp_host | Your provider's outgoing mail server |
| smtp_port | 465 for SSL, 587 for TLS, 25 for none |
| imap_host | Your provider's incoming mail server |
| imap_port | 993 for SSL and TLS, 143 for none |

Any accounts that don't import are listed back to you grouped by reason, so a whole batch with the same problem can be fixed in one pass. A rejected login is the most common one, and it's usually the app password point above.

## Reconnecting a disconnected account

Google and Microsoft revoke access tokens from time to time — after a stretch of inactivity, or as part of a routine security check. When that happens, the account shows `Auth error` in the `Status` column of the `Email accounts` tab, and hovering the badge tells you which credentials couldn't be verified.

An account in `Auth error` can't send or fetch replies until it's reconnected. Reconnecting is the action to take — the sends and replies waiting behind the account come through once it's reachable again, and pausing leads by hand doesn't speed that up.

1.  On the `Email accounts` tab, find the account and open its 3-dot menu.
2.  Click `Reconnect`.
3.  Sign in again with the same mailbox. The flow only accepts the address that's already connected, which keeps you from re-authenticating into a different inbox by accident.
4.  You'll see an `Email account reconnected` confirmation when it lands.

`Reconnect` only appears on an account connected through OAuth, and only while that account is in `Auth error` — a healthy account doesn't show the option. It opens in a pop-up window, so if nothing appears, allow pop-ups for Clay and try again.

For an account added through `Manual SMTP setup` or `Bulk CSV upload`, delete it and add it again with current credentials — that's the reliable fix. For accounts purchased through Clay, contact Clay support and they'll resolve it on their side.

## FAQs

### Why does an admin have to authorize the Clay Sequencer app at all?

Campaign sending comes with inbox warmup, which sends and receives mail on the account's behalf. That puts the app outside the scope Google and Microsoft will fully verify themselves, so the decision moves to the person who administers your domain instead. Every cold email sequencer that includes warmup works this way.

The practical upside is that it's a single step per Workspace or organization. Once it's done, every mailbox on the domain can connect without involving the admin again.

### Can I connect a personal Gmail or Outlook account?

OAuth connections are for business mailboxes on a domain you administer, through Google Workspace or Microsoft 365. A personal address — a Gmail or Hotmail mailbox, for example — can't be connected this way.

That lines up with what works for cold outbound anyway: a domain you control is what lets you set DNS records, spread sending across several mailboxes, and protect your reputation over time.

### Will campaign emails show up in my Sent folder?

For accounts connected with Google or Microsoft OAuth, yes — campaign sends land in the mailbox's `Sent` folder alongside everything else you send. For SMTP accounts it depends on the mail server, and most don't copy messages sent over SMTP into `Sent`.

Either way, replies are fetched from the mailbox over IMAP and collected on the campaign's `Replies` tab, so you can answer from the same address the email went out from.

### Clay says the address is already in use — what now?

Smartlead allows an email address to be connected to one account at a time, so an address that was previously linked to another Smartlead account has to be released there before it can connect here.

If you have access to that Smartlead account, delete the address there and connect it again in Clay. If you don't, contact Clay support with the address you're trying to add and they can remove it for you.
