# How do modes differ in duration, triggers, and risk?

Modes mainly differ in three ways: observation period, prediction condition, and number of variables. YesFi offers Instant durations of 5 seconds, 30 seconds, 1 minute, and 5 minutes. Check the order page for the available durations and parameters.

| Product    | Duration                                      | Trigger condition                                                                | Main risk                                                                             |
| ---------- | --------------------------------------------- | -------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------- |
| Trend      | Usually observes a complete period            | At expiry, the price rises or falls relative to the start price and price spread | Near the start price, a small reverse move may invalidate the condition               |
| Instant    | The shortest period, often seconds or minutes | At the end of the period, price direction meets the selected condition           | Highly sensitive to instant moves and entry timing                                    |
| Range      | Observes the expiry period set in the order   | At expiry, price is inside or outside a specified range                          | A broadly correct view may still fail if price crosses a boundary                     |
| Volatility | Covers short or longer observation periods    | Price movement meets or does not meet a defined threshold                        | Direction does not matter; too little or too much movement can fail                   |
| Pair       | Both assets use the same period               | Compares the relative performance of two assets                                  | Relative strength matters, even if both assets rise or fall                           |
| Streak     | Covers multiple consecutive stages            | Multiple conditions are met in sequence or together                              | One unmet condition may affect settlement; more conditions are usually harder to meet |
| Ladder     | One period with multiple price levels         | Settlement follows the price level reached at expiry                             | Higher levels are usually harder to reach; results differ near a level boundary       |

### Trigger methods

* **Expiry-based**: Only the final price at settlement matters.
* **Path-based**: Touching a condition during the observation period may trigger it.

Rules on the confirmation page take precedence. Do not infer rules from a mode name alone. Shorter durations are more sensitive to short-term price changes.

Before confirming, check the entry price, duration, trigger method, settlement price source, payout multiplier, and maximum loss.

{% hint style="warning" %}
If a condition is not met, you may lose the entire amount paid for that trade.
{% endhint %}
