---
metaLinks:
  alternates:
    - https://app.gitbook.com/s/KiKbOTrmqLWnXHD7ZyeJ/jiao-yi/ding-jia
---

# Pricing

### Where the mark price comes from

#### 1. Trusted price sources across the full flow

The platform oracle provides aggregated quotes from multiple sources. The same pricing framework supports trading, liquidation checks, and conditional-rule scanning. This reduces the chance of one price for entry and a different price for risk control.

#### 2. Bad prices do not execute

* Only quotes that pass the platform's validity checks enter the system.
* The platform does **not** invent prices to force execution.
* If no fresh valid mark price is available, the system can reject or pause execution instead of using stale data.

#### 3. Consistent pricing rules across markets

Supported markets follow a consistent precision model and slippage framework. The same core rules apply regardless of direction or order size, subject to market-specific settings.

***

### Relationship to market and limit orders

* **Market orders** use the current valid mark-price framework plus the platform's execution rules.
* **Limit orders** use your specified price, together with the current mark price and slippage logic, to decide whether the order can execute at that moment.

***

### Summary

| Concept                  | What it means                                                                       |
| ------------------------ | ----------------------------------------------------------------------------------- |
| **Mark price**           | The main reference price for risk control and unrealized PnL.                       |
| **Your execution price** | A price derived from the mark-price path plus published slippage rules.             |
| **Abnormal quotes**      | If no valid price exists, the system can reject or pause instead of forcing a fill. |
