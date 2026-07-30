---
name: Connect the Liquid Co-Invest MCP server
description: Connect an MCP client to Liquid's Co-Invest server, complete the OAuth 2.1 sign-in, and verify the account is ready to trade.
api: mcp/liquid-mcp.yml
surface: mcp
server: https://coinvest.liquid.trade/mcp
scopes: [read, trade]
generated: '2026-07-19'
method: generated
source: https://www.liquid.trade/coinvest-docs
---

# Connect the Liquid Co-Invest MCP server

Liquid publishes no REST API. The only programmable surface is **Co-Invest**, a remote MCP
server. Everything below is grounded in Liquid's own Co-Invest documentation and in the live
OAuth metadata on `coinvest.liquid.trade` — do not invent tool names, endpoints or parameters.

## 1. Pick the right server address

Both forms are documented as valid; use whichever the client expects.

- `https://coinvest.liquid.trade`
- `https://coinvest.liquid.trade/mcp`

| Client | How to connect |
|---|---|
| ChatGPT | Open the Co-Invest app in the app directory, hit Connect, approve access. |
| Claude | Settings → Connectors → **Add custom connector**, name it `Co-Invest`, paste `https://coinvest.liquid.trade`. |
| Claude Desktop / Claude Code (stdio) | Bridge with `npx mcp-remote https://coinvest.liquid.trade/mcp` in `claude_desktop_config.json`. |
| Cursor and other remote-MCP clients | Add `https://coinvest.liquid.trade/mcp` to `.cursor/mcp.json`. |
| iMessage | https://www.liquid.trade/coinvest-imessage |

Claude Desktop config:

```json
{
  "mcpServers": {
    "liquid-co-invest": {
      "command": "npx",
      "args": ["mcp-remote", "https://coinvest.liquid.trade/mcp"]
    }
  }
}
```

## 2. Understand what the OAuth grant covers

An unauthenticated call returns `401` with
`WWW-Authenticate: Bearer realm="mcp", resource_metadata="https://coinvest.liquid.trade/.well-known/oauth-protected-resource"`.
Follow that pointer; it names the authorization server (`https://coinvest.liquid.trade`), which
publishes RFC 8414 metadata with `authorization_code` + `refresh_token`, PKCE `S256`, and a
dynamic client registration endpoint.

Two scopes, and only two:

- `read` — market data, portfolio and account state.
- `trade` — placing and managing orders, always behind an explicit human confirmation.

The grant can **never** withdraw or transfer funds, change account settings, or send an order
without a Confirm tap. Funds stay in the user's own non-custodial wallet.

## 3. Verify readiness before proposing anything

Ask the server for account state (`read` scope). If the account is new, Liquid reports
**"Trading not enabled"** on the first trade attempt. There are exactly two documented causes:

1. the account is not funded yet, or
2. the trading agent key has not been approved.

Do not retry the order. Surface which of the two it is and route the user to a deposit or a
browser re-authorization.

## 4. Troubleshooting

- **Connector will not connect** — confirm the URL is exactly `https://coinvest.liquid.trade`,
  remove and re-add the connector if a failed attempt was cached, then re-run sign-in.
- **Unverified-app warning on the consent screen** — expected for MCP clients Liquid has not
  verified. Tell the user to read what the screen says they are approving; if anything looks
  wrong, connect from Claude or ChatGPT instead.
- Support is Discord (`discord.gg/liquidtrading`, the primary channel), Telegram, or
  https://www.liquid.trade/support.

## Related

- `authentication/liquid-authentication.yml`
- `scopes/liquid-scopes.yml`
- `well-known/liquid-well-known.yml`
