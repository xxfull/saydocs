# Moves

### Rules

* Pick any asset. You do not bet on direction. You only bet on the price movement during the next period.
* The price range during the selected period, `highest price − lowest price`, is split into 5 mutually exclusive bands. The user picks one band.
* Duration options: `30s`, `1 minute`, `3 minutes`, `5 minutes`
* Minimum stake: `10u`. Maximum stake depends on the band, up to `5000u`.
* Range % = `(highest price during the period − lowest price during the period) / starting price × 100%`
* Starting price = the price at the exact second when the user places the bet

### Example gameplay (5 minutes, BTC)

At `14:00:00`, BTC = `$77,000`. The user enters the 5-minute Moves market. The system shows 5 mutually exclusive bands:

😴 Sleep Zone: BTC 5-minute high-low range `< 0.115%` (about `$0 – $89`)

🚶 Steady Zone: BTC 5-minute high-low range `0.115% – 0.273%` (about `$89 – $210`)

🏃 Active Zone: BTC 5-minute high-low range `0.273% – 0.420%` (about `$210 – $323`)

⚡ Shock Zone: BTC 5-minute high-low range `0.420% – 0.600%` (about `$323 – $462`)

💥 Avalanche Zone: BTC 5-minute high-low range `> 0.600%` (about `> $462`)

The total probability across all 5 bands equals `100%`. The user must pick exactly one.

### Odds adjustment rules

* Odds for the 5 bands: Sleep `11.9x`, Steady `2.26x`, Active `3.40x`, Shock `5.94x`, Avalanche `15.8x` — a U-shaped distribution.
* The middle band, Steady, has the highest probability and the lowest odds.
* The edge bands, Sleep and Avalanche, have the lowest probability and the highest odds.
* Band boundaries adjust every second based on market volatility.
