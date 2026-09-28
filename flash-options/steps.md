# Steps

### **Rules** <a href="#cc807bdb" id="cc807bdb"></a>

* Settlement uses the highest tier reached by the asset path within 5 minutes.
* Available durations are 30s, 60s, 3min (standard), and 5min.
* The minimum amount is 10u. The maximum amount is 500u.
* There are 4 upward tiers based on distance from the current price.
* Payouts are not fixed. The values below illustrate one possible configuration.
* The current tier thresholds and payouts appear before the user buys:
  * Tier 1: +0.18% → 2x payout (example; easiest to reach)
  * Tier 2: +0.39% → 4x payout (example)
  * Tier 3: +0.60% → 8x payout (example)
  * Tier 4: +1.11% → 16x payout (example; top tier)
* If the price path never reaches Tier 1, the position expires worthless.

### **Example configuration (5min, BTC)** <a href="#id-9045fad8" id="id-9045fad8"></a>

* At 10:00, BTC is trading at $97,419. A retail user buys a `5min Step Card` for a 5u premium.
* BTC price path during the next 5 minutes:
  * 10:01 reaches $97,600 (+0.19%) → locks Tier 1 at 2x
  * 10:02 rises to $97,800 (+0.39%) → upgrades to Tier 2 at 4x
  * 10:03 reaches $98,050 (+0.65%) → upgrades to Tier 3 at 8x
  * 10:04 pulls back to $97,700
  * 10:05 closes at $97,650
* Settlement rule: the highest price on the path is $98,050. That is +0.65%, above Tier 3 at +0.60%, so settlement uses 8x.
* The user stakes 5u → receives 40u.

### **Illustrative payouts by duration** <a href="#e5b504b9" id="e5b504b9"></a>

Shorter durations can offer higher payouts for the same tier. Actual payouts vary by configuration:

* 30s top tier → 40x example
* 60s top tier → 25x example
* 5min top tier → 16x example
* 15min top tier → 10x example
