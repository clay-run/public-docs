---
title: Installing Clay Plugin (API & CLI)
description: Install the Clay Plugin and CLI into Claude Code or Codex on Mac or Windows, connect your workspace, and start using the API and CLI across all Clay plans.
last_synced: 2026-09-22T21:46:44.834Z
---

# Installing Clay Plugin (API & CLI)

Install the Clay Agent Plugin, sign in from any environment, and see what the API and CLI can do on your plan.

This doc walks you through installing the Clay Plugin and connecting it to your workspace — on Mac or Windows, in Claude Code or Codex.

Once it's set up, you can use Clay from coding agents, terminals, and your own apps to run searches over Clay's GTM dataset, call enrichment functions, and build Workflows, all using Clay's existing integrations and data infrastructure.

**Already set up?** Head to [**Guide: Using Clay Plugin**](/docs/using-clay-plugin) for go-to-market plays you can run once the Plugin is connected — source your market, score it for fit, and route who gets worked first.

**Note:** The Plugin installs Clay's skills and the Clay CLI into your coding agent. It doesn't include an MCP server, so installing the Plugin doesn't give your agent the MCP for Reps toolset — that connection is set up separately.

Setup takes about 15 minutes on Mac and 30 on Windows. You'll need:

-   **A paid coding agent plan:** Claude (Pro, Max, Team, or Enterprise) for Claude Code, or ChatGPT (Plus, Pro, Business, Edu, or Enterprise) for Codex. If your company manages Claude, check that Claude Code is enabled for you.
-   **Editor or Admin access** in the Clay workspace you'll connect.
-   **On Windows, admin rights** (or help from IT) for one step.

<div style="background-color: #FDFBF0; padding: 16px; border-radius: 8px; border: 1px solid #F4E8C1; font-family: Arial, sans-serif;"> <strong>Note:</strong> If pasting turns two hyphens (--) into a long dash (—), retype the hyphens by hand, or the command will fail. </div>

## Quick setup with any agent

Already have a coding agent, like Claude Code, Codex, or Cursor? Give it this prompt:

`Set up the Clay Plugin by following the steps in <https://github.com/clay-run/agent-plugins>`

Your agent installs the Plugin, sets up the `clay` command, and signs you in. On Windows, install WSL first and run the prompt inside Ubuntu (see **Set up on Windows**).

### Setup guide

Starting from scratch, or stuck? Follow the steps for your operating system.

## Set up on Mac

These steps also work on Linux — use `~/.bashrc` instead of `~/.zshrc`.

### Claude Code

**1\. Install Claude Code.** Open Terminal and run:

`curl -fsSL <https://claude.ai/install.sh> | bash   `

If the output says `~/.local/bin` isn't in your PATH, run:

`echo 'export PATH="$HOME/.local/bin:$PATH"' >> ~/.zshrc && source ~/.zshrc   `

**2\. Sign in.** Run `claude`, accept the defaults, and sign in with your Claude account in the browser.

**3\. Install the Clay Plugin.** At the `>` prompt, run these one at a time:

`/plugin marketplace add clay-run/agent-plugins   /plugin install clay@clay-plugins   `

Choose `Install for you (user scope)` when asked.

**4\. Connect your workspace.** Run `/clay:setup` and approve its checks. In the browser, sign in to Clay, pick your workspace, and click `Authorize`. You're done when Terminal shows `Setup complete`.

<div style="background-color: #FDFBF0; padding: 16px; border-radius: 8px; border: 1px solid #F4E8C1; font-family: Arial, sans-serif;"> <strong>Note:</strong> Prefer the desktop app? Quit and reopen it after setup, and the Plugin is available in the <code>Code</code> tab. </div>

### Codex

**1\. Install Codex.** Open Terminal and run:

`curl -fsSL <https://chatgpt.com/codex/install.sh> | sh   `

**2\. Sign in.** Run `codex` and sign in with your ChatGPT account.

**3\. Add the Clay Plugin.** Exit Codex, then run:

`codex plugin marketplace add clay-run/agent-plugins   `

Start `codex` again, open `Plugins`, and install `clay`.

**4\. Connect your workspace.** Run the `clay:setup` skill, or paste the quick setup prompt if Codex doesn't recognize it. Approve the step that adds `clay` to your PATH, open the sign-in link it gives you, pick your workspace, and click `Authorize`. Then restart Codex (`/exit`, then `codex`) and ask it to run `clay whoami` to confirm.

### Troubleshooting

