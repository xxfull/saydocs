---
metaLinks:
  alternates:
    - https://app.gitbook.com/s/KiKbOTrmqLWnXHD7ZyeJ/jiao-yi/qiang-ping
---

# Liquidations

**Liquidation** is the most passive type of position close in perpetual trading. It happens when the equity of your isolated position falls below the platform's maintenance requirement under the mark-price framework.

The goal is to cap losses within the margin assigned to that position and keep risk from spreading in a disorderly way.

### When liquidation happens

Under **isolated margin**, a position becomes liquidatable when its equity falls **strictly below** the required maintenance margin.

Position equity is broadly driven by:

* current margin
* unrealized PnL
* liquidation-related fee or penalty logic where applicable

Important details:

* Liquidation logic uses the **mark price**, not the best visible order-book price.
* The same pricing framework also governs the relevant accounting path.
* When you approach the maintenance line, the assistant can try to warn you.

### What you can still do before liquidation

| Action                              | Effect                                                                                |
| ----------------------------------- | ------------------------------------------------------------------------------------- |
| **Add isolated margin**             | Increases equity and moves the liquidation threshold farther away.                    |
| **Reduce leverage or exposure**     | Lowers pressure on the maintenance requirement where the product allows it.           |
| **Use stop-loss or close manually** | Exits before forced liquidation and can help you avoid liquidation-related penalties. |

### How to understand liquidation price

The estimated liquidation price depends on current margin, position size, entry price, maintenance settings, and other live variables.

It can change when you:

* partially close a position
* pay or receive funding
* adjust leverage
* add or remove margin
