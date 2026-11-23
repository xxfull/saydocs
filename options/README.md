# Options

YesFi offers three lines of options. All three are buy-only: you pay up front, the most you can lose is what you paid, and there is no margin or liquidation. All settle in USDC.

* [**Flash Options**](https://docs.yesfi.com/flash-options): fixed-payout predictions that settle in seconds to minutes, across seven modes.
* [**Regular Options**](regular-options.md): listed BTC calls and puts, with expiries from one day to several months.
* [**0DTE Options**](0dte-options.md): Regular Options on their last day, for a low-cost position on today’s move.

### Compare the three lines

|             | Flash Options                                | Regular Options                                                                               | 0DTE Options                          |
| ----------- | -------------------------------------------- | --------------------------------------------------------------------------------------------- | ------------------------------------- |
| What it is  | Digital option with a fixed payout multiple  | Listed call or put                                                                            | Listed call or put that expires today |
| Duration    | 30s – 5min for most modes                    | Daily, weekly, monthly and quarterly expiries                                                 | Expires at the next 08:00 UTC         |
| Underlyings | Crypto, gold, oil, FX and US stocks, by mode | BTC                                                                                           | BTC                                   |
| You choose  | Mode, asset, duration, amount                | Expiry, Call / Put, strike, contracts                                                         | Call / Put, strike, contracts         |
| You pay     | A fixed amount, 1 – 5,000 USDC by mode       | Premium × contracts                                                                           | Premium × contracts                   |
| Payout      | Amount × multiple, fixed when you open       | Calls: (settlement price − strike) × contracts. Puts: (strike − settlement price) × contracts | Same as Regular Options               |
| Close early | No                                           | Yes                                                                                           | Yes                                   |
| Max loss    | Amount paid                                  | Premium paid                                                                                  | Premium paid                          |

### Key terms

* **Premium**: what you pay to open. For Flash Options it is the amount you choose; for Regular and 0DTE Options it is the price per contract × contracts. It is the most you can lose.
* **Payout multiple** (Flash Options): what you receive per 1 USDC if your prediction is met, fixed when you open.
* **Call / Put**: a call pays out if the price settles above the strike; a put pays out if it settles below.
* **Strike**: the price a Regular or 0DTE option is measured against at expiry, shown in $.
* **Expiry**: when the option settles. Regular and 0DTE Options expire at 08:00 UTC.
* **Contracts**: the quantity of a Regular or 0DTE option. 1 contract = 1 BTC; fractions such as 0.001 contracts are allowed.
* **Breakeven**: the settlement price at which you get back exactly what you paid. Call: strike + premium per contract. Put: strike − premium per contract.
* **ITM / ATM / OTM**: in, at, or out of the money. An OTM option costs less but needs a bigger move to pay out.

### FAQ

**What is the most I can lose?** The premium you paid. Buying an option never creates margin calls or liquidation.

**How is this different from Flash Options?** Flash Options pay a fixed multiple set when you open and cannot be closed early. Regular and 0DTE Options pay according to how far the settlement price ends past the strike, and can be closed before expiry.

### Risks

* Most OTM options, and most 0DTE options, expire worthless. Only trade amounts you can afford to lose.
* Option prices move fast with the underlying, volatility and time. Your close price can be far below what you paid.
* Quotes can pause, for example while the settlement price is being confirmed. You cannot open or close during a pause.

See [Risk disclosure](https://docs.yesfi.com/risk-and-policy/risk-disclosure) for full terms.

