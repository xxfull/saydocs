---
description: >-
  Release notes for YesFi, including new features, improvements, and bug fixes
  by version.
icon: layer-plus
metaLinks:
  alternates:
    - >-
      https://app.gitbook.com/s/KiKbOTrmqLWnXHD7ZyeJ/guan-wu-sayfi/chan-pin-geng-xin
---

# Tech Log

{% hint style="info" %}
Dear YesFi Genesis Traders,

We are thrilled to announce that from now until **August 31, 24:00 (UTC)**, YesFi.com is officially entering its Beta Testing phase!

During this period, we will be stress-testing our platform—including **Quick Options**, **Signal Feed**, and the **Matching Engine**—under live market-making conditions. To ensure absolute system security and financial integrity for our upcoming Mainnet Launch, please review the following rules:

* **Trading Assets & PnL Reset**: All open positions, as well as unrealized and realized PnL accumulated during the Beta period, will be cleared and reset on **August 31 at 24:00 (UTC)**. Your initial deposited principal remains 100% safe and unaffected, and can be withdrawn at any time.
* **Permanently Retained Rewards**: All **Membership Levels** and **Y Points** earned during the Beta phase will be **100% permanently retained**! As a tribute to our early Genesis contributors, your status and points will directly map to your weekly reward distribution (Option & Insurance Vouchers) weight upon the official Mainnet Launch.

Thank you to every pioneer evolving with YesFi.

**One Yes, Trade All.**
{% endhint %}

{% updates format="full" %}
{% update date="2026-08-07" %}
## 1.0.8.3

* Corrected **Today's PnL** on the Assets page. It now includes realized PnL across all businesses and unrealized PnL from open contracts.
* Unified the cumulative PnL curve with account-overview data. It now refreshes immediately after `account` WebSocket updates.
* Refined daily-PnL refresh triggers. Filters now ignore unrelated accounts, duplicate events, and legacy frames.
* Option candle intervals now adapt to the exercise window. Range keeps the selected interval and dims other tiers.
* Fixed reconnect wicks, unrecoverable page charts, and liquidation-line colors that caused blank TradingView charts.
* Fixed **Add to Home Screen** appearing in installed PWAs. Expanded iOS Chrome installation guidance to three steps.
* Updated invitation rewards to reflect long-term rules. Added same-device and same-IP risk notices, plus invitation review statuses.
* Distinguished bonus-voucher types in blind-box results. Fixed weekly voucher counts, equity fallbacks, and unboxing modal interactions.
* Improved frozen-state displays, first-deposit copy, Burst modal triggers, and option product names.
{% endupdate %}

{% update date="2026-08-03" %}
## 1.0.8.2

* Added staged listing support for 54 stocks, ETFs, FX pairs, indices, and crypto assets. This includes AMAT, ARM, ASML, QQQ, SPY, GLD, GBP, JP225, MINIMAX, and ZHIPU. Availability follows release batches.
* Improved TradingView usability with local layout persistence, interval mapping, and position, order, TP, SL, and liquidation lines.
* Improved the TradingView data-feed and candle-session management. Charts now behave consistently across market, mobile trading, and options pages.
* Added product-introduction dialogs, adaptive Y-axes, and tier names to desktop options. Compacted the right trading panel and fixed Range-option position bubbles.
* Defaulted options to lower or nearby tiers.
* Market charts now default to the daily interval.
* Fixed option-price and payout precision, Pair payout mapping
* Fixed SEO first-screen flickering. Updated asset-information and paper-trading copy.
* Added an entry point for the tech log.
{% endupdate %}

{% update date="2026-08-01" %}
## 1.0.8.1

* Added local options paper trading for Trend, Moves, Range, Steps, Pair, and Combo. It includes virtual balances, orders, positions, and settlement.
* Added top-level market categories for crypto, stocks, indices, commodities, and FX.
* Fixed the Combo paper-trading switcher and Legal links.
* Asset search now matches English, Simplified Chinese, Traditional Chinese, and Japanese names.
* The Current Positions tab now shows open quantities.
* Added SEO-ready multilingual routes, page metadata, `robots`, and a sitemap. Crawlers and visitors without JavaScript now receive readable first-screen content.
* Added **Add to Home Screen** guidance for iOS, Android, Telegram, WeChat, and browser-native installation.
* Added a `penalty` liquidation charge to daily PnL and position-close events. Daily PnL now includes fees and liquidation costs.
* Added `total_pnl` to position-close and asset-delisting ledger broadcasts. Downstream consumers now receive the complete PnL for each action.
* Included opening fees in daily PnL when positions fully close. Unified daily-PnL cursor naming and retrieval.
* Improved WebSocket funding-fee event processing. This prevents funding-fee spikes from delaying user-ledger pushes.
* Improved Charting Library preloading, caching, and same-origin loading. This reduces first-chart load times.
{% endupdate %}

