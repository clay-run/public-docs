---
title: Plans & billing
description: We'll walk through each of our pricing plans and information around
  billing your workspace.
last_synced: 2026-04-26T01:40:29.319Z
---

# Plans & billing

We'll walk through each of our pricing plans and information around billing your workspace.

Clay offers three plan tiers that differ by features, capacity, and pricing. For a detailed comparison of all plans, visit our [pricing page](https://www.clay.com/pricing).

You can adjust your yearly or monthly credit limits on most plans to match your usage needs, either during sign-up or by contacting our team.

## Understanding actions and data credits

-   **Actions** measure the orchestration you do in Clay: enriching data, running AI research, and sending data to other tools (like posting to Slack or generating Notion briefs). Each enrichment or execution task consumes 1 action. Each action costs a few tenths of a penny. Actions are a background meter included in your Clay plan. 90% of customers will never hit their actions limit.
-   **Data credits:** Used to buy data or AI from 3rd-party vendors in Clay's data marketplace—costs vary by data type. Each credit costs a few pennies.

This separation gives you transparency and control over exactly what you're paying for.

### AI usage

Every AI prompt counts as **one action**. Data credits are consumed based on the model you select—Clay offers both fixed and variable AI pricing. For details on how AI pricing works, see our guide on [how AI is priced](https://university.clay.com/docs/ai-pricing).

For more details on actions and data credits, see our comprehensive guide on [actions and data credits](https://www.clay.com/university/guide/actions-and-data-credits).

## **Upgrade your plan**

To upgrade your Clay workspace plan:

1.  Click your profile picture in the top-right corner and select `Settings`.
2.  In the left sidebar, navigate to `Plans & billing`, then click `Switch plan`.
3.  Select the plan you want to upgrade to and review the details.
4.  Confirm your selection by clicking `Review change → Continue to payment`.

Your new plan will activate immediately, and any applicable charges will be applied.

**How upgrade billing works:** Plan upgrades are **not prorated** — you pay the full price of the new tier immediately, not a partial amount for remaining days in your current cycle. In return, you receive the **full** Actions and Data Credits for your new plan right away. Unused Actions from your previous plan are not carried over (Actions reset each billing cycle and do not roll over). Your existing unused Data Credits are preserved when you upgrade.

### Launch plan

-   **Best for:** Teams enriching less than 1,000 records per month
-   **Actions:** 15,000 per month
-   **Data credits:** 2,500 to 10,000 per month
-   **Monthly pricing:** Starting at $185/month (includes 2,500 credits and 15,000 actions)
-   **Table limit:** 50,000 rows per table
-   **Features:** Basic enrichment, list building

### Growth plan

-   **Best for:** Teams enriching 1,000 to 10,000 records per month
-   **Actions:** 40,000 per month
-   **Data credits:** 6,000 to 100,000 per month
-   **Monthly pricing:** Starting at $495/month (includes 6,000 credits and 40,000 actions)
-   **Table limit:** 50,000 rows per table
-   **Features:** Webhooks, CRM integrations, HTTP API, web intent signals, advanced automation, audiences

### Enterprise plan

-   **Best for:** Teams enriching 10,000+ records per month
-   **Actions:** 100,000+ per month (custom)
-   **Data credits:** 100,000+ per month (custom)
-   **Table limit:** 50,000 rows per standard table (this limit applies by default and is not automatically removed on Enterprise); use [bulk enrichment](bulk-enrichment.md) to process larger datasets — rows are enriched in rolling batches and sent to your destination with no cumulative row cap
-   **Benefits:** Volume discounts on data credits at higher tiers, dedicated Growth Strategist, managed onboarding, data warehouse integrations, bulk enrichment, SSO, RBAC

### Downgrade your plan

To downgrade your Clay workspace plan:

1.  Click your profile picture in the top-right corner, then select `Settings`.
2.  Navigate to `Plans & billing` and click `Switch plan`.
3.  Choose the plan you'd like to downgrade to and confirm your selection.

**How downgrade billing works:** Plan downgrades are deferred to the end of your current billing cycle — your existing plan stays active until then, and you keep receiving its current Actions and Data Credit allocation. At renewal, your workspace switches to the new plan and your monthly Actions and Data Credit allocation resets to the new plan's level.

**What happens to your Data Credits:** When the plan change takes effect, your credit balance is reduced to the rollover cap of your new plan — 2× its monthly credit limit. For the free plan (100 credits/month), that cap is 200 credits. Any credits above the cap are forfeited. If you have a large balance, spend it down before the change takes effect.

## Billing

To update your billing and payment information:

1.  Click your profile picture in the top-right corner and select `Settings`.
2.  In the sidebar, navigate to `Plans & billing`.
3.  Click `Update credit card` to edit your payment method or `Update email` to change your billing email.
4.  Enter the updated information for your payment method or billing email.
5.  Confirm your changes and click `Update`.

### Trials

Clay offers a 14-day free trial with 1,000 data credits, giving you access to webhooks, CRM integrations, email sequencers, and HTTP API capabilities.

Phone number enrichments aren't available on free or trial plans — this restriction applies even if you have unused data credits. To access this feature, upgrade to a paid plan. This also affects some waterfall templates: if a waterfall includes a provider that can return phone numbers (such as PDL or Bytemine), free and trial users will see "Your subscription does not allow this integration to be added" even if the goal of the waterfall is something other than a phone number (for example, a profile URL). To work around this, remove the phone-number providers from the waterfall sequence. See [Waterfalls](https://university.clay.com/docs/building-a-data-waterfall) for details.

If phone number enrichment doesn't appear immediately after upgrading, refresh the page and re-add the phone-number enrichment column to reload the available providers.

If your team wants to do a trial, each team member can create their own trial account to explore Clay independently.

Trial tables can hold up to **1,000 rows each**. The table view also displays only the first **50 rows** — rows beyond that are blurred in the UI until you upgrade to a paid plan.

When your trial ends, your account automatically moves to the free plan — you won't be charged unless you actively choose to upgrade to a paid plan. Clay does not auto-upgrade you. For details on what happens to your trial data credits at that point, see [Actions and data credits](actions-data-credits.md).

## FAQs

### How do I track my actions and data credits usage?

You can track both actions and data credits usage in the `Usage Dashboard`, which you can access from the `Settings` menu in the app. You can also track usage at the table level via `Table history`.

### Do credits roll over?

**Monthly plans:** When your plan refreshes, unused data credits will roll over and accumulate. The maximum accumulation is capped at 2× your plan's monthly credit limit — and this cap includes the newly added renewal credits. For example, if your plan includes 50,000 credits per month, your maximum balance is 100,000. If you already have 82,000 credits when your plan renews, you will end up with 100,000 credits, not 132,000.

**Annual plans:** When your plan refreshes, you can roll over up to 15% of your annual data credits in addition to the new credits you receive, provided you renew on the same or a higher-tier plan.

**If you cancel or downgrade your plan:** When the plan change takes effect, your Data Credit balance is reduced to the rollover cap of your new plan — 2× that plan's monthly credit limit. For example, canceling to the free plan (100 credits/month) caps your balance at 200 credits; any credits above 200 are forfeited. You can continue spending your existing credits up until the plan change takes effect.

For more details, see our guide on [actions and data credits](https://www.notion.so/Actions-and-data-credits-2a77e66eb01480b798f2ddca99d45e80?pvs=21).

### Is upgrading my plan prorated?

No. Plan upgrades are not prorated. When you upgrade to a higher tier, you are charged the full price for the new plan immediately — not a partial amount for remaining days in your current billing cycle. In return, you receive the **full** Actions and Data Credits for your new tier right away, not just the incremental difference over your current plan.

Unused Actions from your previous plan are not refunded or carried over (Actions reset each billing cycle and do not roll over). Your existing unused Data Credits are preserved when you upgrade.

If you're unsure whether you need a higher tier, check your current usage in `Settings` → `Usage` to see how many Actions and Data Credits you've consumed this billing cycle before committing to an upgrade.

### What if I need more actions or data credits?

**Actions:** Actions cannot be purchased as one-time top-ups — they represent fixed platform capacity tied to your action tier. To increase your Actions limit, you must upgrade to a higher action tier in `Settings` → `Plans & billing`.

**Data Credits:** You have two options:

-   **Upgrade your Data Credits tier** (recommended for ongoing needs) — no premium charged.
-   **Purchase a one-time top-up** — available for emergency needs during your billing cycle at a 30% premium (50% on legacy plans), subject to rollover limits. Go to `Settings` → `Usage` and click `Add one-time data credits`.

### How many actions and data credits do I need?

-   **Launch plan:** Suitable for enriching less than 1,000 records per month
-   **Growth plan:** Suitable for enriching 1,000 to 10,000 records per month
-   **Enterprise plan:** Suitable for enriching 10,000+ records per month

Each fully enriched record typically costs 6-20 data credits (including company and person profile, email, phone number, and custom AI enrichments). The more private API keys you use, the fewer data credits you'll spend per record.

### How do I cancel my subscription?

There is no minimum contract commitment — you can cancel at any time. To cancel:

1.  Click your profile picture in the top-right corner and select `Settings`.
2.  Navigate to `Plans & billing`.
3.  Click `Cancel plan` and follow the prompts to confirm.

Cancellations take effect at the end of your current billing cycle. Until then, you retain access to your paid plan's features and credit allocation. At the end of the cycle, your workspace moves to the Free plan and your Data Credit balance is reduced to the Free plan's rollover cap (200 credits — see [Do credits roll over?](#do-credits-roll-over) for how the credit cap works). Any credits above that cap are forfeited.

For information on payment refunds after canceling, see [How long does a refund take?](#how-long-does-a-refund-take) below.

### How long does a refund take?

Payment refunds take up to **10 business days** to appear in your account after Clay initiates them. If 10 business days have passed and the refund still hasn't appeared:

1.  Confirm the funds haven't already been credited to your account.
2.  Contact [Clay support](https://app.clay.com) and share any available transaction details — an Acquirer Reference Number (ARN) is especially helpful for tracing the payment.

Clay Data Credit refunds (for enrichment actions that return no data) are applied to your account balance immediately after processing.

### What happens if my payment fails?

If a payment fails, Clay retries the charge automatically before canceling your subscription:

-   **Credit card billing (Launch, Growth):** Clay retries for up to **14 days**. If the payment is not resolved within that window, your workspace is downgraded to the Free plan.
-   **Invoice billing (Enterprise):** Clay retries for up to **30 days** before canceling.

Once downgraded to the Free plan, your Data Credit balance is capped at **200 credits** (the Free plan's rollover limit) — any credits above that cap are forfeited at the end of your billing cycle.

To avoid an interruption, keep your payment information current in `Settings` → `Plan & billing`.
