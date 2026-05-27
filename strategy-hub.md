---
hidden: true
---

# Strategy Hub

Real-time strategy discovery and execution. Combining signal intelligence from top traders with a multi-factor scoring model—integrating real-time news, on-chain data, macro events, and technical indicators—to generate top-ranked, actionable trading strategies.

### Core philosophy

<table data-card-size="large" data-view="cards"><thead><tr><th></th><th></th><th data-hidden data-card-cover data-type="image">Cover image</th></tr></thead><tbody><tr><td><h4>Insights from top traders</h4></td><td>Strategies aren't generated mechanically - they reflect the reasoning patterns, risk preferences, and timing instincts of proven high-performance traders, encoded as reusable signal templates.</td><td><a href="https://images.unsplash.com/photo-1629339942248-45d4b10c8c2f?crop=entropy&#x26;cs=srgb&#x26;fm=jpg&#x26;ixid=M3wxOTcwMjR8MHwxfHNlYXJjaHw4fHx0cmFkZXJ8ZW58MHx8fHwxNzc5ODY0MDkyfDA&#x26;ixlib=rb-4.1.0&#x26;q=85">https://images.unsplash.com/photo-1629339942248-45d4b10c8c2f?crop=entropy&#x26;cs=srgb&#x26;fm=jpg&#x26;ixid=M3wxOTcwMjR8MHwxfHNlYXJjaHw4fHx0cmFkZXJ8ZW58MHx8fHwxNzc5ODY0MDkyfDA&#x26;ixlib=rb-4.1.0&#x26;q=85</a></td></tr><tr><td><h4>Continuous signal ingestion</h4></td><td>The system monitors live news feeds, social sentiment, on-chain flows, and technical pattern formation simultaneously - re-scoring strategies as new information arrives.</td><td><a href="https://images.unsplash.com/photo-1584359983106-ef9366f27454?crop=entropy&#x26;cs=srgb&#x26;fm=jpg&#x26;ixid=M3wxOTcwMjR8MHwxfHNlYXJjaHw4fHxsaXZlJTIwbmV3c3xlbnwwfHx8fDE3Nzk4NjQxNDV8MA&#x26;ixlib=rb-4.1.0&#x26;q=85">https://images.unsplash.com/photo-1584359983106-ef9366f27454?crop=entropy&#x26;cs=srgb&#x26;fm=jpg&#x26;ixid=M3wxOTcwMjR8MHwxfHNlYXJjaHw4fHxsaXZlJTIwbmV3c3xlbnwwfHx8fDE3Nzk4NjQxNDV8MA&#x26;ixlib=rb-4.1.0&#x26;q=85</a></td></tr><tr><td><h4>Multi-factor scoring</h4></td><td>Each strategy receives a composite score computed across four independent signal layers. No single factor dominates - confidence requires corroboration across dimensions.</td><td><a href="https://images.unsplash.com/photo-1719464521902-4dc9595b182d?crop=entropy&#x26;cs=srgb&#x26;fm=jpg&#x26;ixid=M3wxOTcwMjR8MHwxfHNlYXJjaHw2fHxidXklMjBzdHJhdGVneXxlbnwwfHx8fDE3Nzk4NjQ0NzF8MA&#x26;ixlib=rb-4.1.0&#x26;q=85">https://images.unsplash.com/photo-1719464521902-4dc9595b182d?crop=entropy&#x26;cs=srgb&#x26;fm=jpg&#x26;ixid=M3wxOTcwMjR8MHwxfHNlYXJjaHw2fHxidXklMjBzdHJhdGVneXxlbnwwfHx8fDE3Nzk4NjQ0NzF8MA&#x26;ixlib=rb-4.1.0&#x26;q=85</a></td></tr><tr><td><h4>Two execution modes</h4></td><td><strong>Flash Options -</strong> sub-minute settlement with fixed multiplier payouts.<br><strong>Contract Signals -</strong> leveraged perpetuals with defined entry, target, and stop-loss.</td><td><a href="https://images.unsplash.com/photo-1590283603385-17ffb3a7f29f?crop=entropy&#x26;cs=srgb&#x26;fm=jpg&#x26;ixid=M3wxOTcwMjR8MHwxfHNlYXJjaHwxfHwlRTQlQkElQTQlRTYlOTglOTN8ZW58MHx8fHwxNzc5ODY0Mjk4fDA&#x26;ixlib=rb-4.1.0&#x26;q=85">https://images.unsplash.com/photo-1590283603385-17ffb3a7f29f?crop=entropy&#x26;cs=srgb&#x26;fm=jpg&#x26;ixid=M3wxOTcwMjR8MHwxfHNlYXJjaHwxfHwlRTQlQkElQTQlRTYlOTglOTN8ZW58MHx8fHwxNzc5ODY0Mjk4fDA&#x26;ixlib=rb-4.1.0&#x26;q=85</a></td></tr></tbody></table>

