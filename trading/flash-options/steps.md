# Steps

### **Rules** <a href="#cc807bdb" id="cc807bdb"></a>

* Settlement uses the highest tier reached by the asset path within 5 minutes.
* Available durations are 30s, 60s, 5min (standard), and 15min.
* The minimum amount is 1u. The maximum amount is 500u.
* There are 4 upward tiers based on distance from the current price:
  * Tier 1: +0.18% → 2x payout (easiest to reach)
  * Tier 2: +0.39% → 4x payout
  * Tier 3: +0.60% → 8x payout
  * Tier 4: +1.11% → 16x payout (top tier)
* If the price path never reaches Tier 1, the position expires worthless.

### **Example (5min, BTC)** <a href="#id-9045fad8" id="id-9045fad8"></a>

* At 10:00, BTC is trading at $97,419. A retail user buys a `5min Step Card` for a 5u premium.
* BTC price path during the next 5 minutes:
  * 10:01 reaches $97,600 (+0.19%) → locks Tier 1 at 2x
  * 10:02 rises to $97,800 (+0.39%) → upgrades to Tier 2 at 4x
  * 10:03 reaches $98,050 (+0.65%) → upgrades to Tier 3 at 8x
  * 10:04 pulls back to $97,700
  * 10:05 closes at $97,650
* Settlement rule: the highest price on the path is $98,050. That is +0.65%, above Tier 3 at +0.60%, so settlement uses 8x.
* The user stakes 5u → receives 40u.

### **Payout rules by duration** <a href="#e5b504b9" id="e5b504b9"></a>

The shorter the duration, the lower the probability of reaching the same tier, so the payout is higher:

* 30s top tier → 40x
* 60s top tier → 25x
* 5min top tier → 16x
* 15min top tier → 10x
