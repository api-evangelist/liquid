---
name: Dry-run the Liquid workflow in paper mode
description: Switch a Liquid Co-Invest account into simulated paper trading against live market data, rehearse the confirmation flow safely, then switch back to live.
api: mcp/liquid-mcp.yml
surface: mcp
server: https://coinvest.liquid.trade/mcp
scopes: [read, trade]
generated: '2026-07-19'
method: generated
source: https://www.liquid.trade/coinvest-docs
---

# Dry-run the Liquid workflow in paper mode

Liquid has no separate sandbox host, no test API keys and no magic test symbols. The sandbox is
**paper mode**: account state you toggle in conversation through the same OAuth-protected
Co-Invest MCP endpoint.

## What paper mode is

- A simulated balance of **$10,000** running against **live market data** — real prices, fake money.
- Enabled by asking the assistant to switch to paper mode; disabled with "go back to live trading".
- The paper account can be **reset** back to its starting balance on request.
- Paper status can be asked for at any time.
- The setting **persists between conversations** until it is changed.
- While it is on, the assistant explicitly labels everything as simulated.

## When to use it

- The user has never placed a trade through an MCP client and wants to see what the confirmation
  card actually does before real money is involved.
- You want to rehearse a multi-position basket from **portfolio planning** end to end.
- You are validating that TP/SL, leverage changes and closes behave the way the user expects.

## Rules while paper mode is on

1. **Say which account you are on, every time.** The single worst failure here is a user believing
   a live order was simulated, or vice versa. Check and state the mode before any proposal.
2. The same constraints still apply — $15 minimum collateral, minimum position scaling with the
   multiplier, and rejection of a stop-loss at or past the liquidation price.
3. The confirmation card still gates everything. Paper mode removes the money, not the tap.

## Switching back

Say "go back to live trading". Re-confirm the mode has flipped and re-read the real portfolio
before proposing anything, because the balances you were sizing against were simulated.

## Related

- `sandbox/liquid-sandbox.yml`
- `liquid-place-a-confirmed-trade.md`
