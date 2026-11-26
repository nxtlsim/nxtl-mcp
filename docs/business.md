# NXTL for Business and MCP

This note records only what NXTL publishes about MCP access for a business account. It does not add a second registry server. The Partner API reference names a NXTL Business MCP server, and it does not publish a remote URL for it.

The REST API at `https://nxtlsim.com/api/v1` is a different interface. Its API keys and scopes are not MCP permissions.

## What a business assistant can do

Two public descriptions cover business use. They do not use the same words, and this page keeps them apart.

On the [MCP guide](https://nxtlsim.com/mcp/), under NXTL for Business:

> Team members see company eSIMs, usage and billing in their own assistant, within their role. Changes run only after you confirm.

The [For Business](https://nxtlsim.com/for-business/) page points “How it works” at that same section and says assistants are Claude or ChatGPT, within each member’s role.

The [Partner API reference](https://nxtlsim.com/nxtl-api-reference/) names a NXTL Business MCP server, opened from the business dashboard under Assistants. Assistants read with the rights of the person who connects them. Its published developer tip names these tools, in this order:

1. Read first with `nxtl_business_overview`, `nxtl_business_list_esims`, `nxtl_business_rates` and `nxtl_business_alert_rules`.
2. Prepare a change with `nxtl_business_preview_action`.
3. Read that summary to the person.
4. Run it with `nxtl_business_confirm_action` and `customer_confirmed: true`.

Money, terminate and rule changes are done on the NXTL page the tool links to. Changes from assistants work only when they are switched on for the company.

The reference does not publish a field list for those tools, and it does not publish MCP scope names. Do not treat REST scopes such as `balance:read` as MCP scopes.

The [guide for AI assistants](https://nxtlsim.com/nxtl-api-reference/nxtl-api-guide-for-ai.md) says the same dashboard connection, and it says to use the Business MCP server’s tools for that account’s live data. Writing code against the REST API is the job of that guide, not of the MCP tools.

## The assistant never pays

Public MCP pages say the customer pays on NXTL:

- By default the assistant can only read. It cannot charge your card. Purchases open in NXTL for you to review and pay. ([MCP guide](https://nxtlsim.com/mcp/))
- The assistant cannot charge a saved card or debit your balance. A prepared top-up or a new eSIM is paid on NXTL, and a new eSIM is ready only after NXTL confirms payment and fulfilment. ([MCP guide](https://nxtlsim.com/mcp/))
- Money, terminate and rule changes are done on the NXTL page the Business MCP tool links to. ([Partner API reference](https://nxtlsim.com/nxtl-api-reference/))
- Purchases are always reviewed in NXTL. ([AI assistants and research](https://nxtlsim.com/ai-info/))

## How to connect

### The published remote address

For Business sends “How it works” to the MCP guide. That guide publishes one remote address:

`https://nxtlsim.com/wp-json/nxtl-ai/v1/mcp`

Sign in on the NXTL page with the account whose access should apply. The password stays with NXTL. Never put a password or token in a config file. Tick what the assistant may see, then approve. Disconnect under More, Connected assistants, or in the NXTL app. Access stops at once.

None of the pages in [Sources](#sources) publishes a second business URL, so this repository does not register one.

**Claude** (web, desktop and phone), as published:

1. In Claude, open Customize, then Connectors.
2. Choose Add, then Add custom connector. Paste the address and click Add.
3. Click Connect, sign in to NXTL and approve.

On a Team or Enterprise plan, an Owner adds the connector for the organisation first.

**ChatGPT** (on the web), as published:

1. Click + and choose Add custom MCP server.
2. Name it NXTL eSIM, paste the address as the Server URL, choose OAuth, then create it.
3. Sign in to NXTL, tick what ChatGPT may see and approve.

Adding NXTL to ChatGPT needs a paid ChatGPT plan with developer mode.

**Claude Code**, as published:

```bash
claude mcp add --transport http nxtl https://nxtlsim.com/wp-json/nxtl-ai/v1/mcp
```

Then run `/mcp`, choose nxtl, and sign in to NXTL in the browser.

**Other MCP apps.** Any app that supports remote MCP with sign-in can use the same address (HTTP or Streamable HTTP). The MCP guide includes config examples for Cursor, VS Code with GitHub Copilot and Windsurf. When the app opens the browser, sign in to NXTL and approve.

### The Business MCP server in the dashboard

The Partner API reference says to connect AI assistants with the NXTL Business MCP server from the business dashboard under Assistants. It does not publish the remote URL, the Claude steps, or the ChatGPT steps for that server. Use the dashboard entry the reference names. The tool sequence above is the published way those tools are meant to be used.

## How this differs from the consumer server

| | Consumer account, as the MCP guide describes it | Business, as the public pages describe it |
| --- | --- | --- |
| Where it is documented | [MCP guide](https://nxtlsim.com/mcp/) | The same guide’s Business card, plus the [Partner API reference](https://nxtlsim.com/nxtl-api-reference/) for the named Business MCP server |
| Published remote URL | `https://nxtlsim.com/wp-json/nxtl-ai/v1/mcp` | No separate URL is published. For Business links “How it works” to the MCP guide |
| What the assistant can see | Balance, membership and permitted account information; destination rates and data estimates; permitted line details and setup guidance | On the MCP guide: company eSIMs, usage and billing, within that member’s role. On the API reference: the `nxtl_business_*` tools, read with the rights of the person who connects |
| Changes | A top-up or new eSIM is prepared, then paid by the customer on NXTL | Changes run only after you confirm. The API reference adds preview, then `nxtl_business_confirm_action` with `customer_confirmed: true`. Money, terminate and rule changes finish on the NXTL page, and only when assistant changes are switched on for the company |
| Who can connect | Eligible free and Premium accounts. Premium is not required just to connect | The For Business page names Claude or ChatGPT within each member’s role. The API reference limits reads to the connecting person’s rights |

Both stay separate from nxtlAI, the assistant built into the NXTL site and app.

## What is not in the registry

`server.json` in this repository registers `io.github.nxtlsim/nxtl-esim` and the one published remote URL. A second remote, or a server such as `io.github.nxtlsim/nxtl-business`, needs a public `https` URL. None is published, so the registry metadata is unchanged.

## Sources

Each claim above comes from these pages, fetched on 26 November 2026.

| Claim | Page |
| --- | --- |
| One remote address, `https://nxtlsim.com/wp-json/nxtl-ai/v1/mcp`. Sign in on NXTL. The password stays with NXTL. Never put a password or token in a config file. By default the assistant can only read. It cannot charge your card. Purchases open in NXTL for review and payment. | [https://nxtlsim.com/mcp/](https://nxtlsim.com/mcp/) |
| ChatGPT: add a custom MCP server, choose OAuth, sign in, tick what it may see. A paid plan with developer mode is required, on the web. | [https://nxtlsim.com/mcp/](https://nxtlsim.com/mcp/) |
| Claude: Customize, Connectors, add a custom connector, then Connect and sign in. On a Team or Enterprise plan, an Owner adds the connector for the organisation first. Claude Code uses the `claude mcp add` command on the same address. Cursor, VS Code and Windsurf are documented on the same page. | [https://nxtlsim.com/mcp/](https://nxtlsim.com/mcp/) |
| Team members see company eSIMs, usage and billing in their own assistant, within their role. Changes run only after you confirm. | [https://nxtlsim.com/mcp/](https://nxtlsim.com/mcp/) (also the markdown copy [https://nxtlsim.com/mcp.md](https://nxtlsim.com/mcp.md)) |
| The assistant cannot charge a saved card or debit the balance. A new eSIM is ready only after NXTL confirms payment and fulfilment. Disconnect under More, Connected assistants, or in the NXTL app. | [https://nxtlsim.com/mcp/](https://nxtlsim.com/mcp/) |
| Eligible free and Premium accounts can connect. Premium is not required just to connect. | [https://nxtlsim.com/mcp/](https://nxtlsim.com/mcp/) |
| AI assistants: Claude or ChatGPT, within each member’s role. “How it works” links to `https://nxtlsim.com/mcp/#capabilities`. | [https://nxtlsim.com/for-business/](https://nxtlsim.com/for-business/) |
| Connect AI assistants with the NXTL Business MCP server (dashboard: Assistants). They read with the rights of the person who connects them. | [https://nxtlsim.com/nxtl-api-reference/](https://nxtlsim.com/nxtl-api-reference/) and [the AI guide](https://nxtlsim.com/nxtl-api-reference/nxtl-api-guide-for-ai.md) |
| Read tools `nxtl_business_overview`, `nxtl_business_list_esims`, `nxtl_business_rates`, `nxtl_business_alert_rules`; then `nxtl_business_preview_action`; then `nxtl_business_confirm_action` with `customer_confirmed: true`. Money, terminate and rule changes are done on the NXTL page the tool links to. Changes from assistants work only when they are switched on for the company. | [https://nxtlsim.com/nxtl-api-reference/](https://nxtlsim.com/nxtl-api-reference/) (developer tips; same text in [nxtl-api-reference.md](https://nxtlsim.com/nxtl-api-reference.md)) |
| If an assistant is connected through the NXTL Business MCP server, use its tools for that account’s live data, and the API guide to write code against the API. | [AI guide](https://nxtlsim.com/nxtl-api-reference/nxtl-api-guide-for-ai.md) |
| Purchases are always reviewed in NXTL. The MCP link on this page goes to the MCP guide. | [https://nxtlsim.com/ai-info/](https://nxtlsim.com/ai-info/) |
| The eSIM API overview links to the MCP guide in the site footer and does not publish a business MCP URL or tool list. | [https://nxtlsim.com/esim-api/](https://nxtlsim.com/esim-api/) |
| The OpenAPI document for the REST API does not mention MCP. | [nxtl-v1-openapi.json](https://nxtlsim.com/wp-content/plugins/nxtl-data-esim-v2/docs/nxtl-v1-openapi.json) |
