---
metaLinks:
  alternates:
    - https://app.gitbook.com/s/KiKbOTrmqLWnXHD7ZyeJ/mian-xiang-kai-fa-zhe
---

# For developers

This section explains how to integrate with YesFi through HTTP APIs and WebSocket streams.

Use it to learn authentication, signing, endpoint groups, realtime subscriptions, and error handling.

***

### What this section includes

#### HTTP API

Start with the top-level entries:

* [**API**](api/)
* [**HTTP Methods**](api/http-methods/)

Read these foundation pages first:

* [**Authentication**](api/http-methods/authentication.md)
* [**Signing**](api/http-methods/signing.md)
* [**Rate limits**](api/http-methods/rate-limits.md)

Then move into endpoint groups:

* [**Market**](api/http-methods/market/) — public market data and symbol reads
* [**Wallet & Funds**](api/http-methods/wallet-and-funds/) — deposits, withdrawals, transfers, and balances
* [**Positions & Orders**](api/http-methods/positions-and-orders/) — order placement and position actions
* [**Insurance**](api/http-methods/insurance/) — quotes, buy, renew, cancel, and policy queries
* [**Error responses**](api/http-methods/error-responses.md) — shared response schema and stable error codes

#### WebSocket Methods

Use [**WebSocket Methods**](api/websocket-methods/) for realtime data and push workflows.

It covers connection setup and topic subscriptions such as `price`, `kline`, `ticker_24h`, `ledger`, and rank streams.

***

### Recommended reading order

1. Start with [**Authentication**](api/http-methods/authentication.md) and [**Signing**](api/http-methods/signing.md).
2. Then read [**Rate limits**](api/http-methods/rate-limits.md) and [**Error responses**](api/http-methods/error-responses.md).
3. Use [**Market**](api/http-methods/market/) for public market reads.
4. Use [**Wallet & Funds**](api/http-methods/wallet-and-funds/), [**Positions & Orders**](api/http-methods/positions-and-orders/), and [**Insurance**](api/http-methods/insurance/) based on your workflow.
5. Add [**WebSocket Methods**](api/websocket-methods/) when you need realtime updates.

***

### Core principles

* Private APIs use **EIP-712** signatures tied to an **EVM address**.
* Public and private routes have different access rules.
* Clients should branch on stable error `code` values, not `message` text.

***

### Best entry points

* Building a server or bot — start with [**Authentication**](api/http-methods/authentication.md) and [**Signing**](api/http-methods/signing.md)
* Reading public market data — start with [**Market**](api/http-methods/market/)
* Building trading flows — start with [**Positions & Orders**](api/http-methods/positions-and-orders/) and [**Wallet & Funds**](api/http-methods/wallet-and-funds/)
* Building insurance flows — start with [**Insurance**](api/http-methods/insurance/)
* Streaming prices or ledger events — start with [**WebSocket Methods**](api/websocket-methods/)
