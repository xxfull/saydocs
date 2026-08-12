---
description: How YesFi calculates composite index and mark prices.
metaLinks:
  alternates:
    - https://app.gitbook.com/s/KiKbOTrmqLWnXHD7ZyeJ/jiao-yi/ding-jia
---

# Pricing

### 1. Composite index price

YesFi retrieves real-time quotes from multiple external markets.\
Multi-source Oracles then produce a composite index price.

The index does not use one exchange's latest trade price.\
It does not simply average every market price.

The system validates price sources and filters abnormal quotes.\
It also adjusts weights to reduce single-market risk.

This design limits the impact of price anomalies and outages.\
It also limits technical failures and isolated abnormal trades.

The composite index updates continuously.\
Refresh rates vary by pair, market conditions, and quote availability.

### 2. Index price sources

#### 2.1 Crypto derivatives sources

YesFi can connect to these crypto derivatives markets:

* Binance USDT-margined futures
* OKX perpetual swaps
* Bybit linear perpetuals
* Bitget USDT-margined futures
* Hyperliquid perpetuals
* Kraken Futures

#### 2.2 Equity, xStock, FX, and index sources

YesFi can also connect to these sources:

* Gate stock perpetuals
* Kraken xStock spot
* Bitget stock-token spot
* Kraken FX spot
* MEXC stock and index perpetuals
* Gate xStock spot
* DipCoin perpetuals

The price sources used for each pair can differ.\
They depend on the following factors:

* Whether the external market supports the asset
* Whether the source is enabled
* Whether the quote is valid and current
* Whether the quote passes anomaly checks
* The pair's configured Oracle rules

This list describes available market connections.\
It does not mean every pair uses every source.

### 3. Index price design principles

#### 3.1 Multi-source pricing

Multiple external markets contribute to the composite index.\
This reduces reliance on a single exchange.

#### 3.2 Anomaly filtering

Quotes may receive lower weights when they materially diverge.\
Quotes may be excluded when they exceed normal market movement.

#### 3.3 Quote freshness

The system continuously checks quote status.\
Invalid, stale, or unavailable quotes are not used.

#### 3.4 Source consistency

The system publishes a new index only after sources meet requirements.\
Requirements cover valid-source count and consistency.

#### 3.5 Weighted aggregation

Validated sources contribute according to configured weights.\
Weights can vary by market coverage, quote quality, and configuration.

### 4. Index price calculation

#### 4.1 Retrieve and normalize quotes

The system retrieves price data through external market APIs.\
Available quote fields can include:

* Index price
* Mark price
* Best bid
* Best ask
* Latest trade price

The system normalizes trading-pair names and quote fields.\
It then sends the data through the calculation process.

#### 4.2 Basic validation

A price source may not join the current calculation when:

* Its index price is missing or invalid
* Both mid price and latest trade price are unavailable
* Its quote has not updated for an extended period
* Its market-data connection has failed
* The market does not support the asset
* The pair configuration disables the source

Some sources support fallback queries.\
The system may use another market-data interface when live quotes fail.

#### 4.3 Per-source movement checks

The system tracks a smoothed price for each source.\
This helps identify abnormal price jumps.

$$
E_{i,t}=\alpha P_{i,t}+(1-\alpha)E_{i,t-1}
$$

Where:

* $$P_{i,t}$$: current index price from source $$i$$
* $$E_{i,t}$$: current smoothed price for source $$i$$
* $$E_{i,t-1}$$: previous smoothed price for source $$i$$
* $$\alpha$$: coefficient determined by the smoothing window

The relative deviation from the smoothed price is:

$$
D_{i,\mathrm{EMA}}=\frac{|P_{i,t}-E_{i,t}|}{E_{i,t}}
$$

The system handles deviations as follows:

* Normal deviations allow the source to contribute normally.
* Soft-limit deviations reduce the source's effective weight.
* Hard-limit deviations exclude the source from the current calculation.

#### 4.4 Market median checks

Sources passing basic validation calculate the market median:

$$
P_{\mathrm{median}}=\operatorname{median}(P_1,P_2,\ldots,P_n)
$$

The system then calculates each source's deviation from that median:

