# Trend

### **Rules**

* Choose any asset and predict the price direction (Up/Down) after a set time. If the price moves by the specified amount, you win the corresponding payout; if it doesn't, you lose your stake.
* Time options: 60s, 3 minutes, or 5 minutes
* Three movement tiers — Light / Medium / Heavy: higher threshold = higher payout odds = harder to win
* Minimum stake: 10u; maximum stake varies by tier (10u–5,000u; higher-odds tiers have lower stake caps)
* Available assets: BTC, ETH, SOL, Gold, Crude Oil, JPY (24 hours); NVIDIA, SPCX (US market hours), etc.

### **Example**

Using 60s as an example: at 10:00:00, a user selects BTC Long and places an order. Three tiers are available:

**Light:** Target move of +0.05% (BTC must rise at least \~$39 within 60 seconds)

* Actuarial logic: Requires sustained small buy orders to push price up. With this small threshold added, the win probability compresses to \~33%, pushing the payout to 2.83x.

**Medium:** Target move of +0.12% (BTC must rise at least \~$92 within 60 seconds)

* Actuarial logic: Requires a clear one-sided buying surge. A 0.12% gain in 60 seconds qualifies as a "mini breakout," compressing win probability to \~15% and pushing the payout to 6.4x.

**Heavy:** Target move of +0.20% (BTC must rise at least \~$154 within 60 seconds)

* Actuarial logic: A 0.20% BTC move in 60 seconds is equivalent to a "whale sweep" or breaking news event. Win probability is only \~3%, with a payout of up to 28x.

At 10:01 settlement: BTC actual gain is +0.14%, exceeding the Medium tier threshold of 0.12%. A 10u bet on Medium wins 64u. A bet on Heavy loses the stake.

**Payout Structure**

* Longer timeframes allow larger price swings, so thresholds are adjusted accordingly — but the three-tier payout structure is always maintained: 2.83x / 6.4x / 28x. The 28x payout is a platform hard cap for risk control. It is the highest-excitement tier and large stakes are not recommended.
