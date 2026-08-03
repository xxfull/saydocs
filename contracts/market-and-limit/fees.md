---
metaLinks:
  alternates:
    - https://app.gitbook.com/s/KiKbOTrmqLWnXHD7ZyeJ/jiao-yi/fei-yong
---

# Fees

### Trading fees for opening and closing

#### Core formulas and rounding

* **Notional value**

$$
N = Q \cdot P_{\text{fill}}
$$

* **Open fee**

$$
F_{\text{open}} = \mathrm{round}(N \cdot r,\ 8)
$$

* **Close fee**

$$
F_{\text{close}} = \mathrm{round}(Q \cdot P_{\text{exec}} \cdot r,\ 8)
$$

Where:

* **`Q`** is position size
* **`P_fill`** is the fill price for the opening trade
* **`P_exec`** is the execution price for the closing trade
* **`r`** is the fee rate

***

### Slippage

Slippage changes the execution price relative to the mark-price path in the published buy-side or sell-side direction. See [**Order**](order.md) for the trading behavior and interpretation.

***

### Penalty reservation

$$
R_p = M \times p
$$

Where:

* **`M`** is the current isolated `margin`
* **`p`** is the effective penalty rate for the market or global setting

If `M <= 0` or `p <= 0`, then:

$$
R_p = 0
$$

When the platform calculates equity for liquidation checks, marked equity can be represented as:

$$
E = M + PnL - R_p
$$

The maintenance requirement remains:

$$
\text{maintenance} = Q \cdot P_m \cdot m
$$

Liquidation becomes possible only when equity is **strictly below** the maintenance requirement.

For estimated liquidation-price calculations, effective margin can first be represented as:

$$
M_{\text{eff}} = M - R_p
$$

#### Cap on actual penalty deduction

Marked equity:

$$
\text{eq} = M + PnL
$$

Raw penalty:

$$
\text{penalty}_{\text{raw}} = \mathrm{round}(M \times p,\ 8)
$$

Actual penalty:

$$
\text{penalty} = \min(\text{penalty}_{\text{raw}},\ \text{eq})
$$

Remainder:

$$
\text{remainder} = \text{eq} - \text{penalty}
$$

This means the actual penalty does not exceed the positive equity that still remains in the position at that time.
