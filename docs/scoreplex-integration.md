---
title: scoreplex-integration
description: How to use the Scoreplex integration in Clay to validate contact information, detect fraud risk, and discover social profiles across 25+ platforms.
last_synced: 2026-06-29T22:02:44.028Z
---

# Scoreplex integration

Validate contact information, detect fraud risk, and discover social profiles

Scoreplex is a digital identity verification and fraud detection tool for lead validation and risk assessment.

With this integration, you can validate contact information, detect fraud risk, and discover social profiles across 25+ platforms.

## Enriching data with Scoreplex

1.  In your Clay table, click `Add enrichment`.
2.  Search for **Scoreplex** and select it from the results.
3.  In the modal, you will be asked to `Select Scoreplex account`.
    -   If you haven't already connected your Scoreplex account, click `+ Add account` and go through authentication. Otherwise, use the Clay-provided key.

### `Action` Find fraud risk

Analyzes email and phone inputs to return validation signals, breach history, social platform presence, and fraud risk scoring.

**Inputs**

Required:

-   Email address: The email to analyze.
-   Phone number: The phone number to analyze.

Optional:

-   IP address: Unlocks IP-level fraud signals and geolocation.
-   First name: Helps validate identity matches.
-   Last name: Helps validate identity matches.

**Outputs**

-   Email validation: Deliverability status, disposable email detection, format validation.
-   Phone validation: Carrier type, line type (mobile/landline/VoIP), country code verification.
-   IP validation: Proxy/VPN detection, geolocation, ISP information.
-   Fraud risk score: Composite risk score based on digital footprint analysis.
-   Breach exposure: Known data breaches associated with the email address.
-   Compromised credentials: Historical password leaks or account compromises.
-   Social platform presence: Detected accounts across 25+ platforms including:
    -   Professional networks: GitHub, AngelList, Crunchbase, and other professional networking sites.
    -   Social media: Twitter/X, Instagram, Facebook, TikTok, Telegram, WhatsApp, Skype.
    -   Other platforms: PayPal, TrueCaller, Xing, plus dating, gambling, crypto, and adult platforms.
-   Inferred identity: First name, last name, approximate age or age range, location (city, state, country).
-   Employer: Current or recent employer (when available).

### Run settings

**Auto-update**

Automatically re-runs the enrichment when new rows are added to the table. Recommended when you are regularly adding new contacts and want enrichment to stay current.

**Only run if**

Set conditions to run this enrichment only when specific criteria are met. Use [conditional formulas](https://www.clay.com/university/lesson/use-formulas-in-claygent) to control when the action runs.

## Best practices

**Qualify leads before enrichment**

Use Scoreplex after basic lead qualification to avoid spending credits on low-quality contacts. Filter out obvious bounces or test emails first.

**Handle sensitive data responsibly**

Scoreplex returns sensitive information including breach history and presence on adult content, dating, and gambling platforms. Only enrich contacts you have a legitimate business reason to investigate, handle data securely, and ensure compliance with GDPR, CCPA, and other applicable data privacy laws.

**Use for fraud screening**

For PLG or self-serve signups, flag high-risk users by checking for disposable emails, VPN/proxy IPs, high fraud scores, or absence of social presence.