{% update date="2026-07-27" %}
## 1.0.8

* Added a daily cumulative PnL curve with zero-filled dates, business-type aggregation, and tab-specific tooltips.
* Updated the daily-PnL API to query by the `address` parameter. Added aggregation by business type.
* Added real-time daily-PnL processing, fallback ETL, and 30-day backfills for perpetuals, seven option types, and insurance.
* Added a controlled asset-delisting workflow. It stops trading, closes orders and positions, cancels insurance, completes delisting, and clears Redis state.
* Added forced settlement when option prices remain unavailable beyond the timeout. Loss settlements now trigger alerts.
* Added maximum-notional validation by leverage tier.
* Began integrating TradingView Charting Library.
* Fixed candle gaps, OHLC data overwrites, and hidden time axes in fullscreen mode.
* Improved closed-position history queries by prefetching opening fills. Removed per-row correlated subqueries, improved database throughput, and removed redundant indexes.
* Migrated Admin logging to go-kit. Logging and runtime configuration now use a unified structure.
{% endupdate %}

{% update date="2026-07-21" %}
## 1.0.7.1

* Split position margin into user margin, bonus-voucher margin, and total margin. Added voucher usage, recovery, and opening snapshots.
* Simplified deposit details in Explorer. `DEPOSIT` entries no longer show an irrelevant **To** row.
* Renamed the Explorer **From** column to **Address**. This avoids ambiguity for deposits, withdrawals, and transfers.
* Explorer no longer shows empty rows or empty JSON when Extra Data has no valid fields.
* Unified copy across YesFi products, the task center, insurance, and empty states. Corrected strategy descriptions.
* Updated the invitation page to use a unified invitation-code field. Adjusted task thresholds and progress copy.
{% endupdate %}

{% update date="2026-07-14" %}
## 1.0.7

* Added bonus vouchers. They can offset opening fees, margin, insurance premiums, losses, closing fees, and funding fees.
* Updated partial-close release order. Losses release voucher offsets first, while profits release user margin first.
* Prioritized vouchers for partial-close fees, liquidation penalties, and funding fees.
* Updated insurance quotes to use user margin. Risk, liquidation price, and position safety calculations continue to use total margin.
* Added an optional `category` field to `/exchange/symbols` for market classification and filtering.
* Added the `account` WebSocket topic. It unifies balance, position, and ledger updates, replacing the legacy ledger topic over time.
* Added ws-hub multiplex delivery, batched Oracle updates, multi-pair ticker aggregation, and symbol-based candle refreshes.
* Added in-process Beats pricing, multi-tier warnings near liquidation, and a funding-fee user feed. This reduces independent services and duplicate pushes.
* Replaced manually selected Combo assets with predefined combinations. Range now supports multiple profitable intervals. Refined tiers and payout models for Moves, Steps, and Pair.
* Upgraded charts with technical indicators, drawing tools, fullscreen mode, logarithmic scales, countdowns, second-level intervals, and mobile indicators.
* Rebuilt the signals page, desktop trading area, and options explanation flow. Improved Moves zone rulers, animations, and tier interactions.
* Added YFV Payment, YFV Receive, and formatted Extra Data in Explorer. Option details now use consistent percentages, payouts, and multi-value displays.
* Added Kraken as a market-data source, price ordering, and asset-delisting monitoring.
{% endupdate %}

{% update date="2026-06-16" %}
## 1.0.6

* Added opening, underlying, settlement, and payout delivery for Trend, Range, Combo, Pair, Moves, and Steps.
* Added the Beats short-duration product, its positions and liquidity pool, and WebSocket delivery.
* Added target-move and range configurations for Trend, Range, and Moves.
* Added mistaken-deposit recovery requests and handling, with token-recovery data structures.
* Migrated market, insurance, and Explorer list endpoints to cursor pagination.
* Unified opening prices and WebSocket spot prices to reduce Oracle source differences.
* Improved read performance for positions, orders, and transfer records.
* Retired legacy Class A FlashOption tables and settlement paths. Options now use product-level APIs.
{% endupdate %}

