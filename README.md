# Liquid

Liquid (**liquid.trade**, formerly tryliquid.xyz) is a perpetual-futures trading platform and perp-DEX
aggregator. Traders go long or short on 500+ markets — crypto perps, US and international equities,
commodities, FX, indices, pre-IPO names like OpenAI, Anthropic and SpaceX, and event/prediction contracts
— 24/7 with up to 50x multipliers, routed through venues including Hyperliquid, with funds held in the
user's own non-custodial wallet.

Liquid raised an **$18M Series Seed** led by Neo and Left Lane Capital in April 2026, following a $7.6M
seed led by Paradigm.

## Programmable surface

Liquid publishes **no public REST API and no OpenAPI**. Its entire programmable surface is **Co-Invest**,
a published remote **MCP server** at `https://coinvest.liquid.trade/mcp` that puts market research,
portfolio state and confirmed trade execution inside Claude, ChatGPT, Cursor, iMessage and any
MCP-compatible client.

- OAuth 2.1 — authorization code + PKCE (S256) + dynamic client registration, with RFC 8414 and RFC 9728
  discovery documents live on the MCP host.
- Two scopes: `read` and `trade`. The grant can never withdraw funds or change account settings.
- Every state-changing action renders a confirmation card; nothing executes without a human tap.
- Paper mode: a simulated $10,000 balance against live market data.

## Artifacts

| Dir | Artifact |
|---|---|
| `mcp/` | Co-Invest MCP server manifest (searched) |
| `well-known/` | RFC 9728 + RFC 8414 metadata, saved verbatim |
| `llms/` | `llms.txt` from docs.liquid.trade, saved verbatim |
| `authentication/` | OAuth 2.1 profile |
| `scopes/` | `read` / `trade` scope reference |
| `conventions/` | MCP transport, confirmation model, limits, error shape |
| `conformance/` | Standards conformance + Zellic audit record |
| `sandbox/` | Paper-trading mode |
| `changelog/` | Daily dated changelog |
| `lifecycle/` | Versioning, cadence, support; no status page or deprecation policy published |
| `packages/` | Registry sweep — no first-party SDK exists |
| `security/` | Domain security probe (TLS/HSTS/DNSSEC/CAA/SPF/DMARC) |
| `skills/` | Four Agent Skills for the Co-Invest surface |

Backed by: paradigm, techstars — https://www.liquid.trade