$$
D_i=\frac{|P_i-P_{\mathrm{median}}|}{P_{\mathrm{median}}}
$$

Where:

* $$P_i$$: index price from source $$i$$
* $$P_{\mathrm{median}}$$: median of current candidate prices
* $$D_i$$: source $$i$$'s relative deviation from the median

Quotes beyond the configured threshold do not join the calculation.\
Thresholds can vary by asset, source characteristics, and market conditions.

#### 4.5 Valid-source checks

After filtering abnormal quotes, the system checks:

1. Whether valid sources meet the minimum count.
2. Whether valid sources meet the required candidate-source ratio.

The valid-source ratio is:

$$
R_{\mathrm{valid}}=\frac{N_{\mathrm{valid}}}{N_{\mathrm{candidate}}}
$$

Where:

* $$N_{\mathrm{valid}}$$: sources passing all checks
* $$N_{\mathrm{candidate}}$$: sources with basically valid quotes this round

The system calculates a new index only when both requirements pass.\
Updates may pause when too few sources remain valid.

The system resumes updates once sources recover and meet requirements again.

#### 4.6 Weighted composite index

All validated sources contribute using their effective weights:

$$
P_{\mathrm{index}}=
\frac{\sum_{i=1}^{n}P_iW_i}{\sum_{i=1}^{n}W_i}
$$

Where:

* $$P_{\mathrm{index}}$$: composite index price
* $$P_i$$: index price from valid source $$i$$
* $$W_i$$: source $$i$$'s effective weight after anomaly checks
* $$n$$: number of valid sources in the calculation

A soft-deviation safeguard can reduce a source's effective weight.\
The result reflects the current composite price across valid external markets.

### 5. Mark price

The composite index represents the broader external market price.\
YesFi also produces a mark price using the market basis.

The market basis is the difference between valid market prices and the index.

#### 5.1 Basis calculation

For each valid source, the system calculates the basis:

$$
B_i=P_{\mathrm{mid},i}-P_{\mathrm{index}}
$$

Where:

* $$P_{\mathrm{mid},i}$$: mid price or valid market price from source $$i$$
* $$P_{\mathrm{index}}$$: composite index price
* $$B_i$$: market basis for source $$i$$

The system uses the median valid basis.\
This reduces the impact of an abnormal basis on one market.

#### 5.2 Basis smoothing

The median basis is smoothed with an exponential moving average:

$$
B_t=\alpha B_{\mathrm{median},t}+(1-\alpha)B_{t-1}
$$

Where:

* $$B_t$$: current smoothed basis
* $$B_{\mathrm{median},t}$$: median basis from valid sources this round
* $$B_{t-1}$$: previous smoothed basis
* $$\alpha$$: coefficient determined by the smoothing window

#### 5.3 Mark price calculation

The final mark price is:

$$
P_{\mathrm{mark}}=P_{\mathrm{index}}+B_t
$$

The mark price supports position valuation and risk assessments.\
It can differ from the composite index due to the smoothed basis.

### 6. Updates and anomaly handling

#### 6.1 Partial source failures

When some sources fail, the system excludes abnormal sources first.\
It calculates a new index from the remaining valid sources.

This continues only when count and consistency requirements still pass.

#### 6.2 Insufficient valid sources

The system may pause new index calculations when valid sources are insufficient.\
It also pauses when sources do not meet consistency requirements.

The system does not force an index from incomplete or unreliable quotes.\
Updates resume when the requirements are met again.

### 7. Price definitions

* **Composite index price**: Weighted price from filtered external market sources.
* **Mark price**: Composite index plus the smoothed market basis.
* **Execution price**: Price at which a user's order actually executes.

These prices serve different purposes and can differ.\
The composite index does not guarantee an execution at that price.

Order direction, trading rules, and applicable slippage affect execution prices.

### 8. Risk disclosure

1. Multi-source aggregation reduces, but cannot remove, market and technical risks.
2. Price sources can differ across trading pairs.
3. The system may exclude failed, stale, or abnormal sources.
4. Composite index updates may pause when too few valid sources remain.
5. External markets can show short-term price differences during rapid movements.
6. Composite index, mark, and execution prices can differ.
7. Displayed prices reflect the system at that time. Execution records govern final trade results.
