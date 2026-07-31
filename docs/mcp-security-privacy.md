---
title: MCP Security & Privacy
description: Covers how Clay's MCP connections are authenticated, which workspace roles can use MCP, and how Clay handles data processed through MCP connections.
last_synced: 2026-07-31T17:00:10.419Z
---

# MCP Security & Privacy

Review how MCP connections are authenticated, which roles can use them, and how Clay handles your data.

Clay's MCP (Model Context Protocol) connects your workspace to AI tools like Claude, ChatGPT, Microsoft Copilot, and Glean. Because that means an external application acts on workspace data on a user's behalf, this doc covers how those connections are authenticated, which roles can create them, and how Clay handles the data involved.

**Note:** The Sales Rep permission type described below is in beta and available to select workspaces on request. If you don't see it when inviting a team member, contact Clay support.

## How MCP connections are authenticated

MCP connections use browser-based OAuth — there are no shared secrets or API keys to distribute:

-   A team member starts the connection from their AI tool and signs in to Clay in the browser.
-   They select which Clay workspace to connect. A user who belongs to several workspaces connects each one separately.
-   The resulting access token is scoped to that one user and that one workspace, and Clay stores only a hash of it.
-   A connection only reaches the one workspace it was authorized for, and only the Functions an admin has enabled for MCP. What a user can do through MCP is not identical to what they can do in the web app — see the roles below.

Admins can also limit which applications are allowed to connect at all. Under `Settings → MCP users`, `Allowed MCP clients` controls which platforms members may connect to your workspace's MCP server. Turning a client off blocks new connections to it.

## What each role can do via MCP

A Clay workspace has four permission types, assigned from `Settings → Team`:

-   `Admin` — can edit workspace resources and manage users, and can run anything via MCP.
-   `Editor` — can edit workspace resources, and can run anything via MCP.
-   `Sales Rep` — restricted to MCP only. Reps with this role do not have access to Clay's full web experience, which makes it the tightest way to give someone MCP access and nothing else.
-   `Viewer` — can still trigger runs via MCP. The Viewer restriction governs what the user can do inside the Clay web app, not what they can do through MCP.

Because a `Viewer` can still run via MCP, restricting the web app is not on its own a way to restrict MCP. Use the controls below for that.

## Controls available to admins

Each of these is configured outside this doc — the links go to the full instructions:

-   **Client allow-listing** — restrict which AI platforms can connect, via `Allowed MCP clients`.
-   **Function allow-listing** — Functions are not exposed to MCP until an admin enables them, so reps can only invoke workflows you have approved. See [MCP in Clay](https://university.clay.com/docs/mcp-settings).
-   **Spend limits** — a workspace default credit limit plus per-user overrides cap what any one user can spend. Setting a limit to 0 hard-blocks further actions. See [MCP in Clay](https://university.clay.com/docs/mcp-settings).
-   **Credit budgets** _(Enterprise)_ — named budgets assigned to individual users and groups. See [Credit budgets](https://university.clay.com/docs/credit-budgets).
-   **Removing access** — removing a user from the workspace is the definitive way to cut off their access. Individual MCP connections cannot be revoked from the admin UI.

## Shared responsibility

Clay secures the infrastructure, platform, and data processing layers. Your team controls who reaches them.

**Clay's responsibilities:**

-   Maintain SOC 2 Type II certification, ISO 27001 compliance, and GDPR and CCPA compliance.
-   Encrypt data in transit and at rest.
-   Secure application code and infrastructure.
-   Vet and monitor third-party data providers and AI subprocessors.

The supporting documentation — the SOC 2 Type II report, the current AI subprocessor list, and security questionnaire responses — is available through the [Clay Trust Center](https://trust.clay.com), or by contacting [security@clay.com](mailto:security@clay.com).

**Your responsibilities:**

-   **Decide who gets MCP access** — not every team member needs it. Grant it by role and need, and prefer `Sales Rep` for users who only need MCP.
-   **Decide what MCP can reach** — you choose which Functions and which client applications are enabled.
-   **Brief your team** — prompts a user types into an AI tool are processed by that tool's provider under your organization's agreement with them, not Clay's. Make sure users know which accounts are approved for business use.

## How Clay handles data sent through MCP

When a user triggers an action via MCP:

-   **Data is processed only to fulfill that request.** If a user asks to enrich a company domain, Clay retrieves the enrichment and returns it to complete that specific request.
-   **Your data is never used for AI model training.** Clay holds contractual agreements with all of its AI providers that prohibit training on customer data.
-   **Your data is not shared with other customers.** Workspace data stays logically isolated.
-   **Data is encrypted in transit and at rest.** Clay uses TLS 1.2/1.3 for all data transmission and industry-standard encryption at rest.
-   **You can delete your data at any time.** Deleting a workspace removes all of its data after 30 days.

## FAQs

### How do Anthropic and OpenAI handle prompts sent through MCP?

Both exclude commercial and API customer data from model training by default, and Clay's MCP operates through their commercial APIs. For the per-provider detail on retention and Zero Data Retention eligibility, see the security and data privacy section of [MCP FAQs and troubleshooting](https://university.clay.com/docs/mcp-troubleshooting-and-faqs).

### Can we require that our team only connect from company-managed AI accounts?

Not from Clay. `Allowed MCP clients` controls which platforms can connect to your workspace, but Clay cannot see whether the person connecting is using a company-managed or personal account on that platform. Enforce that through your AI vendor's own admin controls, then use client allow-listing to block platforms you have not approved.

### How do we stop someone from using MCP?

Lowering their role won't do it — a `Viewer` can still trigger runs. To cut off access entirely, remove the user from the workspace. To stop them spending without removing them, set their credit limit to 0, which hard-blocks further actions.

### Does MCP usage appear in our audit and usage reporting?

MCP credit consumption appears in the main dashboard at `Settings → Credit Usage` alongside all other workspace usage, and per-user consumption is visible in the `MCP users` table. Enterprise workspaces using credit budgets can also attribute MCP spend to a specific budget.
