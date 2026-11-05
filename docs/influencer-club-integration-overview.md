---
title: Influencer club integration overview
description: Creator data and outreach platform.
last_synced: 2026-04-26T01:40:10.989Z
---

# Influencer club integration overview

Creator data and outreach platform.

## Influencer Club Overview

The Influencer Club integration in Clay provides access to creators' verified contact information and social media profiles across popular platforms like TikTok, Instagram, YouTube, OnlyFans, and more.

### Setting up Influencer Club and Clay

You can connect and pay for Influencer Club enrichments in two options.

1.  **Clay-managed account**: Utilize your Clay Credits to pay for enrichments utilizing the credits available in your Clay account.
2.  **(Only available to paid Clay users) Influencer Club account via API key**: Use your Influencer Club account credits by integrating your API key into Clay.

## **Available Actions with the Influencer Club Integration**

### `Action` **Find social profiles by creator email**

Use this action to find a creator's social media profile URLs from their email address. Returns profile links for Instagram, TikTok, YouTube, Twitch, OnlyFans, Linktree, and Patreon.

**Setup Inputs**

-   **Email address**: Enter the creator's email address.

### `Action` **Find Creator Personal Email**

Use this action to retrieve a creator's personal email address based on their existing profile URL.

**Setup Inputs**

-   **Profile URL**: Enter the profile URL of the creator on platforms such as Instagram or TikTok to locate their personal email.

### `Action` **Find Creator Phone Number**

Use this action to retrieve a creator's phone number based on their profile URL.

**Setup Inputs**

-   **Profile URL**: Enter the creator's profile URL on a supported social media platform to find their phone number.

### `Action` **Find all social profiles from one**

Use this action to find all social media profiles associated with a creator based on an existing profile URL, username, or Influencer Club user ID.

**Setup Inputs**

-   **Social platform**: Select the platform of the profile you are providing (e.g., Instagram, TikTok, YouTube).
-   **Profile URL, username, or user ID**: Enter the creator's existing profile URL, username, or Influencer Club user ID.
