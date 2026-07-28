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

By default, Zerobounce enrichments will use the Clay-managed Zerobounce account. This means that any new enrichment will charge 1 credit.

Simply pull up any Zerobounce enrichment within Clay to use the Clay-managed Zerobounce account.

### Option 2: Add your own Zerobounce API key

If you are currently on a paid plan (Starter, Explorer, Pro) you can use your own Zerobounce account within Clay through an API key.

To add your own API key for any Zerobounce enrichment, you can do so when you're selecting an account.

Below is an example of where to click within the enrichment panel to add your API key. For more instructions on how to find your Zerobounce API key, [follow these instructions](https://www.zerobounce.net/docs/api-dashboard/key-management/) within Zerobounce's documentation.

## `Action` Validate Email

With Zerobounce's **Validate Email** action, you can determine if a certain email has a valid inbox.

**Step 1: Choose the ZeroBounce account you want to use**  
You can use either the Clay-managed ZeroBounce account or bring your own key. If you use the Clay-managed ZeroBounce account you will be charged at 1 credit per enriched cell.

**Step 2: Select the email you want to verify**  
Input the email address you want to verify.

The enrichment includes an **Only "Safe To Send" Emails?** toggle that controls how catch-all emails are handled:

- **Toggle off (default):** Emails that ZeroBounce classifies as catch-all are returned with a **Status** of `valid` and a **Sub Status** of `catch_all`. Catch-all emails count as valid results by default.
- **Toggle on:** Only emails that ZeroBounce strictly classifies as `valid` are returned. Catch-all emails are excluded entirely from the results.

**Step 3 (Optional): Select Auto-update**  
By default, Nimbler will auto-update the integration every 24 hours. Make sure to toggle this step off if you do not want to auto-update. However if you do so, you might run into stale data problems.

**Step 4 (Optional): Select Conditional Run Criteria**  
If you want to only run this enrichment under set circumstances, you are able to input formulas where the column runs only if the formula is true. Learn more about conditional runs in [this Clay University lesson](https://www.clay.com/university/lesson/ai-formulas-conditional-runs-clay-101#:~:text=Conditional%20runs%20\(which%20make%20use,personal%20emails%20for%20all%20rows\).).

## Viewing ZeroBounce validation results

The ZeroBounce Validate Email enrichment outputs a **Status** column for each row. Possible values include `valid`, `invalid`, `catch-all`, `spamtrap`, `abuse`, `do_not_mail`, and `unknown`. A **Sub Status** column provides additional detail (for example, `catch_all` when a catch-all email is returned as valid under the default setting).

There is no built-in validation rate dashboard, but you can track results directly in your table:

- **Filter by Status** — add a filter on the Status column (for example, Status = "valid") to isolate rows by category. The row count shown in the table header gives you the total for that status.
- **Add a formula column** — create a formula column to flag valid emails, then use the column summary to get a count or percentage of valid results across your entire table.
