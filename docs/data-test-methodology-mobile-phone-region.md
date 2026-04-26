---
title: "[Data test] Mobile phone providers by region"
source_url: https://university.clay.com/docs/data-test-methodology-mobile-phone-region
description: Mobile phone providers by region
last_synced: 2026-04-26T01:39:51.023Z
upstream_hash: d4fb9948962bd860e7ddf7bb87056b3f13c5eb58b4233580b4ce550fd1fde272
---

# \[Data test\] Mobile phone providers by region

Mobile phone providers by region

Sales teams often lose valuable time calling inaccurate mobile phone numbers from contact databases. It's frustrating to call an inaccurate phone number or the wrong person picks up.

In our endless quest to help you save time (and Clay credits!), we partnered with TitanX to test over 9,806 mobile numbers to find the best combination of accuracy and cost across North America, Europe, and APAC. Our data test focused on three key areas:

1.  **Accuracy:** When you dial a number, how likely are you to actually reach your intended recipient?
2.  **Coverage:** Which provider produced the most mobile numbers for prospects, both in sheer volume and across different regions? **‍**
3.  **Budget:** Which provider offers the best price per mobile number, and saves your sales team the most time in the long run?  

We recommend using [mobile phone data waterfalls](https://www.clay.com/waterfall-enrichment) to get best combination price and coverage. However, if you’re choosing just one provider, we’ll guide you to the best fit.

## **Our data test methodology**

We started by amassing over 6,000 B2B contacts across North America (NAMER), Europe, the Middle East, and Africa (EMEA), and the Asia Pacific (APAC). We then [enriched](https://www.clay.com/blog/anthropic-case-study) these contacts by running them through the following B2B data providers:

-   Forager
-   Nimbler
-   Wiza
-   Datagma
-   Leadmagic
-   RocketReach
-   People Data Labs
-   ContactOut
-   Findymail
-   Prospeo

After enriching our contact data, we received 9,806 mobile numbers. Seeing as different providers may offer different phone numbers for a single contact, we then sifted through this list to extract only unique combinations of mobile numbers and full names.

From there, we measured each provider’s coverage based on the quantity of numbers they delivered for each region.

💡**Pro tip:** _Data coverage can vary not only from region to region but also from industry to industry. While we didn't evaluate coverage based on industry in this particular report, this is still something you should take into account as you search for providers that will help you to connect with prospects that meet your ideal customer profile (ICP)._

#### **Testing & Scoring Phone Numbers**

We partnered with [TitanX](https://www.titanx.io/?utm_source=clay&utm_medium=blog&utm_campaign=scoring) (formerly Phone Ready Leads) to implement their proprietary scoring algorithm for numbers across the NAMER and EMEA regions. For scoring numbers in the APAC region, we partnered with an offshore team who verified calls using the comprehensive method outlined below.

#### NAMER & EMEA

TitanX kicked off our evaluation by implementing their proprietary Titan Scoring algorithm, which includes both manual cold calling as well as an evaluation of 11 other data signals over the course of four days. Think of this algorithm as a form of intent data [lead scoring](https://www.clay.com/blog/lead-scoring-in-clay); it not only verifies mobile numbers, but also offers one of the following weighted scores for each number:

-   **P1 mobile numbers** are not only verified, but they also lead to contacts that have a high propensity for picking up the phone. Due to these two factors, P1 numbers are likely to connect you with your intended contact at least 25% of the time.
-   **P2 mobile numbers** are also verified, but they lead to contacts with a lower propensity to answer calls. This means that the mobile number may only connect you with your intended contact around 4-10% of the time.
-   **P3 mobile numbers** are unverified, and lead to contacts with a very low propensity to answer the phone. They have a connection rate that’s usually under 1%.
-   **Mobile numbers that “need attention”** are usually inactive, disconnected, and/or belong to the wrong person. Naturally, they have a 0% connection rate and you should continue enriching with other providers to find the right number.

TitanX approached scoring this way to address the dreaded "Right Name, Wrong Person" problem. This occurs when data appears to be accurate on the surface, but actually belongs to a different person with the same name. TitanX's process catches these mix-ups, ensuring you don't waste time calling John Smith the professor when you're trying to reach John Smith the CEO. This level of accuracy is crucial for effective prospecting and targeted marketing campaigns.

**TitanX Benchmarks for Scoring Mobile Numbers**

After scoring mobile numbers with TitanX, here’s the formula we used to standardize the quality score for each provider:

This formula assumes that P2 is half the quality of P1, and that P3 is a quarter of the quality of P1. “NA” scores, or mobile numbers that “Need attention,” have a completely negative impact.

💡**Did you know?** _With our upcoming integration, you’ll be able to harness the power of TitanX without leaving your Clay workbook._

#### APAC

For our APAC contacts, we took a slightly different approach. Our offshore team called each number at least five times, or until we reached a deterministic outcome, like a number being out of service, or a person with a different name picking up the phone. This hands-on method helped us to assign the following scores to each of the mobile numbers in our dataset:

-   **Good phone numbers** are verified by contacts answering the phone _and_ confirming their name. They can also be verified by a voicemail mentioning the contact’s name.
-   **Unverified phone numbers** led to calls that went completely unanswered, or did not have a voicemail mentioning the contact’s name.
-   **Bad phone numbers** were out of service, or led to calls where the wrong contact picked up. These numbers should be removed from your contact lists to maintain data quality and optimize your sales process.

Similar to our formula for the NAMER and EMEA scores, we used the following to calculate the quality score for each provider:

This formula assumes that unverified phone numbers are a quarter of the quality of good phone numbers, and that bad phone numbers have a completely negative impact.

#### **Calculating Budget & Costs**

We calculated each provider’s cost per quality mobile number according to the value of Clay credits you’d need to purchase it.

However, the dollar amount isn't the only thing that you should include in your budget; there's also the efficiency factor. If a sales team is stuck using unverified numbers, they might waste precious hours on unproductive calls. Taking this under consideration, we also factored potential [time savings](https://www.clay.com/blog/how-chatmetrics-saved-time-cut-costs-and-replaced-their-sdrs-with-clay) into our findings.

### **Results & Analysis**

After enriching 6,000 contacts, we found 9,806 mobile numbers. Only 23% of those numbers were deemed to be P1 or “Good” numbers. (Remember: These are verified numbers for contacts who have a high propensity for answering calls.)

This number may be lower than expected, but shows why it's essential to reference each provider's quality score before buying. By choosing a provider with more accurate, actionable data, you'll be better able to prioritize your sales reps' time so that they don't have to keep getting stuck at voicemail.

In fact, TitanX found that by using providers with more verified mobile numbers, sales reps can have up to 5X more conversations every hour—thereby significantly improving their sales process and lead generation efforts.
