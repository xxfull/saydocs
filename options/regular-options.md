# Regular Options

Regular Options are listed call and put options on BTC. You choose an expiry, a direction and a strike, and pay a premium in USDC. The most you can lose is the premium.

### Rules

* Before expiry you can close all or part of your position at the quoted close price. New orders stop shortly before expiry, and closing also stops close to expiry; after that the position is held to settlement.
* At expiry the option is cash-settled in USDC, using the average BTC price from the YesFi price feed over the last 30 minutes before expiry (07:30–08:00 UTC). No BTC is delivered:
  * Call: (settlement price − strike) × contracts, if the settlement price is above the strike.
  * Put: (strike − settlement price) × contracts, if the settlement price is below the strike.
  * Otherwise the option expires worthless and the premium is lost.
* Fees: limited-time free trading. Opening, early close and settlement at expiry are all charged at 0% for now. We’ll announce before any fees apply.

### Example (BTC call, 11 days to expiry)

* BTC is trading at $64,500. The user buys `0.1 contracts of BTC-27NOV26-67000-C`, a $67,000 call expiring at 08:00 UTC on 27 Nov, at 968 USDC per contract.
* Cost: 968 × 0.1 = 96.80 USDC. Breakeven: $67,000 + $968 = $67,968.
* At expiry BTC settles at $70,000 → settlement (70,000 − 67,000) × 0.1 = 300 USDC, net profit 300 − 96.80 = 203.20 USDC ✓
* If BTC settles at or below $67,000 → the option expires worthless, loss 96.80 USDC ✗

### Payout rules

Further out of the money + shorter time to expiry → cheaper premium, but a larger move is needed to pay out.

### How to trade

1. Go to **Options** and open **Regular Options**.
2. Pick an expiry.
3. In the option chain, pick a strike and tap **Call** or **Put**.
4. Enter the quantity in **Contracts** and choose **Market** or **Limit**.
5. Check the premium, Est. cost, breakeven and the payoff scenario, then confirm.
6. Track the trade under **Positions**. To exit early, close all or part of it; otherwise it settles automatically at expiry.

### FAQ

**Do I need to exercise the option?** No. In-the-money options settle automatically in USDC at expiry.

**Can I sell before expiry?** Yes. Close all or part of your position at the quoted close price. The value can be higher or lower than what you paid.

**Where does the settlement price come from?** Settlement uses the average BTC price from the YesFi price feed over the last 30 minutes before expiry (07:30–08:00 UTC). If quotes are delayed, data is abnormal or the source market halts, opening, closing or settlement may be paused or delayed.