-   **`command not found: claude`** — run the PATH command from step 1.
-   **Claude replies in sentences instead of running a command** — retype it with the leading `/`.
-   **`/clay:setup` shows `Unknown command`** — restart Claude Code (`/exit`, then `claude`) and try again.
-   **Clay's `Authorize` page won't let you through** — you need Editor or Admin access in that workspace.
-   **You connected the wrong workspace** — ask your agent to run `clay login` and pick again.
-   **The sign-in link expired** — links last about 5 minutes. Start again and use the newest one.

## Set up on Windows

On Windows, the Plugin runs inside WSL (Windows Subsystem for Linux). Run everything in the Ubuntu window (its prompt ends in `$`), not PowerShell (`PS C:\`), where Claude Code, Codex, and `clay` don't work.

### Install WSL (both agents)

Right-click the Start button, open `Terminal (Admin)`, and run:

`wsl --install   `

Restart if asked, open `Ubuntu` from the Start menu, and create a username and password (the password stays hidden as you type).

**Note:** This is the only step that needs admin rights. If it fails with `requires elevation`, ask IT to run `wsl --install` for you.

### Claude Code

**1\. Install Claude Code.** In the Ubuntu window, run:

`curl -fsSL <https://claude.ai/install.sh> | bash   `

Then add it to your PATH:

`echo 'export PATH="$HOME/.local/bin:$PATH"' >> ~/.bashrc && source ~/.bashrc   `

**2\. Sign in.** Run `claude`. The browser won't open from WSL, so:

1.  Press `c` to copy the sign-in link and open it in your Windows browser.
2.  Sign in and click `Copy code`.
3.  Paste the code into the Ubuntu window and press `Enter`.

**3\. Install the Clay Plugin.** At the `>` prompt, run these one at a time:

`/plugin marketplace add clay-run/agent-plugins   /plugin install clay@clay-plugins   `

Choose `Install for you (user scope)` when asked.

**4\. Connect your workspace.** Run `/clay:setup` and approve its checks (the selector sometimes defaults to `No`). Open the sign-in link in your Windows browser, pick your workspace, and click `Authorize`.

**Note:** Using the desktop app's `Code` tab on Windows? Install Git for Windows first.

### Codex

**1\. Install Codex.** In the Ubuntu window, run:

`curl -fsSL <https://chatgpt.com/codex/install.sh> | sh   `

**2\. Sign in.** Run `codex` and open the sign-in link it prints in your Windows browser.

**3\. Add the Clay Plugin.** Exit Codex, then run:

`codex plugin marketplace add clay-run/agent-plugins   `

Start `codex` again, open `Plugins`, and install `clay`.

**4\. Connect your workspace.** Same as on Mac, but open the sign-in link in your Windows browser.

### Troubleshooting

-   **`not recognized`** — you're in PowerShell. Type `wsl` to switch to Ubuntu.
-   **`wsl --install` says `requires elevation`** — run it from `Terminal (Admin)`, or ask IT.
-   **You pasted the sign-in code and nothing happened** — press `Enter`.
-   **The sign-in link won't load** — it likely broke when copied across lines. Ask your agent to copy it to your clipboard with `clip.exe`.
-   **The browser shows an error on `127.0.0.1` after you click `Authorize`** — usually a corporate VPN. Sign in with `clay login --device` instead (see below).
-   **Anything else** — the Mac troubleshooting fixes above apply on Windows too.

## Signing in without a browser

The `clay login` command signs you in by opening a browser on the machine you're working on. That isn't possible everywhere — on a remote server, inside a container, or in an automated pipeline, there's no browser for it to open.

In those cases, run `clay login --device` instead. It prints a link and a short code, and you approve the sign-in from a browser on any other device — your laptop or phone works fine.

1.  Run `clay login --device`. The CLI prints a verification link with your code pre-filled, prints the code on its own, and then waits for approval.
2.  Open the link in a browser on any device, and sign in to Clay if you aren't already.
    -   If you enter the verification URL without the code, Clay shows `Connect a device` — type the code from your terminal into the `Code` field and click `Continue`.
3.  On `Connect Clay CLI`, check that the code on screen matches the one in your terminal, choose a workspace under `Which workspace should Clay CLI connect to?`, and click `Authorize`. To reject the request, click `Deny`.
4.  The browser confirms `Device connected` and the CLI finishes signing in on its own — there is nothing to paste back into your terminal.

**Note:** The code expires 10 minutes after the CLI prints it, and it can only be approved once. If it expires before you approve it, or you deny the request, run the command again to get a new code.

For the full CLI quickstart, Public API setup, code examples, and guides for Searches, Routines, and Workflows, see [**developers.clay.com**](https://developers.clay.com/).

## What you can do

The Plugin has two primary features:

-   **CLI** — Build GTM workflows in natural language from coding agents (including Claude Code, Codex, and Cursor).
-   **Public API** — Access data from Clay or 200+ vendors in the data marketplace. Trigger functions, Claygents, or workflows.

Both paths consume the same credits and actions as equivalent in-product work. There is no additional cost to use the Plugin.

The Plugin also gives you access to:

-   [**Audiences**](https://university.clay.com/docs/audiences) — Read and segment the workspace's own people, companies, and deals. See [**Audiences for agents and the CLI**](https://university.clay.com/docs/audiences-for-agents).
-   [**Searches**](https://university.clay.com/docs/search) — Find companies and people using structured filters over Clay's GTM dataset. Learn more about Searches in [this video walkthrough](https://www.loom.com/share/6a125988c8b14b89aded2e75b8265d5c).
-   [**Functions**](https://university.clay.com/docs/functions) — Run [**managed functions**](https://university.clay.com/docs/managed-functions) and custom functions. Learn more about functions in [this video walkthrough](https://www.loom.com/share/7050c0b62b0648a984d6438112d02985).
-   [**Workflows**](https://university.clay.com/docs/workflows) — Enrichment, research, scoring, routing, and other repeatable GTM logic.
-   **Tables** — Read structured data from known Clay tables.
-   [**Sequencer**](https://university.clay.com/docs/getting-started-with-sequencer) — Build and edit campaign sequences, run variant tests, and read analytics from the CLI. Launching, pausing, and resuming a campaign stay in the Clay app.

**Note:** The CLI and API run on Mac and Linux. On Windows, they run through WSL — there's no native Windows (PowerShell) version of the CLI.

## Plan availability and limits

The developer platform is available across all Clay plans, including free and trial plans. Legacy plans also have access for a limited time.

Search result limits vary by plan:

| Plan | Search results per request | Total search results |
| --- | --- | --- |
| Free | 50 | 100/mo |
| Trial | 50 | 10k per 14 days |
| Paid self-serve plans | 500 | 1M/yr |
| Enterprise | 500 | 10M/yr |

## FAQs

### Does using the API or CLI cost extra credits?

No. API and CLI calls consume the same credits and actions as the equivalent work done in-product. There is no additional cost because work is triggered via the developer platform instead of the UI.

### What's the difference between the Plugin and the Public API?

The Plugin gives agent environments (Claude Code, Codex, Cursor) Clay's skills and the Clay CLI — the fastest path for agent-first and interactive coding workflows. The Public API is better suited for background jobs and your own apps, where you want to call Clay directly instead of installing anything.

The Public API uses its own key rather than your CLI sign-in. Create one with the `clay api-keys create` command — the key is shown only once, so store it somewhere safe.

### What's the difference between MCP for Reps and the CLI/API?

They're separate surfaces, not two halves of one product. The Plugin installs Clay's skills and the Clay CLI into your coding agent, and the CLI is what you or your agent run in a shell for one-off runs, scripting, and inspecting data. It authenticates with the session created by `clay login`, so there's no separate key to configure.

MCP for Reps is a different connection, set up separately by an admin for sellers working in chat apps and coding agents. It comes with its own Functions and per-rep credit budgets. See [**MCP in Clay**](https://university.clay.com/docs/mcp-settings) for how that access is configured.

### Can I build or write to Clay tables via CLI or API?

No. The CLI builds logic via Workflows, not tables. `Tables` in the Public API is read-only — you can query and read rows, but not create tables, add fields, or write records.

Basic row reads work on any plan. Structured queries — joins, ranges, and paging past 100 rows — need API table sync, an Enterprise feature. There are no current plans to support table building from the API or CLI.

### Can I build Workflows with the API or CLI?

Yes, Workflows are available from the CLI and Plugin in `Beta`. For production use, Clay-managed functions and custom functions are the more stable option.

### Are credit budgets available via the developer platform?

Credit budgets aren't available on the developer platform yet. You can see run-level credit and action consumption from the `Runs` view in Workflows. Credit budget support is on the roadmap.

### Who can approve a device sign-in?

Whoever opens the verification link. They need to be signed in to Clay in that browser and have editor access to at least one workspace, since the sign-in is tied to the workspace they pick, not to the machine running the command. If they don't have editor access anywhere, the page shows `Editor access required` instead of the authorization screen.
