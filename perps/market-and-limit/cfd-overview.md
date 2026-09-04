---
metaLinks:
  alternates:
    - https://app.gitbook.com/s/KiKbOTrmqLWnXHD7ZyeJ/jiao-yi/cfd-gai-lan
---

# CFD overview

YesFi offers **USD-settled perps**. You can think of them as long-running CFD-style positions with no spot delivery. Your margin, PnL, and settlement stay anchored in **USD**.

The core experience is simple:

* express intent in **natural language**
* manage each trade with **isolated margin**
* optionally add insurance products where available

For the product model, see [**What is YesFi**](../../readme/what-is-yesfi.md).

| Feature                    | What it means                                                                                                                                 |
| -------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------- |
| **Isolated margin**        | Each position has its **own margin**. A liquidation in one position does **not** automatically consume the margin locked in another position. |
| **Long and short trading** | You can hold long or short exposure on supported markets, with USDC as collateral.                                                            |
| **Leverage**               | You can increase notional exposure within the allowed range for each market.                                                                  |
| **Transparent pricing**    | Mark price drives unrealized PnL, funding, and liquidation logic. Executions apply the platform's published slippage rules.                   |
| **TP and SL protection**   | You can attach take-profit and stop-loss rules when placing an order or after the position is open.                                           |

***

### Recommended reading order

1. [**Pricing**](pricing.md) — where the mark price comes from
2. [**Order**](order.md) — how orders execute and how slippage works
3. [**Position & Margin**](position-and-margin.md) — how margin, unrealized PnL, and liquidation distance work
4. [**Funding**](funding.md) — the hourly transfer between longs and shorts
5. [**Liquidations**](liquidations.md) — when forced closure can happen
6. [**Fees**](fees.md) — trading fees and liquidation-penalty handling
