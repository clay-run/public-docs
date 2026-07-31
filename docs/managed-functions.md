---
title: Managed functions
description: How to add, configure, and manage Clay's pre-built managed enrichment functions, and expose them as callable tools for AI assistants via MCP.
last_synced: 2026-07-31T18:04:36.481Z
---

# Managed functions

Learn how to add ready-made functions from Clay's catalog, make them callable from your team's AI tools, and customize one when the catalog doesn't quite fit.

Clay managed functions are ready-made Functions that Clay builds and maintains for you. Add one from Clay's catalog and it works out of the box—no table to build—and Clay keeps it up to date automatically.

**Note:** Clay managed functions are rolling out. If you don't see them in your workspace yet, they're on the way.

## What are Clay managed functions

A Function packages an enrichment workflow into a single, reusable building block you can call from a table, from the API or CLI, or from a rep's AI tool. (For the fundamentals, see [Functions](https://university.clay.com/docs/functions).)

There are two kinds of Functions:

-   **Managed functions** — a curated set that Clay builds and maintains. You add them from Clay's catalog, and Clay updates the underlying logic over time so results stay current without any work on your end.
-   **Custom functions** — the ones you build yourself from a table.

Managed functions cover common company and person research jobs, so your team gets value without building anything first.

## Available managed functions

Each managed function takes a small set of inputs and returns a standardized output. Clay's catalog focuses on company and person GTM jobs, including:

-   **Estimate Company IT Spend:** Given a company name and domain (plus optional details like industry and description), return annual revenue, IT spend (with reasoning), and the tech stack.
-   **Find Recent Company Developments:** Given a company name, profile, domain, and a lookback window in months, return a summary of notable news, including M&A, product updates, and executive hires.
-   **Get Company Hierarchy:** Given a company name and domain, return parent companies, subsidiaries, and the full hierarchy (with reasoning).
-   **Get Funding and Expansion Events:** Given a company name and domain, return M&A, funding, or expansion news from the last 2 years.
-   **Validate Company Domain:** Given a company domain, return the validated company name and domain (with reasoning), including whether the provided name was correct and, if not, why.
-   **Validate Professional Profile and Employment:** Given any information about a person, validate their name, employer, role, and other professional-identity details. All inputs optional; more inputs increase accuracy.
-   **Full Tech Stack:** Given a company domain, return a consolidated tech stack with normalized provider lists and detection data across many categories (automation, communication, CRM, data management, dev tools, ecommerce, ERP, finance, HR, logistics, marketing, marketplace, security, support).
-   **Generate ICP Fit:** Given a customer name, domain, and profile URL, return an ICP fit score and tier plus enriched company info.
-   **Infer Digital Transformation Initiatives:** Given a company name, domain, and profile URL, return whether the company has active digital-transformation initiatives, each with a summary and source links.
-   **Track Job Change Status:** Given a person's profile, employer, and title, return whether they've changed companies or titles, with the new company and/or title.

## Adding a managed function

1.  In your workspace, open `Functions` from the sidebar.
2.  Click `New` (or `New` → `Function`) to open `Browse Clay managed functions`.
    -   Use the search box and the category list to find a function. The filter toggle switches between `Only show functions not in workspace` and `Show all managed functions`.
3.  Select a function to preview its `Inputs`, `Steps`, `Outputs`, and estimated cost per row. A function tagged `Requires API key` needs a provider key to run. In the preview, each key is listed as either `Provided` (Clay supplies the connection) or `Required at use` (you choose an account during setup).
4.  Click `Setup as managed` and complete the setup steps:
    -   `Required API keys` — choose an account for any connection marked `Selection required`. Keys Clay already supplies don't block setup.
    -   `Tools` — choose where the function is available (see [Using managed functions with MCP](#)).
    -   `Access permissions` — set `Edit access` to `Admins and editors in this workspace` or `Admins and invited collaborators only`.
5.  Click `Add to workspace`. The function appears under the `Clay managed` view on the Functions homepage, marked with a Clay badge.

## Using managed functions with MCP

Managed functions become callable from AI tools like Claude and ChatGPT when you expose them as a tool during setup.

1.  When adding (or later editing) a managed function, go to the `Tools` step.
2.  Select the `MCP` checkbox — "Allow this function to be called from ChatGPT and other MCP clients".
3.  Set the `Routine name` and `Description`. This is how the function appears to the AI, so make it clear and actionable — good names and clean inputs are what let the agent pick the right function and call it correctly.
4.  Finish setup. Reps who have connected Clay to their AI tool can invoke the function by name. It runs asynchronously and returns results to the records the rep points it at.

To change MCP settings for a function you've already added, open it and use the `Integrations` section.

Setting up rep access, credit budgets, and per-tool connection guides is covered in [MCP in Clay](https://university.clay.com/docs/mcp-settings).

**Note:** MCP access is gated to specific plans, so the MCP checkbox is unavailable on plans that don't include it. Check the MCP in Clay doc for the current plan requirements.

## Editing and managing managed functions

-   **Find them.** Added managed functions live under the `Clay managed` view on the Functions homepage, each marked with a Clay badge (tooltip: "Function managed by Clay").
-   **They stay current.** Clay maintains the logic in each managed function, so added functions improve automatically.
-   **Customize one.** To change a managed function's logic, first detach it from Clay's updates:
    -   For a function already in your workspace, use `Detach and edit`. Clay confirms with `Detach from Clay updates?` — this cannot be undone.
    -   For one you haven't added yet, use `Duplicate as custom` to create an editable copy.
    -   Either way, the copy becomes a custom function and stops receiving Clay's managed updates.
-   **Remove one.** Use `Remove from workspace`. Runs and configuration tied to the workspace copy are no longer available, but you can add the function again later.

## Managed vs. custom functions

|  | Managed functions | Custom functions |
| --- | --- | --- |
| Built and maintained by | Clay | You |
| Updates | Automatic, as Clay improves them | Only when you edit them |
| Editing | Not editable while managed — Detach and edit or Duplicate as custom first | Fully editable |
| Getting started | Add from Browse Clay managed functions | Build with Save as function from a table |
| Enabling for MCP | Supported | Supported |

Use a managed function when Clay already offers the enrichment or research job you need. Build a custom function when you have a specific play Clay's catalog doesn't cover.

## FAQs

### Do managed functions cost extra credits?

No. There's no surcharge for running a function. Credits are consumed by the individual enrichment steps inside it, attributed to wherever the function runs — a table or a rep's AI tool. While browsing the catalog, each function shows an estimated cost per row.

### Do I need my own API keys?

Some managed functions call third-party providers and are tagged `Requires API key`; you pick which connected account to use during the `Required API keys` step. Others run entirely on Clay's data and need no key.

### Can I change a managed function's inputs or logic?

Not while it remains managed. Use `Detach and edit` (or `Duplicate as custom` for one you haven't added) to create an editable copy — which stops it from receiving Clay's updates.

### Is there anything MCP-specific about managed functions?

No. Once a function is enabled for `MCP`, managed and custom functions behave the same way for reps in their AI tool. Managed functions simply save you the step of building the workflow first.
