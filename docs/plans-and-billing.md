---
title: Plans & billing
source_url: https://university.clay.com/docs/plans-and-billing
---

# Plans & billing

Clay offers three plan tiers that differ by features, capacity, and pricing. For a detailed comparison of all plans, visit the [pricing page](https://www.clay.com/pricing).

You can adjust your yearly or monthly credit limits on most plans to match your usage needs, either during sign-up or by contacting the Clay team.

## Understanding actions and data credits

Clay usage is measured across two separate meters:

- **Actions** measure the orchestration work Clay performs on your behalf: enriching data, running AI research, and sending data to third-party tools (e.g., pushing to a sequencer, triggering a Slack alert). Each enrichment or execution task consumes 1 action. 90% of customers will never hit their actions limit.
- **Data credits** are used to buy data from 3rd-party vendors in Clay's data marketplace—costs vary by data type. Each credit costs a few pennies.

This separation gives you transparency and control over exactly what you're paying for.

### What counts as an action

**Actions are consumed for:**

- Enriching records with 3rd-party data (from Clay's marketplace or via your own API key)
- AI web research (Claygent) and AI-generated content
- GTM execution tasks: pushing records to a CRM (e.g., Salesforce, HubSpot), sending to a sequencer, triggering ads audiences, or calling an HTTP API

**Actions are NOT consumed for:**

- Importing records (from CSV, webhooks, CRM, or data warehouse)
- Exporting data to CSV — CSV downloads are completely free and unlimited on all plans
- Running formula columns, data transformations, or scoring logic
- Moving data between tables within Clay
- Looking up 1st-party data you've already imported

### AI usage

Every AI prompt counts as one action. Data credits are consumed based on the AI model you select—Clay offers both fixed and variable AI pricing. For details, see the guide on [how AI is priced](https://university.clay.com/docs/ai-pricing).

For a comprehensive breakdown, see the [actions and data credits guide](https://www.clay.com/university/guide/actions-and-data-credits).

## Plans

### Launch plan

- **Best for:** Individuals and small teams enriching fewer than 1,000 records per month
- **Starting price:** $185/month ($167/month billed annually)
- **Actions:** 15,000 per month
- **Data credits:** 2,500 to 10,000 per month
- **Table limit:** 50,000 rows per table
- **Features:** Basic enrichment, list building, phone number enrichment, job change and signal tracking, email campaign integrations

### Growth plan

- **Best for:** Teams enriching 1,000 to 10,000 records per month
- **Starting price:** $495/month ($446/month billed annually)
- **Actions:** 40,000 per month
- **Data credits:** 6,000 to 100,000 per month
- **Table limit:** 50,000 rows per table
- **Features:** Everything in Launch, plus CRM auto-sync and enrichment (Salesforce, HubSpot, etc.), HTTP API integrations, webhook automation, web intent signal tracking, audience pushes to ads platforms, and priority support

### Enterprise plan

- **Best for:** Teams enriching 10,000+ records per month
- **Actions:** 100,000+ per month (custom)
- **Data credits:** 100,000+ per month (custom)
- **Benefits:** Volume discounts, dedicated Growth Strategist, managed onboarding, data warehouse integrations, bulk enrichment, SSO, RBAC permissions management

## Upgrading your plan

1. Click your profile picture in the top-right corner and select `Settings`.
2. In the left sidebar, navigate to `Plans & billing`, then click `Switch plan`.
3. Select the plan you want to upgrade to and review the details.
4. Confirm by clicking `Review change → Continue to payment`.

Your new plan activates immediately.

## Downgrading your plan

1. Click your profile picture in the top-right corner and select `Settings`.
2. Navigate to `Plans & billing` and click `Switch plan`.
3. Choose the plan you'd like to downgrade to and confirm your selection.

## Billing

To update your payment information:

1. Click your profile picture in the top-right corner and select `Settings`.
2. Navigate to `Plans & billing`.
3. Click `Update credit card` to edit your payment method or `Update email` to change your billing email.
4. Enter the updated information and confirm.

### Free trial

Clay offers a 14-day free trial with 1,000 data credits, giving you access to webhooks, CRM integrations, email sequencers, and HTTP API capabilities. Phone number enrichments aren't available during the trial—upgrade to a paid plan to access them.

Each team member can create their own trial account to explore Clay independently.

## FAQs

### Does exporting to CSV count as an action?

No. Downloading your table data as a CSV is completely free on all plans and does not consume any actions or data credits. You can export as many rows as you like without any cost.

Note that **pushing records to a CRM** (e.g., syncing a row to Salesforce or HubSpot) is a different operation—it counts as 1 action per record because Clay is orchestrating work with a third-party system. CRM integrations are only available on Growth and Enterprise plans.

### Do Launch and Growth plans have different export limits?

Both Launch and Growth plans have identical CSV export capabilities—unlimited, free downloads. The difference between plans lies in which export *destinations* are available:

- **Launch:** CSV export only
- **Growth:** CSV export plus CRM sync (Salesforce, HubSpot, Pipedrive, etc.), HTTP API, webhooks, and ads audience pushes

### How do I track my actions and data credits usage?

You can track both actions and data credits usage in the `Usage Dashboard`, accessible from the `Settings` menu. You can also track usage at the table level via `Table history`.

### Do credits roll over?

**Monthly plans:** Unused data credits roll over and accumulate up to 2× your plan's monthly credit limit. For example, a plan with 50,000 credits/month can bank up to 100,000 credits total.

**Annual plans:** You can roll over up to 15% of your annual data credits when you renew on the same or a higher-tier plan.

Actions do not roll over—they reset each billing cycle.

### What if I need more actions or data credits?

You can upgrade your plan tier at any time in `Settings → Plans & billing`. You can also purchase one-off data credits at a 30% premium during your billing cycle.

### How many actions and data credits do I need?

- **Launch plan:** Suitable for enriching fewer than 1,000 records per month
- **Growth plan:** Suitable for enriching 1,000 to 10,000 records per month
- **Enterprise plan:** Suitable for enriching 10,000+ records per month

Each fully enriched record typically costs 6–20 data credits (covering company profile, person profile, email, phone number, and custom AI enrichments). The more private API keys you bring, the fewer data credits you spend per record. Use Clay's [pricing calculator](https://www.clay.com/pricing-calculator) to estimate your usage.
