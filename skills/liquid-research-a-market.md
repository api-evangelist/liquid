---
name: Research a Liquid market before trading it
description: Use the read scope of the Liquid Co-Invest MCP server to assemble price, funding, positioning, liquidation and news context on a market, and to decide whether there is a catalyst worth acting on.
api: mcp/liquid-mcp.yml
surface: mcp
server: https://coinvest.liquid.trade/mcp
scopes: [read]
generated: '2026-07-19'
method: generated
source: https://www.liquid.trade/coinvest-docs
---

# Research a Liquid market before trading it

Read-only. Requires the `read` scope; never needs `trade`. Every capability named below is a
capability Liquid documents on its Co-Invest page — the server publishes no public tool schema,
so match the user's request to the capability by intent rather than by a hard-coded tool name.

## 1. Resolve the market

Use **market search** to browse or search everything tradeable on Liquid — crypto perps, US and
international stocks, commodities, FX, indices, pre-IPO names (SpaceX, OpenAI, Anthropic) and
prediction contracts. Confirm the exact market before pulling data; the app addresses crypto
perps by bare ticker (`BTC`, `ETH`, `SOL`, `HYPE`) and other markets with an `xyz:` prefix
(`xyz:TSLA`, `xyz:GOLD`, `xyz:EUR`).

## 2. Pull the signal layer

**Market analysis** returns live price, funding rate, open interest and Liquid's proprietary
positioning: whale exposure by size tier, behavioral cohorts and liquidation clusters.

Coverage caveat — state it plainly when it applies: the proprietary positioning analytics cover
Liquid's **core crypto universe**. For stocks, commodities, FX and indices you have price action,
market structure and news only. Do not present crypto-grade positioning confidence on an equity.

## 3. Add context

- **News** — recent headlines with sources, cross-referenced against positioning to find catalysts.
- **Leaderboard & positioning pulse** — what top Liquid traders hold (rank, PnL, directional bias,
  largest positions) plus the day's biggest positioning themes.
- **Prediction markets** — event contracts with YES/NO outcomes and live probabilities, when the
  question is event-shaped rather than price-shaped.

## 4. Render, don't just describe

Ask for the inline visuals when they carry the argument: **price charts** (OHLCV at a chosen
interval), **order books** (bid/ask depth, for spot-checking liquidity before sizing), and the
**market overview** dashboard (all markets by price, funding, open interest, volume).

## 5. Conclude honestly

A usable conclusion has a direction, a size and a **named catalyst** with a link to its source —
an earnings print, a central-bank decision, ETF flow data, an on-chain print. If the catalyst is
weak, say so and recommend sitting on your hands. Liquid's own framing: the assistant should tell
you when nothing is worth trading.

Nothing in this skill places an order. Hand off to
`liquid-place-a-confirmed-trade.md` only after the user asks to act.

## Related

- `mcp/liquid-mcp.yml`
- `conventions/liquid-conventions.yml`
