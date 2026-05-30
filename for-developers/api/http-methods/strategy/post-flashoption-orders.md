# POST flashoption/orders

Buy shares of an active flash option product and create an **open** user position.

```
POST /v1/private/flashoption/orders
```

The server validates account existence, product active / started / not settled, remaining shares, usable mark price within `available_distance`, and sufficient USDC balance. The write is **transactional**: sold shares, balance, position, ledger entries, and outbox commit in one transaction.

`client_order_id` is optional. When provided it acts as a **per-user idempotency key**; duplicates return the existing position. Without it, retries after timeout may create a new order.

#### Request Body

| Field             | Type    | Required | Description                               |
| ----------------- | ------- | -------- | ----------------------------------------- |
| `product_id`      | string  | Yes      | Product ID to buy.                        |
| `shares`          | integer | Yes      | Number of shares; minimum 1.              |
| `client_order_id` | string  | No       | Optional idempotency key for the account. |

#### Response

```json
{
  "success": true,
  "data": {
    "position": {
      "product_id": "100000001",
      "symbol": "BTC-USDT",
      "touch_mode": "long",
      "shares": 10,
      "price_per_share": "1",
      "premium_amount": "10",
      "odds": "1.8",
      "start_price": "67000",
      "opened_price": "67120.5",
      "opened_price_ts": 1779870012345,
      "started_at": 1779870000000,
      "settled_at": 1779870300000,
      "status": "open",
      "tx_hash": "0x1111111111111111111111111111111111111111111111111111111111111111",
      "client_order_id": "0x658ef23ceca717a14cddb3689b96014148992825-100000001-001",
      "created_at": 1779870012500
    }
  }
}
```

#### Response Fields — `data.position`

| Field             | Type    | Description                                                                              |
| ----------------- | ------- | ---------------------------------------------------------------------------------------- |
| `product_id`      | string  | Product ID.                                                                              |
| `symbol`          | string  | Trading pair.                                                                            |
| `touch_mode`      | string  | `long`, `short`, or `breakout`.                                                          |
| `shares`          | integer | Shares purchased.                                                                        |
| `price_per_share` | string  | Premium per share.                                                                       |
| `premium_amount`  | string  | Total premium (`shares × price_per_share`).                                              |
| `odds`            | string  | Payout multiplier.                                                                       |
| `start_price`     | string  | Product reference start price.                                                           |
| `opened_price`    | string  | Mark price snapshot at open.                                                             |
| `opened_price_ts` | integer | Open price timestamp (Unix ms).                                                          |
| `started_at`      | integer | Product start time (Unix ms).                                                            |
| `settled_at`      | integer | Scheduled settlement time (Unix ms).                                                     |
| `status`          | string  | New positions are `open`.                                                                |
| `tx_hash`         | string  | SHA3-256 hash of internal ledger tx id (`0x` + 64 hex); raw ledger tx id is not exposed. |
| `client_order_id` | string  | Returned when provided in the request.                                                   |
| `created_at`      | integer | Position creation time (Unix ms).                                                        |

#### Errors

| HTTP | Code                                    | Meaning                                       |
| ---- | --------------------------------------- | --------------------------------------------- |
| 401  | `LITEOPTION_UNAUTHORIZED`               | Missing auth or gateway EIP-712 failure.      |
| 404  | `LITEOPTION_NOT_FOUND`                  | Account or product not found.                 |
| 409  | `LITEOPTION_PRODUCT_NOT_ACTIVE`         | Product is not active.                        |
| 409  | `LITEOPTION_PRODUCT_NOT_STARTED`        | Product has not started.                      |
| 409  | `LITEOPTION_PRODUCT_EXPIRED`            | Product expired or already settled.           |
| 409  | `LITEOPTION_PRODUCT_SOLD_OUT`           | Insufficient remaining shares.                |
| 409  | `LITEOPTION_PRODUCT_PRICE_OUT_OF_RANGE` | Mark price outside purchasable distance.      |
| 409  | `LITEOPTION_PRODUCT_INVALID_CONFIG`     | Invalid product configuration.                |
| 409  | `LITEOPTION_INSUFFICIENT_FUNDS`         | Insufficient USDC balance.                    |
| 503  | `LITEOPTION_PRICE_UNAVAILABLE`          | Oracle mark price unavailable.                |
| 503  | `LITEOPTION_PRICE_SYMBOL_MISMATCH`      | Price snapshot symbol does not match product. |
| 500  | `LITEOPTION_INTERNAL`                   | Internal server error.                        |
