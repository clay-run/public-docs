---
title: CLI security & privacy
description: How Clay CLI sessions are authenticated, which roles can use the CLI, why bulk routine runs from the CLI ask for approval and how to always allow a workflow, the shared security responsibilities, and how Clay handles data sent from your terminal.
last_synced: 2026-10-19T18:12:06.412Z
---

# CLI security & privacy

Understand CLI authentication, role requirements, and how Clay handles data sent from your terminal.

Clay's CLI lets your team drive a Clay workspace from a terminal or coding agent instead of the UI. Because that means credentials live on a local machine and commands run outside the app, admins need to know who can sign in and what those sessions can reach.

**Note:** The CLI is part of Clay's Agent Plugin, which is in open beta and currently supported on Mac and Linux. Windows is not supported during the beta.

## How CLI sessions are authenticated

The recommended path is browser-based OAuth:

-   Running `clay login` opens a browser sign-in and completes the flow back to the local machine. Nothing is copied and pasted, and no client secret is involved.
-   On a machine with no browser — an SSH session, a container, or a headless server — `clay login --device` prints a link and a code to open on any other device instead.
-   Either flow is validated against Clay before anything is written to disk, so a failed sign-in leaves no credential behind.
-   Credentials are written to a local config file at `~/.config/clay/config.json`, created with owner-only file permissions. Treat that file like any other credential on disk — it is not stored in your operating system's keychain.
-   Running `clay logout` clears the stored credentials for that machine.

API keys are for calling the Clay public API directly — they don't sign in to the CLI. To create one, open `API and CLI` in the left sidebar and select the `API keys` tab, or run `clay api-keys create --name "<key name>"` from a signed-in CLI. `Admin`, `Editor`, and `Viewer` users can create keys; `Sales Rep` users can't. The older key under `Settings → Account → API key (legacy)` doesn't work with the public API.

## Which roles can use the CLI

CLI access is restricted to the two permission types that can already edit workspace resources:

-   `Admin` and `Editor` — can sign in to the CLI.
-   `Viewer` and `Sales Rep` — cannot. Sign-in fails with `Editor access required`, and CLI-backed endpoints reject the request even if the user holds an API key. `Sales Rep` is in beta, so it only appears in workspaces that have requested it.

Because the check runs again whenever a CLI session refreshes its credentials, removing a user from the workspace or lowering their role below `Editor` also invalidates their existing CLI session — it does not keep working until it expires.

## Why bulk routine runs from the CLI ask for approval

On paid plans, starting a bulk routine run from the Clay CLI — for example `clay routines runs start workflow:<id> --bulk <file>` — is held for a human to approve before it runs. Instead of starting the run, the CLI returns an `approval_required` error with the action `routines.run-batch` and an approval request ID in `details.actionApprovalRequestId` (it starts with `aar_`). Clay holds these runs because a workflow's steps can act outside Clay, such as writing to a CRM, and credits are charged for each item in the file.

To handle a held bulk run from the CLI:

1.  Run `clay approvals get <requestId>` to see what the run will do and how many items it covers.
2.  Run `clay approvals approve <requestId>` to start the run, or `clay approvals deny <requestId>` to cancel it.
3.  After you approve, the run starts with the same input you submitted — you don't need to rerun the original command.

### Can an admin turn off approvals for bulk CLI runs?

No. There's no workspace setting that turns off approval for bulk routine runs from the CLI, and admins can't pre-approve workflows on behalf of other users. Each user can instead always allow a specific workflow for themselves, as described below.

### How to always allow a workflow so bulk runs start without approval

To stop approving every batch for a workflow you run often, approve one held request with `--always-allow`:

`clay approvals approve <requestId> --always-allow`

This approves the current run and saves a rule, so later bulk runs of that same workflow that you start from the CLI begin straight away. The rule covers only that one workflow or routine, only your user, and only that workspace — other workflows and other teammates still need approval. Rules don't expire. To review or remove them:

-   `clay approvals rules list` shows the rules you've saved.
-   `clay approvals rules delete <ruleId>` removes a rule, so that workflow asks for approval again.

The `--always-allow` option needs Clay CLI version 1.14.0 or later. If `clay approvals approve` doesn't accept it, update your CLI.

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
-   **Rotate and remove API keys** — keys don't expire on their own, so rotate them on a schedule and delete any that are no longer needed from the `API keys` tab.

## How Clay handles data sent through the CLI

When your team runs a CLI command:

-   **Data is processed only to fulfill that request.** If a user runs an enrichment command, Clay retrieves the enrichment and returns it to complete that specific request.
-   **Clay does not use your customer data to train or fine-tune any AI models, except when solely for your benefit and use within your own Clay workspace, for example to build your Knowledge Hub.** Clay holds contractual agreements with all of its AI providers that prohibit training on customer data.
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

### Can an API key do things the CLI cannot?

No. An API key works only with the Clay public API and only in the workspace it was created in, so it reaches less than a CLI session does, never more. It also differs in lifetime: it doesn't expire on its own and isn't tied to a browser session, which is why rotating and deleting keys matters more than it does for `clay login`.
