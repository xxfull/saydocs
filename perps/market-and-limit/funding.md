---
metaLinks:
  alternates:
    - https://app.gitbook.com/s/KiKbOTrmqLWnXHD7ZyeJ/jiao-yi/zi-jin-fei
---

# Funding

**Funding** is the standard mechanism that helps perpetual perps stay closer to the underlying market even though they have no expiry date. At each settlement interval, value transfers between longs and shorts.

YesFi currently settles funding on an **hourly** basis unless the live product configuration says otherwise.

***

### Where the money comes from and where it goes

* Each period, the protocol measures long and short exposure for the market.
* If one side needs to pay funding, positions on that side pay in proportion to their size.
* Positions on the other side receive the transfer.
* Whether you pay or receive depends on the market, the funding rate sign, and your position direction.

***

### Funding calculation

$$
\text{Hourly funding} \approx |r| \times (\text{position size} \times \text{mark price}) = |r| \times \text{notional value}
$$

Where:

* **`r`** is the funding rate for the current period
* **`r > 0`** usually means longs pay shorts
* **`r < 0`** usually means shorts pay longs
* **`|r|`** determines the magnitude of the transfer

The actual funding rate can change each hour. Do **not** extrapolate one historical hour across an entire holding period.

***

### Where the funding rate comes from

The funding rate can combine external market inputs with YesFi's internal position state and exposure balance.

***

### Important notes

* If long and short exposure is effectively balanced, funding for that hour can be zero or near zero.
* Funding rates are dynamic.
* Funding can move value into or out of your position margin every hour while the position stays open.
