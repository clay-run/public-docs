---
title: Upfluence integration
source_url: https://university.clay.com/docs/upfluence-integration
description: Find collaboration opportunities and engagement strategies through
  enriched influencer profiles.
last_synced: 2026-04-26T01:40:50.960Z
upstream_hash: 0c47e2ed1ae7efb3ebef1f535b328f2db22fcdc75b6a48dc8601c08e9f198bfc
---

# Upfluence integration

Find collaboration opportunities and engagement strategies through enriched influencer profiles.

Upfluence enhances influencer marketing by identifying, retrieving, and validating personal email addresses and comprehensive data across platforms like Instagram, YouTube, and TikTok.

This integration supports targeted outreach, collaboration opportunities, and effective engagement strategies through enriched influencer profiles.

## **Enriching data with Upfluence**

1.  While in a Clay table, click `Add enrichment` and search for `Upfluence`.
2.  Select any of the `Upfluence` actions detailed below.
3.  In the modal, you will be asked to `Select Upfluence account`.
    -   If you have your own account, click `+ Add account` and go through authentication. Otherwise, use the Clay provided key.

### `Action` Find Creator Personal Email

Retrieve the personal email address associated with a creator's social media profile to enable direct outreach and collaboration opportunities.

**Inputs**

-   **Platform:** Select the social media platform (Instagram, TikTok, or YouTube)
-   **Profile URL/Username:** Enter either the full profile URL or username for the selected platform
    -   Instagram: `https://www.instagram.com/username` or just `username`
    -   TikTok: `https://www.tiktok.com/@username` or just `username`
    -   YouTube: `https://www.youtube.com/c/channelname` or just `channel name`

**Output**

-   **Email:** The creator's personal email address (if found)

### `Action` Enrich influencer details

Streamlines the process of gathering and qualifying comprehensive data on influencers for marketing initiatives.

**Inputs**

-   **Social platform (Required):** Select the platform where the influencer is active:
    -   Instagram
    -   TikTok
    -   YouTube
-   **Username / Profile URL / User ID (Required):** Enter one of the following:
    -   Username (e.g., `@johndoe`)
    -   Profile URL (e.g., `https://instagram.com/johndoe`)
    -   Upfluence User ID

**Output**

-   **ID:** Unique identifier in Upfluence's database
-   **Name:** Full name of the influencer
-   **First Name:** Influencer's first name
-   **Last Name:** Influencer's last name
-   **Email:** Contact email address
-   **Phone Number:** Contact phone number
-   **Description:** Influencer's bio or profile description
-   **Country:** Country where the influencer is based
-   **Address:** Geographic location
-   **Gender:** Influencer's gender
-   **Language:** Primary language used
-   **Rating:** Upfluence's rating score
-   **Community Size:** Total number of followers/subscribers
-   **Created At:** Profile creation date
-   **Updated At:** Last profile update date

### `Action` Find Social Profiles by Creator Email

Find social media profiles matching a creator's email address to discover contact information and engagement metrics for influencer outreach.

**Inputs**

-   **Email address:** The creator's email address to look up

**Output**

-   **Basic Profile Information:**
    -   Name (First and Last name)
    -   Description/Bio
    -   Profile picture URL
    -   Location details
    -   Gender
    -   Primary language
-   **Contact Information:**
    -   Phone number (if available)
    -   Agent email (for business inquiries)
    -   Shipping address
-   **Location Information:**
    -   Country
    -   Full address
    -   Location origin
-   **Profile Metrics:**
    -   Rating
    -   Verification status
-   **Additional Details:**
    -   Created date
    -   Last updated date
    -   Associated tags
    -   Custom merge fields

### **Run settings**

-   **Auto-update**
-   **Only run if:** The enrichment will only run if conditions are met. ([Learn more about conditional formulas here!](https://www.clay.com/university/lesson/ai-formulas-conditional-runs-clay-101))
