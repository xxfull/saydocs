---
hidden: true
---

# POST positions/history

Query flash option position history for one or more wallet addresses.

* Multi-address mode lowercases and deduplicates EVM addresses, **max 10**. When at least two addresses are requested, each `items[]` row includes an `address` field.

```
POST /v1/public/flashoption/positions/history
```

#### Request Body

| Field               | Type      | Required | Description                                                                                   |
| ------------------- | --------- | -------- | --------------------------------------------------------------------------------------------- |
| `address`           | string    | No\*     | Single-address query; also compatible with `X-Address`.                                       |
| `addresses`         | string\[] | No       | Multi-address query; when non-empty, overrides `address` and `X-Address`; max 10 after dedup. |
| `status`            | string    | No       | Position status filter; see enum below.                                                       |
| `symbol`            | string    | No       | Symbol filter.                                                                                |
| `touch_mode`        | string    | No       | Direction filter: `long`, `short`, or `breakout`.                                             |
| `product_id`        | string    | No       | Product ID filter.                                                                            |
| `page_size`         | integer   | No       | Page size; default 20, max 100.                                                               |
| `cursor_created_at` | integer   | No       | From previous page `next_cursor.created_at`.                                                  |
| `cursor_id`         | string    | No       | From previous page `next_cursor.id` (UUID).                                                   |

\* One of `address`, `addresses`, or `X-Address` is required.

**Allowed `status` values**

| Value               | Meaning                          |
| ------------------- | -------------------------------- |
| `open`              | Holding                          |
| `settling`          | Settlement in progress           |
| `won`               | Won and paid out                 |
| `lost`              | Lost                             |
| `settlement_failed` | Settlement failed; pending retry |
| `cancelled`         | Cancelled                        |
| `refunded`          | Refunded                         |

#### Response

```json
{
  "success": true,
  "data": {
    "items": [
      {
        "address": "0x658ef23ceca717a14cddb3689b96014148992825",
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
        "actual_settled_at": 1779870300123,
        "settlement_price": "68120.5",
        "status": "won",
        "payout_amount": "18",
        "tx_hash": "0x1111111111111111111111111111111111111111111111111111111111111111",
        "settlement_tx_hash": "0x2222222222222222222222222222222222222222222222222222222222222222",
        "client_order_id": "0x658ef23ceca717a14cddb3689b96014148992825-100000001-001",
        "created_at": 1779870012500
      }
    ],
    "page_size": 20,
    "has_more": true,
    "next_cursor": {
      "created_at": 1779870012500,
      "id": "019704dd-6c80-7000-8000-000000000001"
    }
  }
}
```

#### Response Fields

| Field                           | Type      | Description                                       |
| ------------------------------- | --------- | ------------------------------------------------- |
| `data.items`                    | object\[] | Position records.                                 |
| `data.items.address`            | string    | Present in multi-address queries (≥2 addresses).  |
| `data.items.product_id`         | string    | Product ID.                                       |
| `data.items.symbol`             | string    | Trading pair.                                     |
| `data.items.touch_mode`         | string    | Product direction.                                |
| `data.items.shares`             | integer   | Share count.                                      |
| `data.items.price_per_share`    | string    | Premium per share.                                |
| `data.items.premium_amount`     | string    | Total premium.                                    |
| `data.items.odds`               | string    | Payout multiplier.                                |
| `data.items.start_price`        | string    | Product reference start price.                    |
| `data.items.opened_price`       | string    | Mark price at open.                               |
| `data.items.opened_price_ts`    | integer   | Open price timestamp.                             |
| `data.items.started_at`         | integer   | Product start time.                               |
| `data.items.settled_at`         | integer   | Scheduled settlement time.                        |
| `data.items.actual_settled_at`  | integer   | Actual settlement time; `0` if not yet settled.   |
| `data.items.settlement_price`   | string    | Settlement mark price; omitted before settlement. |
| `data.items.status`             | string    | Position status; see enum above.                  |
| `data.items.payout_amount`      | string    | Payout amount; usually `0` before settlement.     |
| `data.items.tx_hash`            | string    | Open ledger tx hash.                              |
| `data.items.settlement_tx_hash` | string    | Settlement ledger tx hash.                        |
| `data.items.client_order_id`    | string    | Client idempotency key when present.              |
| `data.items.created_at`         | integer   | Position creation time.                           |
| `data.page_size`                | integer   | Page size for this response.                      |
| `data.has_more`                 | boolean   | Whether another page exists.                      |
| `data.next_cursor`              | object    | Next-page cursor; may be `null`.                  |
| `data.next_cursor.created_at`   | integer   | Cursor timestamp.                                 |
| `data.next_cursor.id`           | string    | Cursor position ID (UUID).                        |

#### Errors

| HTTP | Code                            | Meaning                             |
| ---- | ------------------------------- | ----------------------------------- |
| 400  | `LITEOPTION_ADDRESS_REQUIRED`   | No query address provided.          |
| 400  | `LITEOPTION_INVALID_ADDRESS`    | Invalid address format.             |
| 400  | `LITEOPTION_TOO_MANY_ADDRESSES` | More than 10 addresses after dedup. |
| 400  | `LITEOPTION_INVALID_STATUS`     | Invalid `status`.                   |
| 400  | `LITEOPTION_INVALID_TOUCH_MODE` | Invalid `touch_mode`.               |
| 400  | `LITEOPTION_INVALID_CURSOR`     | Invalid cursor parameters.          |
| 404  | `LITEOPTION_NOT_FOUND`          | Resource not found.                 |
| 500  | `LITEOPTION_INTERNAL`           | Internal server error.              |
