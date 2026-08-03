---
description: >-
  Market orders, limit orders, and TP or SL rules all follow the same trading
  model.
metaLinks:
  alternates:
    - https://app.gitbook.com/s/KiKbOTrmqLWnXHD7ZyeJ/jiao-yi/ding-dan
---

# Order

You can place orders through chat or through manual controls in the interface. Behind both flows, the product uses the same order model: market orders, limit orders, and TP or SL rules attached to positions.

### Common order types

| Type                        | Best for                                                                                                    |
| --------------------------- | ----------------------------------------------------------------------------------------------------------- |
| **Market**                  | You want to execute **immediately** using the current mark-price framework and accepted platform slippage.  |
| **Limit**                   | You have a target price and want execution only if the price is favorable enough.                           |
| **Take-profit / stop-loss** | You want the system to close all or part of a position automatically when the trigger condition is reached. |

TP and SL rules do **not** need to stay visible as always-open conditional orders in the main order list. After the position is open, they can be stored as position protection rules. When triggered, they appear as executed close records.

***

### Slippage: slightly worse on the execution side

To handle market movement and execution risk, the system applies slippage at the **basis-point** level on top of the mark-price path. In practical terms:

* **Buy-side execution** can be slightly higher
* **Sell-side execution** can be slightly lower

This is standard side-protection logic. Exact values follow the live configuration and interface disclosure.

Typical direction mapping:

* **Open long** or **close short** follows buy-side slippage
* **Open short** or **close long** follows sell-side slippage

#### What this means for you

Your final execution price can differ from third-party quotes by a few basis points. PnL and fee calculations still use consistent and reproducible platform rules.

***

### Leverage

You choose leverage within the allowed range for the market. Actual limits vary by symbol and product configuration. Always rely on the live interface.

For related mechanics, see [**Position & Margin**](position-and-margin.md) and [**Fees**](fees.md).
