---
title: CLI Security & Privacy
description: Explains how to authenticate Clay's CLI, which workspace roles can use it, and how Clay handles data from terminal sessions.
last_synced: 2026-07-31T17:01:53.268Z
---

# CLI Security & Privacy

Understand CLI authentication, role requirements, and how Clay handles data sent from your terminal.

Clay's CLI lets your team drive a Clay workspace from a terminal or coding agent instead of the UI. Because that means credentials live on a local machine and commands run outside the app, admins need to know who can sign in and what those sessions can reach.

<div style="background-color: #FDFBF0; padding: 16px; border-radius: 8px; border: 1px solid #F4E8C1; font-family: Arial, sans-serif;">

<strong>Note:</strong> The CLI is part of Clay's Agent Plugin, which is in open beta and currently supported on Mac and Linux. Windows is not supported during the beta.

</div>

## How CLI sessions are authenticated

The recommended path is browser-based OAuth:

-   Running `clay login` opens a browser sign-in and completes the flow back to the local machine. Nothing is copied and pasted, and no client secret is involved.
-   On a machine with no browser — an SSH session, a container, or a headless server — `clay login --device` prints a link and a code to open on any other device instead. Reach for this rather than falling back to an API key.
-   Either flow is validated against Clay before anything is written to disk, so a failed sign-in leaves no credential behind.
-   Credentials are written to a local config file at `~/.config/clay/config.json`, created with owner-only file permissions. Treat that file like any other credential on disk — it is not stored in your operating system's keychain.
-   Running `clay logout` clears the stored credentials for that machine.

API keys remain available as a legacy fallback and can be found under `Settings → Account → API keys (beta)`. New setups should use `clay login` instead — API keys are a long-lived shared secret with no browser flow behind them, and Clay intends to deprecate them.

## Which roles can use the CLI

CLI access is restricted to the two permission types that can already edit workspace resources:

-   `Admin` and `Editor` — can sign in to the CLI.
-   `Viewer` and `Sales Rep` — cannot. Sign-in fails with `Editor access required`, and CLI-backed endpoints reject the request even if the user holds an API key. `Sales Rep` is in beta, so it only appears in workspaces that have requested it.

Because the check runs again whenever a CLI session refreshes its credentials, removing a user from the workspace or lowering their role below `Editor` also invalidates their existing CLI session — it does not keep working until it expires.

## Shared responsibility

Clay secures the infrastructure, platform, and data processing layers. Your team controls who reaches them.

**Clay's responsibilities:**

-   Maintain SOC 2 Type II certification, ISO 27001 compliance, and GDPR and CCPA compliance.
-   Encrypt data in transit and at rest.
-   Secure application code and infrastructure.
-   Vet and monitor third-party data providers and AI subprocessors.

The supporting documentation — the SOC 2 Type II report, the current AI subprocessor list, and security questionnaire responses — is available through the [Clay Trust Center](https://trust.clay.com), or by contacting [security@clay.com](mailto:security@clay.com).

**Your responsibilities:**

-   **Decide who gets CLI access** — CLI access implies edit rights on the workspace. Grant `Editor` deliberately.
-   **Protect local credentials** — the config file on a developer's machine is a live workspace credential. Include it in your device security and offboarding process.
-   **Prefer OAuth over API keys** — and where a legacy API key is still in use, rotate it on a schedule and revoke it as soon as it is no longer needed.

## How Clay handles data sent through the CLI

When your team runs a CLI command:

-   **Data is processed only to fulfill that request.** If a user runs an enrichment command, Clay retrieves the enrichment and returns it to complete that specific request.
-   **Your data is never used for AI model training.** Clay holds contractual agreements with all of its AI providers that prohibit training on customer data.
-   **Your data is not shared with other customers.** Workspace data stays logically isolated.
-   **Data is encrypted in transit and at rest.** Clay uses TLS 1.2/1.3 for all data transmission and industry-standard encryption at rest.
-   **You can delete your data at any time.** Deleting a workspace removes all of its data after 30 days.

## FAQs

### If we drive the CLI from a coding agent, what does that agent's provider see?

The CLI itself communicates only with Clay. But when you run it through a coding agent, whatever you type into that agent — and whatever command output it reads back — is processed by that agent's provider under your agreement with them, not Clay's. Treat prompts and terminal output as data you are sharing with that provider, and apply the same account rules you would to any other AI tool.

### Does removing a user also disable API keys they created?

Yes. A key is tied to the user who created it, so it stops working when they lose workspace access — you don't need to track down and revoke each key separately. Clearing the credential file from their device is still good offboarding practice, but it isn't what cuts off access.

### Do CLI commands consume credits differently from work done in the app?

No. CLI runs consume the same credits and actions as the equivalent work in-product, with no surcharge for using the developer platform. See [Clay API & CLI](https://university.clay.com/docs/clay-api-cli) for plan availability and search limits.

### Can a legacy API key do things the CLI cannot?

An API key inherits the permissions of the user who created it, so it cannot exceed that user's workspace access. It differs from an OAuth session in lifetime rather than reach: it does not expire on its own and is not tied to a browser session, which is why rotating and revoking keys matters more than it does for `clay login`.
