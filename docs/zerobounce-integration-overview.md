---
title: Zerobounce integration
description: Email validation and deliverability tools boost inbox placement and
  marketing ROI.
last_synced: 2026-04-26T01:40:59.101Z
---

# Zerobounce integration

Email validation and deliverability tools boost inbox placement and marketing ROI.

## Getting started with Zerobounce

[ZeroBounce](https://www.clay.com/integrations/data-provider/zerobounce) in Clay validates work emails to ensure they're safe, reducing bounces, protecting your sender reputation, and improving deliverability. Just input your email address to know if your email is validated.

## Connecting Clay to Zerobounce

Within Clay, you have two ways to access the Zerobounce enrichment.

### Option 1: Use the Clay-managed Zerobounce account

By default, Zerobounce enrichments will use the Clay-managed Zerobounce account. On current plans, each Zerobounce email verification run with the Clay-managed account uses 1 Action and 0.1 Data Credits. On legacy plans, it costs 1 credit. See [How much does ZeroBounce email verification cost?](#how-much-does-zerobounce-email-verification-cost) for details.

Simply pull up any Zerobounce enrichment within Clay to use the Clay-managed Zerobounce account.

### Option 2: Add your own Zerobounce API key

If you are currently on a paid plan (Starter, Explorer, Pro) you can use your own Zerobounce account within Clay through an API key.

To add your own API key for any Zerobounce enrichment, you can do so when you're selecting an account.

Below is an example of where to click within the enrichment panel to add your API key. For more instructions on how to find your Zerobounce API key, [follow these instructions](https://www.zerobounce.net/docs/api-dashboard/key-management/) within Zerobounce's documentation.

## `Action` Validate Email

With Zerobounce's **Validate Email** action, you can determine if a certain email has a valid inbox.

**Step 1: Choose the ZeroBounce account you want to use**  
You can use either the Clay-managed ZeroBounce account or bring your own key. If you use the Clay-managed ZeroBounce account, each verified email uses 1 Action and 0.1 Data Credits on current plans (1 credit per enriched cell on legacy plans).

**Step 2: Select the email you want to verify**  
Input the email address you want to verify.

The enrichment includes an **Only "Safe To Send" Emails?** toggle that controls how catch-all emails are handled:

- **Toggle off (default):** Emails that ZeroBounce classifies as catch-all are returned with a **Status** of `valid` and a **Sub Status** of `catch_all`. Catch-all emails count as valid results by default.
- **Toggle on:** Only emails that ZeroBounce strictly classifies as `valid` are returned. Catch-all emails are excluded entirely from the results.

**Step 3 (Optional): Select Auto-update**  
By default, Nimbler will auto-update the integration every 24 hours. Make sure to toggle this step off if you do not want to auto-update. However if you do so, you might run into stale data problems.

**Step 4 (Optional): Select Conditional Run Criteria**  
If you want to only run this enrichment under set circumstances, you are able to input formulas where the column runs only if the formula is true. Learn more about conditional runs in [this Clay University lesson](https://www.clay.com/university/lesson/ai-formulas-conditional-runs-clay-101#:~:text=Conditional%20runs%20\(which%20make%20use,personal%20emails%20for%20all%20rows\).).

## How much does ZeroBounce email verification cost?

When you set up the ZeroBounce **Validate Email** (Verify Email) enrichment on a current plan (for example, Launch, Growth, or Enterprise on current pricing), the usage estimate shows **1 Action** and **0.1 Data Credits** per row. These are two separate charges that come from two different balances, and the total cost of each ZeroBounce email verification is both together:

- **Actions:** 1 Action per email verified. Every ZeroBounce verification uses 1 Action, including when you use your own ZeroBounce API key.
- **Data Credits:** 0.1 Data Credits per email verified with the Clay-managed ZeroBounce account. If you connect your own ZeroBounce API key, ZeroBounce verification uses 0 Data Credits.

For example, verifying 10,000 emails with the Clay-managed ZeroBounce account uses 10,000 Actions and 1,000 Data Credits (10,000 × 0.1). With your own ZeroBounce API key, the same 10,000 verifications use 10,000 Actions and 0 Data Credits.

On legacy plans, ZeroBounce email verification costs 1 credit per row, and the usage estimate does not show an Action cost. See [Legacy plans](./legacy-plans.md) for how pricing changes when you switch to a current plan.

The usage estimate shown when you set up the ZeroBounce column reflects the pricing on your workspace's current plan, so it's the best guide for planning. For more on how the two balances work, see [Actions & Data Credits](./actions-data-credits.md).

## Viewing ZeroBounce validation results

The ZeroBounce Validate Email enrichment outputs a **Status** column for each row. Possible values include `valid`, `invalid`, `catch-all`, `spamtrap`, `abuse`, `do_not_mail`, and `unknown`. A **Sub Status** column provides additional detail (for example, `catch_all` when a catch-all email is returned as valid under the default setting).

There is no built-in validation rate dashboard, but you can track results directly in your table:

- **Filter by Status** — add a filter on the Status column (for example, Status = "valid") to isolate rows by category. The row count shown in the table header gives you the total for that status.
- **Add a formula column** — create a formula column to flag valid emails, then use the column summary to get a count or percentage of valid results across your entire table.
