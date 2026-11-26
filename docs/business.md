# NXTL for Business on the same MCP server

There is one NXTL MCP server. A business does not connect to a second server.

```
https://nxtlsim.com/wp-json/nxtl-ai/v1/mcp
```

A team member adds that address in Claude, ChatGPT or another MCP app and signs in with their NXTL Business account. The tools they get depend on their company role. NXTL for Business can switch assistant access and changes on or off for the company.

The [MCP guide](https://nxtlsim.com/mcp/) publishes that address once, for every account. Its “Run your team’s eSIMs” card, fetched on 26 November 2026, says:

> Team members see company eSIMs, usage and billing in their own assistant, within their role. Changes run only after you confirm.

[For Business](https://nxtlsim.com/for-business/) points “How it works” at that card and says assistants are Claude or ChatGPT, within each member’s role.

The REST API at `https://nxtlsim.com/api/v1` is a different interface. Its API keys and scopes are not MCP permissions.

## What the assistant can do

On this server, within the member’s role, the MCP guide says the assistant can see company eSIMs, usage and billing. Changes run only after that person confirms.

The [Partner API reference](https://nxtlsim.com/nxtl-api-reference/) still names these assistant tools, in this order:

1. Read first with `nxtl_business_overview`, `nxtl_business_list_esims`, `nxtl_business_rates` and `nxtl_business_alert_rules`.
2. Prepare a change with `nxtl_business_preview_action`.
3. Read that summary to the person.
4. Run it with `nxtl_business_confirm_action` and `customer_confirmed: true`.

Those tools belong to this server. Which of them a person receives depends on their company role. The reference says assistants read with the rights of the person who connects them, and that changes from assistants work only when they are switched on for the company. Money, terminate and rule changes are done on the NXTL page the tool links to.

The reference does not publish a field list for those tools, and it does not publish MCP scope names.

## The assistant never pays

- By default the assistant can only read. It cannot charge your card. Purchases open in NXTL for you to review and pay. ([MCP guide](https://nxtlsim.com/mcp/))
- The assistant cannot charge a saved card or debit the balance. A prepared top-up or a new eSIM is paid on NXTL, and a new eSIM is ready only after NXTL confirms payment and fulfilment. ([MCP guide](https://nxtlsim.com/mcp/))
- Money, terminate and rule changes are done on the NXTL page the tool links to. ([Partner API reference](https://nxtlsim.com/nxtl-api-reference/))
- Purchases are always reviewed in NXTL. ([AI assistants and research](https://nxtlsim.com/ai-info/))

## How to connect

Use the same address and the same sign-in steps as any other NXTL account. Sign in with the NXTL Business account whose role should apply. The password stays with NXTL. Never put a password or token in a config file. Tick what the assistant may see, then approve. Disconnect under More, Connected assistants, or in the NXTL app. Access stops at once.

**Claude** (web, desktop and phone), as published on the MCP guide:

1. In Claude, open Customize, then Connectors.
2. Choose Add, then Add custom connector. Paste `https://nxtlsim.com/wp-json/nxtl-ai/v1/mcp` and click Add.
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

## How a business sign-in differs from a personal one

Both use `https://nxtlsim.com/wp-json/nxtl-ai/v1/mcp`.

| | Personal account, as the MCP guide describes it | NXTL Business, on that same server |
| --- | --- | --- |
| Sign-in | The NXTL account you connect | The team member’s NXTL Business account |
| What the assistant can see | Balance, membership and permitted account information; destination rates and data estimates; permitted line details and setup guidance | Company eSIMs, usage and billing, within that member’s role. The `nxtl_business_*` tools above are the ones the API reference names; the person receives the tools their role allows |
| Changes | A top-up or new eSIM is prepared, then paid by the customer on NXTL | Changes run only after you confirm, and only when NXTL for Business has assistant changes switched on. Money, terminate and rule changes finish on the NXTL page |
| Who can turn it off | The person disconnects the assistant | The person can disconnect, and NXTL for Business can switch assistant access and changes off for the company |

Eligible free and Premium accounts can connect. Premium is not required just to connect. This server is not nxtlAI, the assistant built into the NXTL site and app.

## Registry

`server.json` keeps one entry, `io.github.nxtlsim/nxtl-esim`, version 1.0.3, with one remote: the address above. The registry description is one sentence, within the schema limit of 100 characters:

> NXTL eSIM rates, balance and estimates in Claude, ChatGPT or any MCP app, for travellers and teams.

## Sources

Fetched on 26 November 2026, except the connection model noted as confirmed by NXTL.

| Claim | Page |
| --- | --- |
| One published remote address, `https://nxtlsim.com/wp-json/nxtl-ai/v1/mcp`. Sign in on NXTL. The password stays with NXTL. Never put a password or token in a config file. By default the assistant can only read. It cannot charge your card. Purchases open in NXTL for review and payment. | [https://nxtlsim.com/mcp/](https://nxtlsim.com/mcp/) |
| ChatGPT: add a custom MCP server, choose OAuth, sign in, tick what it may see. A paid plan with developer mode is required, on the web. | [https://nxtlsim.com/mcp/](https://nxtlsim.com/mcp/) |
| Claude: Customize, Connectors, add a custom connector, then Connect and sign in. On a Team or Enterprise plan, an Owner adds the connector for the organisation first. Claude Code uses `claude mcp add` on the same address. Cursor, VS Code and Windsurf are documented on the same page. | [https://nxtlsim.com/mcp/](https://nxtlsim.com/mcp/) |
| “Run your team’s eSIMs”: “Team members see company eSIMs, usage and billing in their own assistant, within their role. Changes run only after you confirm.” | [https://nxtlsim.com/mcp/](https://nxtlsim.com/mcp/) (same text in [https://nxtlsim.com/mcp.md](https://nxtlsim.com/mcp.md)) |
| The assistant cannot charge a saved card or debit the balance. A new eSIM is ready only after NXTL confirms payment and fulfilment. Disconnect under More, Connected assistants, or in the NXTL app. | [https://nxtlsim.com/mcp/](https://nxtlsim.com/mcp/) |
| Eligible free and Premium accounts can connect. Premium is not required just to connect. | [https://nxtlsim.com/mcp/](https://nxtlsim.com/mcp/) |
| AI assistants: Claude or ChatGPT, within each member’s role. “How it works” links to `https://nxtlsim.com/mcp/#capabilities`. | [https://nxtlsim.com/for-business/](https://nxtlsim.com/for-business/) |
| Read tools `nxtl_business_overview`, `nxtl_business_list_esims`, `nxtl_business_rates`, `nxtl_business_alert_rules`; then `nxtl_business_preview_action`; then `nxtl_business_confirm_action` with `customer_confirmed: true`. Assistants read with the rights of the person who connects them. Money, terminate and rule changes are done on the NXTL page the tool links to. Changes from assistants work only when they are switched on for the company. | [https://nxtlsim.com/nxtl-api-reference/](https://nxtlsim.com/nxtl-api-reference/) (developer tips; the tool sequence is also in [nxtl-api-reference.md](https://nxtlsim.com/nxtl-api-reference.md)) |
| Purchases are always reviewed in NXTL. The MCP link on this page goes to the MCP guide. | [https://nxtlsim.com/ai-info/](https://nxtlsim.com/ai-info/) |
| A team member uses this same URL and signs in with their NXTL Business account. The tools they get depend on their company role. NXTL for Business can switch assistant access and changes on or off for the company. There is no second MCP server. | Confirmed by NXTL on 26 November 2026. The published card quoted above is the business text on [https://nxtlsim.com/mcp/](https://nxtlsim.com/mcp/). |