### Signal layer architecture

{% stepper %}
{% step %}
#### Layer 1 - News & macro events

Real-time parsing of financial news, regulatory announcements, geopolitical developments, and macroeconomic data releases. High-impact events (Fed decisions, exchange listings, protocol exploits) trigger immediate strategy re-evaluation.
{% endstep %}

{% step %}
#### Layer 2 - Technical pattern recognition

Automated chart structure detection across multiple timeframes. Signals include breakout confirmations, volume divergence, candlestick formations, and key S/R level interactions — each assigned a pattern-strength confidence rating.
{% endstep %}

{% step %}
#### Layer 3 - On-chain & market microstructure

Wallet flow analysis, exchange net flows, large-address accumulation patterns, open interest changes, funding rates, and liquidation heatmaps. These signals detect institutional positioning before it manifests in price.
{% endstep %}

{% step %}
#### Layer 4 - Community & sentiment consensus

Aggregated signal contributions from verified top-traders within the YesFi community. Signals are weighted by each contributor's historical accuracy. Community consensus acts as a Bayesian prior that adjusts the composite score.
{% endstep %}
{% endstepper %}

### Strategy types

#### Flash options

Predict the price direction of an asset within a short settlement window. At expiry, the outcome is settled at a pre-locked fixed multiplier. No take-profit or stop-loss configuration is required — simply confirm direction (bullish / bearish) and settlement duration before placing the order. Both the upside and downside are fully defined at entry.

**Settlement windows**: ≤10s / ≤15s / ≤30s / ≤1min / ≥1min

**Required inputs**: direction + amount only&#x20;

**Max loss**: principal only, no liquidation

**Execution flow**: <mark style="background-color:$primary;">Select strategy</mark> -> <mark style="background-color:$primary;">Enter amount</mark> -> <mark style="background-color:$primary;">Place order</mark> -> <mark style="background-color:$primary;">Auto-settle</mark>

#### Contract signals

Directional trading strategies on perpetual contracts. Each signal includes a complete set of trade parameters — amount, leverage, take-profit, and stop-loss (this is a real-time trading signal and does not support limit orders). Traders can apply parameters with a single click or adjust them manually before execution. It is best suited for traders seeking larger profit windows and willing to hold positions for minutes to hours.

**Best for**:

{% hint style="success" %}
Clear trending market conditions
{% endhint %}

{% hint style="success" %}
Post-catalyst directional moves
{% endhint %}

{% hint style="success" %}
Traders with position management experience
{% endhint %}

**Watch out for**:&#x20;

{% hint style="danger" %}
Leverage can amplify losses – it is recommended to strictly implement stop-loss orders.
{% endhint %}

{% hint style="danger" %}
Slippage can affect entry price in volatile markets
{% endhint %}

{% hint style="danger" %}
Avoid heavy allocation to a single signal at high leverage
{% endhint %}

{% hint style="danger" %}
Monitor funding rate impact on holding cost
{% endhint %}

**Execution flow**: <mark style="background-color:$primary;">Read signal</mark> -> <mark style="background-color:$primary;">Verify params</mark> -> <mark style="background-color:$primary;">Place order</mark> -> <mark style="background-color:$primary;">Monitor</mark>

### Feed modes

<table data-card-size="large" data-view="cards"><thead><tr><th></th><th></th></tr></thead><tbody><tr><td><strong>Latest</strong></td><td>Sorted chronologically. All strategies scoring above the minimum threshold are sorted by publication date. Best suited for traders looking to capture the latest signals before participation increases.</td></tr><tr><td><strong>Trending</strong></td><td>Ranked by speed score: Overall signal strength × entry rate × sharing activity. Showcasing the strategies with the strongest community growth momentum.</td></tr><tr><td><strong>Following</strong></td><td>The strategies posted or endorsed by traders followed by the user. Personalized recommendations, with weighting based on the historical accuracy rate of the followed traders.</td></tr><tr><td><strong>Bookmarked</strong></td><td>User-defined storage strategy. Persistent storage across sessions. Support for commenting and customizing post-transaction logs.</td></tr></tbody></table>

