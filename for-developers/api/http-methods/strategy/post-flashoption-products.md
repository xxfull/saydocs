# POST flashoption/products

List **active** flash option products that have not yet settled.

```
POST /v1/public/flashoption/products
```

#### Request Body

* Request body may be empty `{}`. When filters are provided, they are combined with **AND** logic.

| Field        | Type   | Required | Description                                                              |
| ------------ | ------ | -------- | ------------------------------------------------------------------------ |
| `id`         | string | No       | Exact product ID filter.                                                 |
| `symbol`     | string | No       | Symbol filter; server normalizes to uppercase, e.g. `BTC-USDT`.          |
| `touch_mode` | string | No       | Direction filter: `long`, `short`, or `breakout`; empty means no filter. |

#### Response

```json
{
  "success": true,
  "data": {
    "items": [
      {
        "id": "100000001",
        "symbol": "BTC-USDT",
        "touch_mode": "long",
        "upper_barrier": "68000",
        "start_price": "67000",
        "started_at": 1779870000000,
        "settled_at": 1779870300000,
        "duration_sec": 300,
        "odds": "1.8",
        "max_shares": 1000,
        "sold_shares": 12,
        "price_per_share": "1",
        "available_distance": "50",
        "mark_price": "67120.5",
        "status": "active"
      }
    ]
  }
}
```

#### Response Fields — `data.items[]`

| Field                | Type    | Description                                                       |
| -------------------- | ------- | ----------------------------------------------------------------- |
| `id`                 | string  | Product ID.                                                       |
| `symbol`             | string  | Full symbol, e.g. `BTC-USDT`.                                     |
| `touch_mode`         | string  | `long`, `short`, or `breakout`.                                   |
| `upper_barrier`      | string  | Upper barrier for `long` / `breakout`; may be omitted otherwise.  |
| `lower_barrier`      | string  | Lower barrier for `short` / `breakout`; may be omitted otherwise. |
| `start_price`        | string  | Product reference start price (decimal string).                   |
| `started_at`         | integer | Product start time (Unix ms).                                     |
| `settled_at`         | integer | Scheduled settlement time (Unix ms).                              |
| `duration_sec`       | integer | Product duration in seconds.                                      |
| `odds`               | string  | Payout multiplier (decimal string).                               |
| `max_shares`         | integer | Maximum sellable shares.                                          |
| `sold_shares`        | integer | Shares already sold.                                              |
| `price_per_share`    | string  | Premium per share (decimal string).                               |
| `available_distance` | string  | Max distance from barrier still purchasable at current mark.      |
| `mark_price`         | string  | Current oracle mark price (decimal string).                       |
| `status`             | string  | Always `active` in this list.                                     |

#### Errors

| HTTP | Code                            | Meaning                                                         |
| ---- | ------------------------------- | --------------------------------------------------------------- |
| 400  | `LITEOPTION_INVALID_TOUCH_MODE` | Invalid `touch_mode`.                                           |
| 503  | `LITEOPTION_PRICE_UNAVAILABLE`  | Mark price missing, stale, or unparseable for a product symbol. |
| 500  | `LITEOPTION_INTERNAL`           | Internal server error.                                          |
