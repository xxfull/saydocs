---
metaLinks:
  alternates:
    - >-
      https://app.gitbook.com/s/KiKbOTrmqLWnXHD7ZyeJ/jiao-yi/cang-wei-yu-bao-zheng-jin
---

# Position & Margin

A **position** is your perps exposure on one market and one direction. It carries its own margin, average entry price, size, unrealized PnL, and liquidation distance.

**Margin** is the **USDC** committed to that position. It absorbs volatility, covers funding transfers, and determines how close the position is to liquidation. YesFi uses **isolated margin**, so each position manages its own risk by default.

***

### What you see in the interface

On the **current positions** page, you can usually filter by **All accounts** to switch between Traders or sub-accounts.

Typical columns:

| Column            | Meaning                                                                          |
| ----------------- | -------------------------------------------------------------------------------- |
| **SYMBOL**        | The perps market, such as `BTC-USD`.                                             |
| **SIDE**          | Direction and leverage, such as `LONG 10x` or `SHORT 10x`.                       |
| **ACCOUNT**       | The AI Trader or sub-account that owns the position.                             |
| **POSITION SIZE** | Current position size in the underlying asset, not in USD notional.              |
| **MARGIN**        | Margin locked for this position, usually shown in USDC.                          |
| **ENTRY**         | Average entry price for the position.                                            |
| **MARK**          | Current mark price. The same area can also show the estimated liquidation price. |
| **UNREALIZED**    | Unrealized PnL and return percentage, based on mark price relative to entry.     |
| **TX HASH**       | A link to the related on-chain transaction where available.                      |
| **Actions**       | Controls such as **Partial close** or **Close all**.                             |

Funding can change effective margin over time because it moves value into or out of the position. See [**Funding**](funding.md).

***

### Why YesFi uses isolated margin

* **One position does not automatically consume another position's margin**
* **Strategy separation is clearer**, especially when you use multiple Traders or sub-accounts

***

### After you close a position

* A **full close** ends the position. PnL becomes realized and appears in history or account records.
* A **partial close** releases part of the margin and realizes the corresponding share of PnL and fees.

***

### Margin concepts

1. **Initial margin**\
   When you open a position, leverage determines how much margin you need to lock for the chosen notional.
2. **Maintenance margin**\
   While the position remains open, your margin plus unrealized PnL must stay above the platform's maintenance requirement.
3. **Liquidation price**\
   The estimated liquidation price depends on current mark price, size, margin, maintenance settings, and other live factors such as funding or manual margin changes.
