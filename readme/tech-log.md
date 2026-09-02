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

We are thrilled to announce that from now until **September 15, 24:00 (UTC)**, YesFi.com is officially entering its Beta Testing phase!

During this period, we will be stress-testing our platform—including **Quick Options**, **Signal Feed**, and the **Matching Engine**—under live market-making conditions. To ensure absolute system security and financial integrity for our upcoming Mainnet Launch, please review the following rules:

* **Trading Assets & PnL Reset**: All open positions, as well as unrealized and realized PnL accumulated during the Beta period, could be cleared and reset at any time before **September 15, 24:00 (UTC)**. Your initial deposited principal remains 100% safe and unaffected, and can be withdrawn at any time.
* **Permanently Retained Rewards**: All **Membership Levels** and **Y Points** earned during the Beta phase will be **100% permanently retained**! As a tribute to our early Genesis contributors, your status and points will directly map to your weekly reward distribution (Option & Insurance Vouchers) weight upon the official Mainnet Launch.

Thank you to every pioneer evolving with YesFi.

**One Yes, Trade All.**
{% endhint %}

{% updates format="full" %}
{% update date="2026-09-02" %}
## 1.1.1.1

* Failed sign-ins and wallet signatures now show lightweight toast messages. Signature-confirmation dialogs now stay above page elements.
* **MAX** now uses the full available balance for withdrawals and internal transfers. Particle migrations now transfer only available balances. Tiny amounts no longer trigger migrations.
* Failed internal transfers now show the specific reason. Transfer copy no longer promises instant delivery. Processing states now use clearer pill labels.
* Mobile **Moves** and **Trend** options now highlight maximum loss in red. **Combo** and **Pair** option prices and charts now stay in sync more promptly.
* One-second option candlesticks now continue correctly after navigation. Candle closes are more accurate. Winning settlements no longer show misleading voucher-offset copy.
* Paper trading no longer applies real checkout vouchers. Market funding rates now prioritize real-time push values.
* Renamed **Blind Box** to **Reward Box**. Membership cards and Y Points guidance are clearer. New-user guidance now focuses on learning rather than gamification.
* Insurance position cards are more compact. Amounts now use a consistent `$` prefix. Empty hashes and negative values are easier to read.
* **Add to Home Screen** now supports more Android browsers, iOS Safari, and iOS Chrome. The OKX in-app browser no longer shows an installation prompt. iOS onboarding for Options and Perpetuals now avoids crashes and scrolling issues.
* Improved **Beats** odds pricing. Near-term grid volatility better reflects 60-second markets. Extreme conditions now reduce anomalous and inverted odds.
{% endupdate %}

{% update date="2026-08-28" %}
## 1.1.1

* Added **Telegram** social login. It can now be used as the primary sign-in method.
* Standardized option directions as **Buy Call** and **Buy Put**. Signal prices now animate more clearly and show 24-hour changes.
* Improved tab readability on Assets and Options. The selected tab now centers automatically. Perpetual trading now shows the funding rate compactly below the latest price.
* Added a dedicated reward category in the notification center. Refined reward templates so they do not mix with operational announcements.
* Improved Explorer deposit recognition and address parsing. Deposit and withdrawal details now include the chain and on-chain transaction hash.
* Pair and Combo options now notify only listed combinations. Delisted combinations no longer send stale odds. Notifications now subscribe precisely by catalog, reducing unnecessary broadcasts.
* Added first-time trading guidance for Options and Perpetuals. Signed-in users see a welcome guide on their first visit. Select **How to trade?** to replay it.
* Paper-trading completion now prompts visitors to connect a wallet. Orders and positions now show premiums and payouts after voucher offsets.
* Settled positions now use **Payout** consistently. Transfer records now show their processing status directly. Pending states no longer use misleading color blocks.
* Balances now refresh promptly for both parties after withdrawals and internal transfers. Deployment settings can now configure the footer contact email.
* High-risk strategy triggers can now reduce positions automatically. Manual per-position intervention is no longer required.
* Insurance quotes now estimate implied volatility with the on-chain oracle. Pricing remains more stable during extreme markets.
{% endupdate %}

{% update date="2026-08-25" %}
## 1.1.0.2

* Removed the Splash animation. The app now opens directly to the main interface.
* Desktop **Moves** positions now restore instantly. **Moves** volatility cards now show their tier ranges.
* Returning from market details now restores the previously selected tab.
* The mobile Market tab now shows a red dot when recent signals exist.
* Desktop option candlestick previews no longer cover charts. Navigation now includes a BETA badge.
* Removed the duplicate divider from paper-trading blank tickets. Aligned target-range typography.
* Adjusted selectable image placement on membership-level cards. Improved the V0 display for users below V1.
* Revised and proofread membership benefits and task copy.
* Fixed option short titles, narrow-screen Combo list truncation, and the English **Add to Home Screen** title. Updated the SEO manifest.
* Replaced the footer Discord link with GitBook. Fixed several mobile notification-inbox display issues.
{% endupdate %}

{% update date="2026-08-21" %}
## 1.1.0.1

