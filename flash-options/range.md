# Range

### **Rules** <a href="#ilnov" id="ilnov"></a>

* You win if the asset price settles inside the selected preset range. If it settles outside the range, the premium is lost.
* Available durations are 30s, 60s, 5min, and 10min.
* The minimum amount is 1u. The maximum amount is 500u.
* The three bands are mutually exclusive. You can choose only one:
  * Inner band: ±0.1% (hardest to hit, highest payout)
  * Middle band: ±0.3% (medium hit rate)
  * Outer band: ±0.5% (easiest to hit, lowest payout)

### **Example (1min, Gold)** <a href="#id-0d11394e" id="id-0d11394e"></a>

* At 10:00, gold is trading at $3,500. The user selects `1min Gold within the ±0.1% inner band` — that is, \[$3,496.5, $3,503.5] — with a 5u premium and a 47x payout.
* At 10:01, gold closes at $3,502.8 → hit ✓
* The user stakes 5u → receives 235u

### **Payout rules** <a href="#jpgij" id="jpgij"></a>

Shorter duration + narrower range + farther from the current price → higher payout
