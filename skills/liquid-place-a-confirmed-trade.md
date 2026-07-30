---
name: Propose and place a confirmed trade on Liquid
description: Use the trade scope of the Liquid Co-Invest MCP server to size a position against the live account, render a confirmation card, and manage the position afterwards — without ever bypassing the human Confirm tap.
api: mcp/liquid-mcp.yml
surface: mcp
server: https://coinvest.liquid.trade/mcp
scopes: [read, trade]
human_in_the_loop: required
generated: '2026-07-19'
method: generated
source: https://www.liquid.trade/coinvest-docs
---

# Propose and place a confirmed trade on Liquid

Requires `read` + `trade`. **Every** state-changing action here renders a confirmation card that
the human must tap. There is no unattended execution path and you must not attempt to construct
one.

## 0. Dry-run first when the user is new

If the user has never traded through Co-Invest, offer paper mode first — see
`liquid-paper-trade-dry-run.md`. It runs a simulated $10,000 balance against live market data.

## 1. Read the account before you size anything

Pull **portfolio & positions** (balance, equity, margin, every open position with live PnL) and
**open orders** (resting limits plus TP/SL triggers, with the IDs needed to modify or cancel).
Size the proposal against the live balance, not against a number the user guessed.

Hard constraints, documented by Liquid:

- Minimum **$15 of collateral** per order.
- Minimum position size scales with the multiplier — $15 at 5x is a $75 position, $15 at 10x is
  a $150 position.
- Up to 50x multipliers; crypto perpetuals up to 40x; the maximum varies by market and asset class.

## 2. Build the proposal

**Place trades** supports long or short, market or limit, optional leverage, and an attached
take-profit / stop-loss — as a single trade or a basket of several at once. For a whole book, use
**portfolio planning**: a multi-position allocation plan driven by the user's risk tolerance, time
horizon and preferred asset classes, proposed as one batch.

Attach a reason. Liquid's confirmation card shows symbol, direction, size, leverage, TP/SL and a
short note on why — write that note as something the user can actually evaluate, anchored to the
catalyst from `liquid-research-a-market.md`.

## 3. Let the card do the committing

The user taps **Confirm** to send or **Cancel** to discard. A batch of five proposals is still one
explicit tap. Do not narrate the trade as done before the tap lands, and do not re-propose an
identical order because you did not see a response — Liquid documents no idempotency key for this
surface, so a blind retry is a second real order.

Server-side sanity checks will reject bad proposals rather than place them; the documented example
is a **stop-loss at or past the liquidation price**. Treat a rejection as a signal to re-derive the
level, not to resubmit.

## 4. Manage the position

Same confirmation rule applies to all of these:

- **Manage positions** — add, change or remove TP/SL on an open position, adjust leverage, or
  close positions (one, several, or all at once).
- **Manage orders** — cancel resting orders by ID (take the ID from open orders, never guess it).
- **Prediction orders** — take a YES/NO side on an event contract, and close it later.

## 5. Failure modes

- **"Trading not enabled"** — the account is unfunded or the trading agent key is unapproved.
  Route the user to a deposit or a browser re-authorization; do not retry the order.
- Funding an account: **deposits & conversions** generates a deposit address or converts between
  balances. The connection can never withdraw or transfer funds out — if a user asks for that,
  send them to the Liquid app.

## Fees

5 bps (0.05%) uniform taker fee on perps, tiered on rolling 14-day weighted volume; no additional
Liquid fee on spot beyond the routing venue's. Co-Invest itself adds no subscription, AI surcharge
or spread markup. Full schedule: https://docs.tryliquid.xyz/trading/fees

## Related

- `scopes/liquid-scopes.yml` — the `trade` scope boundary
- `conventions/liquid-conventions.yml` — confirmation model, limits, no idempotency contract
- `sandbox/liquid-sandbox.yml` — paper mode
