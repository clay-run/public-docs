---
title: Email warmup
description: How email warmup builds sending reputation for Clay email accounts, how it differs between purchased and self-connected accounts, and how to manage and filter warmup traffic.
last_synced: 2026-09-01T03:28:08.880Z
---

# Email warmup

What email warmup does, how it differs on purchased and self-connected accounts, and why you'll see unfamiliar emails while it runs.

Email warmup builds a sending account's reputation before it starts carrying real campaign volume, which makes your emails more likely to land in the primary inbox. It works the same way whether you bought your accounts in Clay or connected your own.

**Note:** While warmup is running, you'll see unfamiliar emails arriving in and going out from your account, sometimes with odd subject lines or filler content. That's warmup traffic between your account and other accounts in the pool, and it's expected — none of it reaches the leads in your campaigns. The filtering section below shows you how to keep it out of your inbox.

## What warmup is

Warmup enrolls your account in a shared pool of other sending accounts. Your account automatically sends and receives email to and from accounts in that pool on a steady daily schedule. Providers then see an account holding ordinary back-and-forth conversations, rather than one that goes from silent to hundreds of cold emails overnight — and that history is what builds the reputation your campaigns rely on.

A new account takes about three weeks to warm fully. Its status in the `Email accounts` list tells you where it is:

-   `Warming up` — the account is inside that three-week window.
-   `Ready` — the account is through the window.
-   `Not warming` — warmup is switched off for the account.

Volume guidelines for an account that has finished warming live in [Deliverability and domain health](https://university.clay.com/docs/sequencer-deliverability).

## Warmup on purchased vs. your own accounts

Accounts you buy in Clay arrive with warmup already running, and Clay keeps the settings tuned for you. Accounts you connect yourself are under your control, so warmup is something you opt into per account.

| Behavior | Accounts you buy in Clay | Accounts you connect yourself |
| --- | --- | --- |
| Turning it on | On automatically as soon as the accounts are provisioned. | Off until you opt in, either as you add the account or any time after. |
| Daily volume | Managed by Clay. | You choose it with Emails per day. |

Because Clay manages warmup on purchased accounts, those accounts don't show warmup controls in the `Email accounts` list.

## Turning warmup on and off

We recommend keeping warmup on at all times for every account you connect, including accounts that have been sending for a while.

1.  Select `Campaigns` in the sidebar, then open `Email accounts`.
2.  Open the 3-dot menu on the account and select `Enable warming`. The option is there whenever warming isn't already running on the account.
3.  In the `Enable email warming to improve deliverability` modal, the accounts are listed already checked. Select `Enable warming` to turn it on for everything still checked. Uncheck all of them and that same button becomes `Continue without warming`, which closes the modal and leaves the accounts as they are.

To change how much warmup mail an account sends, open the same menu and select `Edit warmup frequency`, then set `Emails per day` to anything from 1 to 30. This option appears only once warming is active on the account.

To stop warmup, select `Disable warming` from the same menu. You can also select several accounts in the `Email accounts` list at once and enable warming for all of them together.

## Filtering warmup emails out of your inbox

Every workspace has its own two-word filter key, and every warmup email thread contains that key somewhere. The `Enable email warming to improve deliverability` modal shows it under `Filter key:`, with a button to copy it.

For accounts connected through Google or Microsoft OAuth, Clay sets up an email filter automatically and tries to apply a `Clay sequencer warmup email` label, so most warmup mail never reaches your inbox. To build your own rule instead — or on an account where the automatic filter doesn't apply — filter or search on the filter key and you'll catch every warmup thread.

## Why warmup sometimes disables itself

Warmup occasionally turns itself off. That usually means the email provider is throttling the account's sending, and warmup steps back rather than pushing against the limit.

So an account showing `Not warming` unexpectedly is more often a throttling signal than a problem with the account itself. Once the provider settles, turn warming back on yourself with `Enable warming` from the 3-dot menu on the account.
