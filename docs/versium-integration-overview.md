---
title: Versium integration
description: Versium provides data solutions for audience targeting,
  omnichannel campaigns, and IP-to-domain company enrichment.
last_synced: 2026-04-26T01:40:53.582Z
---

# Versium integration

Versium provides data solutions for audience targeting and omnichannel campaigns.

## Versium Overview

Versium provides contact data for platforms like AdRoll, Facebook, Google, and professional networks, ensuring compatibility and optimized delivery for advertising campaigns.

The integration securely hashes the output data (using SHA256 or MD5) to protect sensitive information while enabling precise audience targeting.

## Setting up Versium and Clay

### Connecting a Versium account

You can connect to Versium in two ways: using a Clay-managed account, which utilizes your Clay credits, or your own account via an API key.

#### Option 1: Use the Clay-managed Versium account

Utilize your Clay Credits to pay for Versium enrichments, utilizing the credits available in your Clay account.

#### Option 2 (**Paid Account Only)**: Connect your Versium API key to Clay

Only workspaces with paid accounts can connect personal API keys to Clay. To connect your API key and set up a personal Versium account, navigate to any of Versium's integration panels or go to **Settings > Connections**.

## Available Versium Actions

Within Clay, there are two actions you can run with Versium:

-   Get additional contact points for advertising audience.
-   IP to Domain Lookup.

### `Action`: Get additional contact points for advertising audience

This action takes personal or business data and returns hashed, pre-formatted contact points (e.g., email, phone, location) for targeting users on platforms such as Facebook, Google, professional networks, and AdRoll.

#### Action Walkthrough

To receive additional contact points for online audience targeting:

**Step 1:** Select the Versium account you want to use.

**Step 2:** Input company or contact data.

Provide one of the following input combinations to match and retrieve accurate records:

1.  **Email, First Name, Last Name**
2.  **Company Domain, First Name, Last Name, City, State**
3.  **Company Name, First Name, Last Name, City, State**
4.  **Social URL** _(Note: This has a lower match rate)_

**Step 3:** Configure run settings.

By default, new rows in your Clay table trigger this action. Learn more about auto-update in this [guide](https://docs.clay.com/en/articles/9642165-auto-update-and-auto-dedupe-table).

To run only under specific conditions, use formulas that trigger the action when true. Learn more [here](https://www.clay.com/university/lesson/ai-formulas-conditional-runs-clay-101).

**Step 4:** Run the action to retrieve your contact points.

#### Input Fields

-   **Email**: A valid email address (business or consumer) used to identify the contact.
-   **First Name**: The individual's first name.
-   **Last Name**: The individual's last name.
-   **Social URL**: A valid URL to the individual's social media profile. Lower match rate compared to other inputs.
-   **Company Domain**: The domain of the company associated with the contact (e.g., [example.com](http://example.com)).
-   **Company Name**: The full name of the company associated with the contact.
-   **State**: The U.S. state where the individual or company is located (two-letter abbreviation).
-   **City**: The city where the individual or company is located.

#### Output Fields

-   **AdRoll**
    -   **Returned Fields**: Email
    -   **Hashed Field**: MD5-hashed email
    -   **Max Field Count**: 8
-   **Facebook**
    -   **Headers**: Email, Phone
    -   **Hashed Field**: SHA256-hashed for all fields
    -   **Max Field Count**: Email: 3, Phone: 3
-   **Google**
    -   **Headers**: Email, Phone
    -   **Hashed Field**: SHA256-hashed for all fields
    -   **Max Field Count**: Email: 3, Phone: 3
-   **Professional network**
    -   **Headers**: Email, Fn (First Name), Ln (Last Name), Job Title, Company, Country, Apple IDFA, Google AID
    -   **Hashed Field**: Email (SHA256), others in plain text
    -   **Max Field Count**: Email: 1
-   **TikTok**
    -   **Headers**: Email, Phone
    -   **Hashed Field**: SHA256-hashed for all fields
    -   **Max Field Count**: Email: 3, Phone: 3
-   **Generic**
    -   **Headers**: Email
    -   **Hashed Field**: SHA256-hashed email
    -   **Max Field Count**: 14

### `Action`: IP to Domain Lookup

This action takes an IP address and returns the domain and company information associated with it. It is commonly used in IP de-anonymization workflows — for example, to identify companies visiting your website.

#### Action Walkthrough

To look up company information for an IP address:

**Step 1:** Select the Versium account you want to use.

**Step 2:** Input the IP address to look up.

**Step 3:** Configure run settings.

By default, new rows in your Clay table trigger this action. To run only under specific conditions, use formulas. Learn more [here](https://www.clay.com/university/lesson/ai-formulas-conditional-runs-clay-101).

**Step 4:** Run the action to retrieve company information.

#### Input Fields

-   **IP Address**: The IP address to look up.

#### Output Fields

-   **IP Usage Type**: Classifies how the IP is used (e.g., `Business`, `Data Center/Web Hosting/Transit`, `ISP/Mobile ISP`). Shared infrastructure types like data centers may be associated with multiple companies.
-   **Is ISP**: Indicates whether the IP is registered to an ISP.
-   **Results**: An array of up to 3 company matches. Each result includes:
    -   **Domain**: The company's website domain.
    -   **Company Name**: The company's name.
    -   **Company Address**, **Company City**, **Company State**, **Company Zip**, **Company Country**: Location details.
    -   **Phone**: Company phone number.
    -   **Website Home Page**: The company's homepage URL.
    -   **Industry**: Industry classification.
    -   **Employee Range**: Estimated employee count range.
    -   **Sales Revenue Range**: Estimated annual revenue range.
    -   **Year Founded**: Year the company was founded.
    -   **SIC** / **SIC Description**: Standard Industrial Classification code and description.
    -   **NAICS** / **NAICS Description**: North American Industry Classification System code and description.
    -   **Public/Private**: Whether the company is publicly or privately held.

#### Understanding multiple results

When an IP address is classified as shared infrastructure (for example, an `IP Usage Type` of `Data Center/Web Hosting/Transit`), Versium may return up to 3 company matches. Multiple organizations can route traffic through the same data center or hosting provider, so the same IP can legitimately be associated with several different companies.

**Important:** The results array is not sorted by confidence — there is no guarantee that the first result is the most accurate match.

**Handling multiple results:**

-   **Keep all matches and enrich further:** Write the results to a new table and continue enriching each company to determine the best match for your use case.
-   **Filter to high-confidence single results:** Add a conditional run formula to skip rows where multiple companies are returned. For example, use `{{IP to Domain Lookup}}?.results?.length` as your condition and only proceed when the value equals `1`.