{% update date="2026-05-28" %}
## 1.0.5

* Added listing, order placement, position history, and settlement for Flash options.
* Added the first trading components for Trend, Beats, Combo, Pair, Steps, and Range.
* Added the unified `protections/set` endpoint for take-profit and stop-loss settings.
* Added a unified chain-configuration endpoint in Chain Sync. Core now retrieves withdrawal fees and minimum amounts dynamically at startup.
* Added account addresses to deposit-ledger broadcasts and closing transaction hashes to position responses.
* Fixed historical position mappings, TP/SL direction and full-position quantities, and frozen-balance releases after limit-order cancellation.
* Fixed empty-account insurance queries, policy filtering, and margin-adjustment message compatibility.
* Improved insurance purchasing, replacement, and quote hot paths to reduce repeated I/O.
* Hardened EIP-712 timestamp replay protection with Redis in Gateway.
* Renamed the `JPY` trading asset to `USDJPY`.
{% endupdate %}

{% update date="2026-05-25" %}
## 1.0.4

* Added Flash options, contract signals, Holdings, manual order entry, and blind-box experiences.
* Added insurance renewal replacement support to the purchase API.
* Added margin-adjustment ledger details and transaction-hash backfilling.
* Unified liquidation when account equity is less than or equal to maintenance margin. Aligned precise liquidation-price boundaries.
* Anchored insured opening quotes and execution to the same mark price. This reduces quote-snapshot differences.
* Fixed a 404 response for zero funding rates, renewal metadata, and profit-insurance payout routes.
* Flattened policy-list responses and removed redundant private endpoints with public replacements.
{% endupdate %}

{% update date="2026-05-17" %}
## 1.0.3.1

* Fixed an issue that blocked explicit full closes.
* Improved risk-control message propagation for better cross-service consistency.
* Linked profit-insurance take-profit to position protection and fixed WebSocket liquidity-index member conflicts.
{% endupdate %}

{% update date="2026-05-14" %}
## 1.0.3

* Added an opening execution-price model with base slippage and price impact.
* Added public position queries and 4-hour and 1-week candlestick intervals.
* Added a complete market page, charts, asset information, batch position adjustment and closing, a notification center, and position sharing.
* Added real-time notifications for TP, SL, liquidation, insurance, funding fees, and wallet changes.
* Added occupied funds to Explorer account summaries and multilingual names for trading pairs.
* Added a volatility-data pipeline and a platform account for bankruptcy-risk margin.
* Released margin proportionally on partial closes. Partial closes are blocked when an active policy exists.
* Fixed expired policies blocking new purchases and incorrect event types when manual closes triggered liquidation.
* Fixed profit-insurance funding-fee collection and liquidation boundaries in Explorer.
* Migrated user sessions to reduce browser-storage token exposure.
{% endupdate %}

{% update date="2026-05-07" %}
## 1.0.2

* Added a public deposit-address endpoint.
* Added mobile support, insurance queries and chat insurance cards, guest chat, and initial PWA assets.
* Requoted insured openings using persisted margin and rechecked the premium cap.
{% endupdate %}

{% update date="2026-04-29" %}
## 1.0.1

* Added order forms, floating order windows, main-account deposits and withdrawals, and balance refreshes after transfers.
* Added insurance position-reduction prompts, message badges, and social-login fixes.
* Fixed insurance-payout formulas and minimum-payout validation.
* Fixed withdrawal transaction-hash semantics and funding-rate reads in Explorer.
{% endupdate %}

{% update date="2026-04-20" %}
## 1.0.0

* Released perpetual trading, Zero Loss Insurance, and Double Profit Insurance quotes, purchases, policies, and payout previews.
* Released a weighted multi-source Oracle using Binance, OKX, Bybit, Bitget, and Hyperliquid.
* Added APIs for cancelling TP/SL and querying policy history across multiple addresses.
* Made leverage ranges configurable per trading pair. Removed the global 100× limit.
* Added support for zero opening and closing fees. Improved minimum margin, funding fees, and deposit confirmation flows.
{% endupdate %}
{% endupdates %}
