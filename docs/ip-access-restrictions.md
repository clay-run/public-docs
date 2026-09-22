---
title: IP access restrictions
description: Configure IP allowlists to restrict which IP addresses can access your Clay workspace via the web app or API, available on Enterprise plans.
last_synced: 2026-09-22T20:17:22.998Z
---

# IP access restrictions

Limit which IP addresses can reach your workspace from the web app and the API, and allowlist the AI agents and integrations that call Clay.

IP access restrictions let workspace admins choose which IP addresses can reach a Clay workspace, such as your corporate network or VPN. Browser access and API access are restricted separately, so you can lock down one or both.

**Note:** IP access restrictions are available on the Enterprise plan. Only workspace admins can view and change them.

IP access restrictions cover two kinds of access:

-   **Web app:** Anyone signed in to Clay in a browser, including opening tables and workbooks.
-   **API:** Requests made with a Clay API key or an authorized connection, including MCP connections from AI agents and the Clay CLI, Clay's command-line tool.

When a restriction is on, requests from an address that isn't on an allowlist for that access type are blocked. People using the web app see an `Access restricted` page with the option to switch to another workspace they belong to. API requests are rejected with a 403 error and the message `Your IP address is not on the allowlist for this workspace.`

## Setting up IP access restrictions

1.  Go to `Settings` → `Workspace` and scroll to the `Security` section.
2.  In the `IP access restrictions` card, click `Add allowlist`.
3.  Enter an `Allowlist name`, such as `NYC HQ` or `VPN range`.
4.  Under `IP addresses`, enter one IPv4 address, IPv6 address, or CIDR range per line (for example, `198.51.100.0/24`).
    -   Click `Add it` next to `You're connecting from…` to add the address you're using right now.
    -   Each allowlist holds up to 50 addresses or ranges.
5.  Under `Applies to`, choose `Web app` or `API`, then click `Add allowlist`.
    -   An allowlist covers one access type. To cover both, create one allowlist for each.
6.  Turn on the switch next to `Web app` or `API`, then click `Turn on` to confirm.
    -   The confirmation shows how many addresses access will be limited to. The status changes from `Unrestricted` to `Restricted`.

**Note:** Changes can take up to 10 minutes to apply to all requests. Give yourself that buffer before testing from a new network.

## Allowlisting AI agents and integrations

API restrictions apply to every tool that calls Clay on your behalf, so add their addresses before you turn on `API` restrictions.

-   **AI agents connected through MCP:** Hosted AI apps call Clay from the provider's servers, not from your browser. Add the provider's published outbound addresses: [Anthropic (Claude)](https://platform.claude.com/docs/en/api/ip-addresses) and [OpenAI (ChatGPT)](https://developers.openai.com/api/docs/guides/ip-addresses). For other AI providers, ask them for their outbound IP ranges.
-   **The Clay CLI:** The CLI calls Clay from the network you're on, so your office or VPN ranges on an `API` allowlist cover it.
-   **Automations and scripts:** Workflow automation tools, data pipelines, and custom scripts that use a Clay API key need their outbound IP addresses added to an `API` allowlist.

## Managing IP access restrictions

-   **Edit an allowlist:** Click the pencil icon next to the allowlist to change its name, addresses, or access type, then click `Save changes`.
-   **Delete an allowlist:** Click the trash icon, then click `Delete`. If you delete the last allowlist for an access type, restrictions for that access type turn off.
-   **Turn off restrictions:** Turn off the switch next to `Web app` or `API`. Your allowlists are kept, so you can turn restrictions back on later.

## FAQs

### Can I set different IP restrictions for different users?

No. IP access restrictions apply to everyone in the workspace. Each workspace has its own settings, so restrictions on one workspace don't affect your other workspaces.

### Can I lock myself out while setting this up?

Clay won't save a `Web app` change that would block the address you're connecting from, and shows a message explaining why. Add your current address with `Add it`, or connect to your VPN, and try again.

If your address changes later, for example when you leave your VPN, you'll see the `Access restricted` page. Reconnect to an allowed network, or ask another workspace admin on an allowed network to update the allowlist.

### Can Clay support still help if we're blocked?

Yes. Clay support sessions aren't affected by IP access restrictions, so support can still access your workspace to help, including if you need restrictions turned off. Contact your Clay account team or Clay support.

### What if I need more than 50 addresses?

Create another allowlist for the same access type. Access is allowed from any address on any of that access type's allowlists. A CIDR range such as `203.0.113.0/24` also counts as a single entry.
