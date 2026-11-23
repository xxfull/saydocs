# 0DTE Options

0DTE (zero days to expiry) Options are Regular Options on their last day. Premiums are small because little time is left, so a small move can multiply the premium, and no move means the option expires worthless.

### Rules

* All Regular Options rules apply: same underlying (BTC), quantity, order limits, order types, fees and settlement.
* 0DTE options expire at 08:00 UTC. After 08:00 UTC, the 0DTE Zone shows the options expiring at 08:00 UTC the next day.
* The 0DTE Zone lists featured OTM options with a countdown to expiry.
* New orders stop shortly before expiry. Existing positions can still be closed until the closing cutoff, which is also shortly before expiry.
* Trading pauses while the settlement price is being confirmed.

### Example (BTC 0DTE call)

* At 08:45 UTC, BTC is trading at $64,500. The user buys `0.1 contracts of BTC-17NOV26-65500-C`, a $65,500 call expiring at 08:00 UTC the next day, at 284 USDC per contract.
* Cost: 284 × 0.1 = 28.40 USDC. Breakeven: $65,500 + $284 = $65,784.
* At expiry BTC settles at $66,500 → settlement (66,500 − 65,500) × 0.1 = 100 USDC, net profit 100 − 28.40 = 71.60 USDC ✓
* If BTC settles at or below $65,500 → the option expires worthless, loss 28.40 USDC ✗

### Payout rules

Less time left + further from the current price → cheaper premium, higher payoff multiple, and a higher chance of expiring worthless.

### How to trade

1. Go to **Options** and open the **0DTE Zone**.
2. Pick a strike and tap **Call** or **Put**.
3. Enter the quantity in **Contracts**, choose **Market** or **Limit**, check the cost and breakeven, then confirm.
4. Close early under **Positions**, or let it settle automatically at 08:00 UTC.

### FAQ

**Why does my 0DTE option say it expires tomorrow?** Options expire at 08:00 UTC. After that time, the next 0DTE options expire at 08:00 UTC the following day.

**How is 0DTE different from Regular Options?** Only the time left. 0DTE options are the Regular Options closest to expiry, so they are cheaper and their value changes faster.
