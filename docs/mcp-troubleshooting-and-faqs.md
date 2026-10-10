---
title: MCP troubleshooting and FAQs
description: Troubleshooting steps and FAQs for common issues with Clay's MCP integration, covering connection errors, function problems, ChatGPT-specific behavior, credits, and data privacy.
last_synced: 2026-07-13T20:05:27.051Z
---

# MCP troubleshooting and FAQs

Answering the most common questions regarding MCP

## **Troubleshooting**

### **Diagnosing a problem: is it Clay or the AI tool?**

This is the most important first step, and the hardest to call without a framework. The clearest way to triage:

Open your browser's Dev Tools (`right-click → Inspect` → **Network** and **Console** tabs) and reproduce the failing action. Then look at what you see:

-   **If the request never leaves the AI tool, or you see a 403 error on an OpenAI endpoint** (e.g. `/backend-api/ecosystem/call_mcp`), the block is happening at the AI tool's layer — not Clay. Your admin needs to enable the app or actions at the org level in ChatGPT or your AI tool's admin settings.
-   **If the tool call reaches Clay and errors there** (e.g. a Function won't enable, integration settings error, or enrichment returns blank), it's Clay-side and the troubleshooting steps below apply.

A useful rule of thumb: when the same prompt works in Claude but fails in ChatGPT, the cause is usually a ChatGPT org-level restriction rather than anything in your Clay configuration.

### **Connection and authentication errors**

#### **"Client name must not impersonate a known platform"**

This error appears when a user tries to connect Clay via the CLI (`claude mcp add`) instead of using the official connector. Clay's OAuth flow rejects CLI-initiated connections by design.

**Fix:** Run `claude mcp remove clay` in your terminal, then connect through the official connector at [**claude.com/connectors/clay**](https://claude.com/connectors/clay) or via `Claude → Settings → Connectors`.

#### **Rep connected to a personal workspace instead of the company workspace**

This happens when a rep runs the Clay MCP connection flow in their AI tool _before_ accepting their Clay workspace invite. The OAuth flow spins up a personal workspace instead of connecting to the company workspace, and the rep won't appear in `Settings → MCP users`.

**Fix:**

1.  Have the rep disconnect Clay from their AI tool's connector settings.
2.  Accept the workspace invite via email first.
3.  Reconnect Clay in the AI tool and select the company workspace during re-auth.

If the original invite expired, resend it from `Settings → Team`.

#### **Viewer-role users can't complete the MCP OAuth flow**

The Viewer role doesn't have permission to complete the MCP connection. Upgrade the user to **Sales Rep** (preferred — restricts them to MCP only) or **Editor** before they attempt to connect.

#### **Enrichment returning no results after connecting**

If a rep's connection appears active but enrichments return nothing, the connection may have gone out of sync.

**Fix:** Have the rep disconnect Clay from their AI tool's connector settings and reconnect. This refreshes the connection and resolves it in most cases.

### **Functions not working or not appearing**

#### **A Function is enabled for MCP but reps can't find it**

Check the following in order:

1.  Confirm `Enable for MCP` is toggled on in `Edit Table Settings` — not just that the function exists.
2.  Confirm the function has a **name and description** set. These are required for reps to see and invoke it.
3.  Confirm the function has an **enrichment or output column** — toggling MCP and setting inputs alone won't populate data without a column that actually returns results.
4.  Confirm the rep has been added to the workspace with a role of Sales Rep, Editor, or Admin.

#### **Function name conflicts with a built-in Clay tool**

If a custom function is named too similarly to a default Clay MCP tool, the AI tool may invoke the default one instead.

**Fix:** Prompt the AI tool to `List subroutines` (the MCP tool that lists your available Functions), then call the specific custom Function by its exact name. When naming functions, avoid generic terms like "find contacts" or "enrich company" that overlap with Clay's built-in capabilities.

#### **"Failed to update integration settings" when toggling Enable for MCP**

If you see this error, hard-refresh the page. If it persists, recreate the Function under a different name and try again — or contact Clay support.

#### **A Function works fine inside Clay but errors when invoked through Claude or ChatGPT**

The most common cause is a **field-mapping or input mismatch**. When a Function is triggered via MCP, the AI tool passes inputs by matching field names — so if the names don't align, the wrong value gets passed (or nothing gets passed at all).

**Fix:** Use `MCP Caller Email` — the email address of the rep who triggered the Function — as an explicit input wherever the function needs to identify the calling rep (e.g., to look up their Outreach mailbox or Salesforce ownership). Ensure input field names match the output field names from any upstream step (like Find Contacts) so the AI tool maps them correctly.

### **ChatGPT-specific issues**

#### **The Clay widget goes blank or buttons stop working in ChatGPT**

This is a rendering issue on the ChatGPT/OpenAI side rather than in Clay — the same flows work in Claude.

**Fix:** Close the tab, reopen it, and hard-refresh (`Cmd+Shift+R` on Mac, `Ctrl+F5` on Windows). If it persists, clear cache and cookies and restart the browser.

#### **403 Forbidden — "MCP Tool is disabled by this workspace admin"**

Clay does not generate this error message. It comes from ChatGPT's policy layer, meaning your organization's OpenAI admin has not enabled the MCP app or specific actions at the org level.

**Fix:** Your OpenAI workspace admin needs to enable the Clay app and its associated actions in ChatGPT's admin settings. To confirm this is the cause: open Dev Tools → Network → reproduce the failure — you'll see a 403 on `/backend-api/ecosystem/call_mcp`.

#### **A custom Function action isn't available in ChatGPT even after enabling it**

Clay MCP exposes several distinct actions to ChatGPT. In some enterprise accounts, org admins enable the Clay connector but don't enable all of its individual actions — the action named `run_subroutine_no_mapping`, which executes custom Functions, is a common one to miss. This means Functions that work in Claude fail silently in ChatGPT.

**Fix:** Your OpenAI workspace admin needs to review the Clay connector's action list in ChatGPT's admin settings and ensure all actions are enabled, not just the connector itself. This is an OpenAI-side access control, not a Clay configuration issue.

### **Audiences data is accessible in Claude but returns generic results in ChatGPT**

The MCP exposes the same tools and Audiences capabilities to both Claude and ChatGPT — there's no platform-specific restriction on Audiences access. When ChatGPT returns generic results where Claude returns rich Audiences data, the cause is almost always an org-level action restriction on the OpenAI side (same fix as above).

Being more explicit in your prompt also helps — e.g. `Search companies in Clay Audiences` rather than asking generically about an account.

## **FAQ**

### **Setup and access**

**Do MCP users need a full Clay seat?**  
Yes — every rep using MCP must be invited to the Clay workspace. However, you can assign them the **Sales Rep** role, which grants access exclusively through the MCP interface (Claude, ChatGPT, etc.). Reps with this role can't see the Clay UI, edit tables, view API keys, or access workflows directly. It's the lowest-permission profile for MCP access.

**What's the minimum setup to get reps running?**  
Invite reps to your workspace, assign a credit budget, and share the connection instructions for their preferred AI tool. Functions and Audiences are additive — they improve the experience but aren't required to start.

**If we're SSO-enabled, do users still need to be added to the Clay workspace?**  
Yes. If a user isn't explicitly added to your workspace, they won't have access to your Clay data, workflows, or MCP — regardless of SSO. Add the specific users from `Settings → Team`.

**Where are the MCP settings?**  
All MCP controls live under `Settings → MCP users` in the left-hand nav. That's where you invite reps, set credit limits, enable Functions, and monitor usage. The `Enable for MCP` toggle for individual Functions lives inside each Function's `Edit Table Settings`.

**Do reps need their own API keys to run Functions?**  
No. Functions execute server-side within your workspace using credentials stored at the workspace level. Reps don't need their own keys to any of the integrations a Function uses — they just invoke it by name.

### **Credits and cost**

**How many credits does a people or company search use?**  
People and company search is free — it runs a lookup against Clay's database without consuming credits. Credits are only consumed when MCP triggers an actual enrichment (finding an email, phone number, tech stack, etc.) or invokes a Function that enriches.

**Does querying Audiences data cost credits?**  
No. Asking questions about data that's already synced to Audiences consumes **actions, not credits**. Credits are only consumed if the query triggers a live enrichment or Function run.

**When a rep runs a Function through Claude or ChatGPT, does it cost the same as running it directly in Clay?**  
Yes. Credit cost is identical regardless of where the Function is triggered. If a Function uses 15 action credits and 5 data credits inside Clay, it costs the same via MCP.

**How do we prevent reps from burning through credits?**  
Set a default credit limit in `Settings → MCP users` before reps connect — this applies automatically to every new rep. You can also set per-user overrides for heavier or lighter users. The **Sales Rep** role provides an additional layer: reps with this role can only invoke Functions that you've explicitly enabled.

**Can I remove a rep's "connected" status from the MCP users page?**  
Not directly — admins can't revoke an OAuth connection from the MCP page itself. To block access, either remove the rep from the workspace entirely (`Settings → Team`) or set their credit limit to 0, which hard-blocks any further actions without removing them.

### **Product behavior**

**When a rep sends outreach from Claude or ChatGPT, does it go through their sequencer or personal email?**  
It depends on whether a Function has been built for it. To send through a sequencer (e.g. Outreach), your ops team needs to build a Function that includes the sequencer column and exposes it via MCP. Reps can then select which sequence to send to directly from the MCP widget as a Function input — no need to hardcode a specific sequence into the Function. Without a Function configured for this, the AI assistant can send through a connected email provider like Gmail, but it won't touch your sequencer automatically.

**When a rep builds something in Claude or ChatGPT, does it become a Clay table?**  
Only if they click `Open in Clay`. Most one-off operations — finding a contact's email, researching one account — don't create a table by default. Results live in the chat session unless explicitly opened in Clay.

**Can I upload a CSV and run it through a Function via MCP?**  
Not via a direct upload, but in Claude you can share a CSV in the conversation and Claude will call the Function once per row. There's no dedicated bulk-upload mechanism via MCP; for true bulk processing, use Clay directly.

**Can Function inputs map automatically from the Find Contacts output?**  
Yes — when Claude or ChatGPT chains a Find Contacts result into a Function call, it maps fields by name. If your Function's input field names match the output field names from Find Contacts, the AI tool will map them reliably without needing explicit instructions. Mismatched names are the most common cause of empty or incorrect Function inputs.

### **Data and Audiences**

**What does "ask questions about accounts" actually see?**  
It runs a read-only query against your Audiences data layer. It can only see fields you've synced and exposed to Audiences — nothing outside that. It doesn't write back to records, which is why Audiences activity triggered through MCP won't appear in the Audiences Activity UI. Querying Audiences this way uses actions, not credits.

**MCP is returning data that I can't see in Audiences. Where is it coming from?**  
This typically happens with data from converted leads. When a lead is converted to a contact in Salesforce, some of the associated data isn't currently displayed in the Audiences UI — but it is still stored and retrievable via MCP queries. It's not missing; it's just not visible in the Audiences view.

**Does MCP have access to the same data in ChatGPT as in Claude?**  
Yes. The MCP exposes the same tools, Functions, and Audiences access to both platforms. If you're seeing a significant difference in what each returns, the cause is almost always a ChatGPT org-level restriction (see Troubleshooting above), not a difference in MCP capabilities between platforms.

### **Security and data privacy**

**Does Clay's MCP use our data to train AI models?**  
No. Both Anthropic (Claude) and OpenAI (ChatGPT, Codex) exclude commercial and API customer data from model training by default. Clay's MCP operates through their commercial APIs, so your workspace data is not used for training. Clay itself does not store customer table data for other customers and acts as a data processor under standard data protection agreements.

**How do Anthropic and OpenAI handle data from MCP requests?**

-   **Anthropic (Claude):** Commercial and API data is excluded from training. Data is retained briefly for abuse monitoring only and never used for model training. For qualifying organizations, Zero Data Retention (ZDR) means data isn't stored at rest after the API response.
-   **OpenAI (ChatGPT, Codex):** API, Enterprise, and Business data is not used for training by default. Inputs and outputs may be retained for a limited period to provide the service and detect abuse, then deleted unless legally required. ZDR is available for eligible endpoints.

These policies are set by Anthropic and OpenAI and may change. For the most current information, refer to [**Anthropic's privacy policy**](https://www.anthropic.com/legal/privacy) and [**OpenAI's usage policies**](https://openai.com/policies).

**What can the AI tool actually access in our workspace when reps connect via MCP?**  
The AI tool can only call Clay tools and Functions that a workspace admin has explicitly enabled — it cannot browse tables, view raw workspace data, or access anything outside of what enabled Functions return. Specifically:

-   Functions: only those with `Enable for MCP` toggled on
-   Audiences data: only if admin has enabled `Sync user IDs from audiences`
-   Account scope: admins can restrict reps to only accounts they own in Salesforce
-   Credit controls: admins set spending limits per user

### **Scale and limits**

**Is MCP designed for bulk use cases?**  
MCP supports targeted research and moderate-scale operations directly from your AI tool. You can search for contacts across multiple companies at once (e.g. `Find sales leaders at Clay, Ramp, and Figma`), search for companies by criteria like headcount or location, and invoke a Function across a batch of contacts (e.g. `Use my email generator for these 20 contacts`). Results paginate in groups of 20, with a `Load more` option — up to 100 results (5 pages) total. For results beyond 100, or for true bulk processing (thousands of rows, automated workflows), use Clay directly.

**Can I self-host the Clay MCP server to connect other AI tools like Cursor or VS Code?**  
Not currently. Clay MCP connects to Claude, ChatGPT, Microsoft Copilot, and Glean — self-hosting for custom AI agent integrations isn't currently supported.
