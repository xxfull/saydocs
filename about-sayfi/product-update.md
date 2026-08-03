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

{% updates format="full" %}
{% update date="2026-08-03" %}
## 1.0.8

* Added a local options paper-trading environment for Trend, Moves, Range, Steps, Pair, and Combo. It includes a virtual balance, order placement, and settlement.
* Added **Add to Home Screen** guidance for iOS, Android, Telegram, and WeChat.
* Added SEO-ready multilingual routes, page metadata, `robots`, and a sitemap. Crawlers and visitors without JavaScript now receive readable first-screen content.
* Added top-level market categories for crypto, stocks, indices, commodities, and FX. Asset search now matches English, Simplified Chinese, Traditional Chinese, and Japanese names.
* Added a daily cumulative PnL curve with zero-filled dates, business-type aggregation, and tab-specific guidance.
* Added staged listing support for 54 stocks, ETFs, FX pairs, indices, and crypto assets. Assets become available gradually by release batch.
* Added a controlled asset-delisting workflow. It stops new trades, cancels related orders and insurance, closes positions, and clears linked state.
* Added maximum-notional validation by leverage tier. Oversized market and limit orders now return clearer errors.
* Began migrating to the TradingView charting engine. The first release saves layouts locally and shows position, order, TP, SL, and liquidation lines.
* Improved same-origin chart loading and prefetching. Fixed candle gaps, OHLC data overwrites, and hidden time axes in fullscreen mode.
* Improved the desktop options experience with product introductions, adaptive Y-axes, compact trade panels, and clearer tier names.
* Improved processing throughput across Admin, Explorer, and WebSocket events.
{% endupdate %}

{% update date="2026-07-22" %}
## 1.0.7

* Added bonus vouchers. They can offset opening fees, margin, insurance premiums, losses, closing fees, and funding fees.
* Split position margin into user margin, bonus-voucher margin, and total margin. Added voucher usage and recovery snapshots.
* Updated partial-close release order. Losses release voucher offsets first, while profits release user margin first.
* Updated insurance quotes to use user margin. Risk and liquidation calculations continue to use total margin.
* Added the `account` WebSocket topic, ws-hub multiplex delivery, batched Oracle updates, and multi-pair ticker aggregation.
* Added in-process Beats pricing and multi-tier warnings near liquidation. This reduces independent services and duplicate pushes.
* Replaced manually selected Combo assets with predefined combinations. Refined tiers and payout models for Range, Moves, Steps, and Pair.
* Upgraded charts with technical indicators, drawing tools, fullscreen mode, logarithmic scales, countdowns, and second-level intervals.
* Rebuilt the signals page, desktop trading area, and options explanation flow. Improved Moves zone animations and tier interactions.
* Added YFV Payment, YFV Receive, and formatted Extra Data in Explorer. Option details now use consistent percentages, payouts, and multi-value displays.
* Fixed incorrect signs on non-transfer amounts, redundant deposit details, and unclear address column labels in Explorer.
* Fixed withdrawal records, duplicate `data` responses, empty account addresses, route prefixes, and buy-position liquidation prices.
* Fixed recipient addresses in transfer pushes and subscription or payout issues for Combo, Pair, Moves, and Range.
* Added Kraken as a market-data source, price ordering, and delisting monitoring.
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
