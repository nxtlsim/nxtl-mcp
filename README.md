# NXTL eSIM MCP

This repository holds the official [MCP Registry](https://registry.modelcontextprotocol.io/) metadata for the NXTL eSIM remote MCP server, plus a short connection guide.

The server itself is hosted by NXTL eSIM at [https://nxtlsim.com/wp-json/nxtl-ai/v1/mcp](https://nxtlsim.com/wp-json/nxtl-ai/v1/mcp) (Streamable HTTP). This repository does not contain the server implementation.

Full documentation: [https://nxtlsim.com/mcp/](https://nxtlsim.com/mcp/)

## What it does

NXTL MCP connects Claude, ChatGPT or another remote-MCP app, with sign-in (OAuth), to selected NXTL eSIM tools. It is not the same as nxtlAI, the built-in assistant on the NXTL site and app.

It is read-only by default. A connected assistant can check balance, membership and permitted account information; compare destination rates and estimate data needs; and request permitted eSIM details and setup guidance.

If you ask it to prepare a top-up or a new eSIM, payment opens on NXTL for the customer to review and complete. Purchases are always reviewed in NXTL.

Free and Premium accounts can connect. Premium is not required just to connect.

## How to connect

1. Add the remote MCP server URL: `https://nxtlsim.com/wp-json/nxtl-ai/v1/mcp`
2. Sign in to NXTL in the browser. The password stays with NXTL.
3. Tick what the assistant may see, and approve.

The server is documented for Claude (web, desktop and phone), ChatGPT (a paid plan with developer mode), Claude Code, Cursor, VS Code with GitHub Copilot, Windsurf, and any app that supports remote MCP with sign-in.

Claude Code, quoted from the docs:

```bash
claude mcp add --transport http nxtl https://nxtlsim.com/wp-json/nxtl-ai/v1/mcp
```

Then run `/mcp`, choose nxtl, and sign in in the browser.

You can disconnect at any time under More, Connected assistants, or in the NXTL app. Access stops at once.

## Registry metadata

- Registry name: `io.github.nxtlsim/nxtl-esim`
- Website: [https://nxtlsim.com/mcp/](https://nxtlsim.com/mcp/)
- Metadata file: [`server.json`](./server.json)
- Publishing: GitHub Actions with OIDC (see [`.github/workflows/publish-mcp.yml`](./.github/workflows/publish-mcp.yml)). No registry token is stored in the repository.

## Related

- [awesome-esim](https://github.com/nxtlsim/awesome-esim) - Curated list of eSIM tools, specs, APIs, guides and resources, including this MCP server.

## Licence

The files in this repository are released under the MIT Licence. The NXTL MCP server and the NXTL eSIM service remain NXTL products; see [nxtlsim.com](https://nxtlsim.com).