* Homepage campaign banners now vary for signed-in and signed-out visitors.
* WebSocket compact frames speed up market, odds, and leaderboard pushes. They use less bandwidth and improve stability on weak connections.
* Beats odds now refresh immediately with market changes. Quiet markets and nearby slots now receive more appropriate prices.
* Steps Quick Options now support tiered two-, three-, and five-minute periods. Quotes respond more flexibly during high volatility.
* Beats-option settlements now complete faster. Peak trading periods are less likely to cause settlement backlogs.
* Zero Loss and Double Profit Insurance now process quotes, openings, and closes in parallel. Order waits are shorter.
* Fixed an issue in the market service BBO index calculation.
* Explorer address-operation charts now group low-share types under **Other**. Quick Options copy now uses **Quick Option Open / Exercise** consistently.
* Reward popups now arrive sooner after earning points, vouchers, or coupons. Settlements automatically claim eligible rewards.
* The task center now groups tasks by check-in, trading, invitation, and other types. Each reward uses its matching display style.
* Holiday and birthday benefits now appear separately from daily tasks.
* Reward popups now expire after a reasonable period. Stale reminders, including **Daily Trading Complete**, no longer reappear.
* Missed notifications are automatically resent. Expired records are cleared.
* Improved notification-center line wrapping and benefit displays. Notification-detail external links now use HTTPS.
* Signed-out users no longer see new-user reward guidance on Assets. The page defaults to insurance information and prompts sign-in on other tabs.
* Second-level candlesticks no longer connect opening prices across gaps.
* Fixed PNG exports bug for position and insurance share images.
* Active insurance policies no longer show a redundant **Purchased** label. Improved text contrast.
* Benefit box records now load with pagination. Homepage operations-bar copy can now be selected and copied.
{% endupdate %}

{% update date="2026-08-18" %}
## 1.1.0

* Migrated social login and signing from Particle to Eocene. Embedded wallets continue to use Particle ConnectKit.
* Added a Particle-to-Eocene asset migration flow. Fixed wallet-address rendering and tamper protection on the migration page. Updated the footer.
* Updated Steps-option settlement to use the European-style expiry price. Tiers now use the expiry close against the entry price. Opening odds remain fixed. Intraperiod highs no longer lock a higher tier.
* Prevented Beats-option price updates from rerendering the full React page. This reduces stutter during high-frequency quotes.
* Tightened option quote slots for desktop. Price changes now use red and green backgrounds. Asset-selector hover no longer covers prices. Transparent logos now have white backgrounds.
* Exported share images in the active theme. Preview and export now match. Copy-button icons no longer shift with label changes.
* Changed desktop dialogs from bottom sheets to centered modals.
* Defaulted two-minute option charts to a five-second candlestick interval.
* Removed exercise income from the Moves-option position table. Position tables now scroll horizontally. Fixed empty transaction-hash displays.
* Android **Add to Home Screen** now shows a guide image before the system prompt. Added a Service Worker to meet installation requirements.
* Updated the iOS home-screen banner to use **Add**. Raised the insurance-calculator asset selector to prevent overlap.
{% endupdate %}

{% update date="2026-08-14" %}
## 1.0.9.1

* Added **On-chain Withdrawal** and **Internal Transfer** tabs to the withdrawal modal. Users can now transfer USDC to another platform user's address instantly, with no on-chain fee.
* Added real-time recipient validation for platform account addresses. Clear messages now cover unregistered accounts, system errors, and self-transfers.
* Rebuilt the internal account-transfer modal. Separate desktop and mobile components improve account selection and amount entry.
* Standardized internal-transfer copy as **Transfer**. Added clearer guidance for recipient addresses, main accounts, and the USDC contract.
* Improved counterparty address displays in transaction lists and details. Deposits, withdrawals, transfers, and insurance are now identified more accurately.
* Added a explorer back button, inline in-app links, and safe-area support. Fixed mobile header overlap and navigation issues.
* Transaction-detail **Interaction With** now supports protocol addresses and readable names. Refined the operation-distribution donut chart.
* Added operational announcements to the notification center. Announcements support their own category, detail pages, and controlled deep links.
* Excluded insurance from daily PnL calculations. Removed historical insurance summary rows.
* Improved paper trading with Moves volatility-tier previews and candlestick watermarks. Fixed Beats boundary logic, second-level candlestick sampling, grid proportions, and header entry jitter.
* Fixed Moves volatility-tier percentages and bar heights.
{% endupdate %}

{% update date="2026-08-10" %}
## 1.0.9

* Integrated the YesFi Block Explorer into the main site. Search transaction hashes, wallet addresses, and block heights without leaving YesFi.
* Added latest transactions, automatic refresh, business-type filters, and cursor pagination to the Explorer home page.
* Added transaction details with natural-language descriptions for opening and closing positions, transfers, deposits, withdrawals, funding fees, insurance, and option settlements.
* Added methods, parameters, display events, and asset flows to transaction details. Also added price labels, fees, PnL, penalties, premiums, payouts, and other key fields.
* Added address details with account balances, transaction counts, first and latest activity, and a 30-day operation-type distribution.
* Added block details with synthetic block and parent hashes, a fixed status, configured validator names, distinct traders, recorded amounts, and operation distribution. These fields do not represent L1 consensus data.
* Added Explorer API endpoints for block overviews, Action Mix, address overviews, address operation statistics, and transaction display projections. Business groupings are now unified.
* Added validation for Explorer search input, block-height, cursor, and business-filter parameters. Added display-address and validator configuration. Invalid configuration now fails at startup.
* Added a restricted Explorer reverse proxy and route SEO configuration to the main site. Transaction-hash links now open in-app by default.
* Fixed Explorer amount formatting, transaction narratives, and component structure. Improved Facebook sharing previews.
{% endupdate %}

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
