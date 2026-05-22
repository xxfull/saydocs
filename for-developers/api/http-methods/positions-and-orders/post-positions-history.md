---
description: Query public closed positions.
---

# POST positions/history

```
POST /v1/public/exchange/positions/history
```

Query closed positions by `address` or `addresses`.

#### Request body

| Field       | Type       | Required | Description                                                     |
| ----------- | ---------- | -------- | --------------------------------------------------------------- |
| `address`   | `string`   | No       | Single target EVM address.                                      |
| `addresses` | `string[]` | No       | Batch target EVM addresses. Raw input accepts at most 20 items. |

#### Request rules

* Use `address` or `addresses`.
* `addresses` raw input accepts at most 20 items.

#### Response

```json
{
  "success": true,
  "data": {
    "positions": [
      {
        "address": "0x1234567890abcdef1234567890abcdef12345678",
        "avg_close_price": "63360.00",
        "close_reason": "user_close",
        "closed_at": "2026-05-20T15:30:00Z",
        "closed_quantity": "0.5000",
        "entry_price": "62000.00",
        "margin": "3100.00",
        "opened_at": "2026-05-18T08:00:00Z",
        "opening_fee": "1.24",
        "position_uid": "9d3eb3f8-85af-42c5-8aee-56a2b86516f6",
        "realized_pnl": "680.00",
        "side": "buy",
        "size": "0.5000",
        "symbol": "BTC-USD"
      }
    ],
    "total": 1
  }
}
```

#### Response fields

| Field                              | Type       | Description                            |
| ---------------------------------- | ---------- | -------------------------------------- |
| `success`                          | `boolean`  | Request result.                        |
| `data`                             | `object`   | Response payload.                      |
| `data.positions`                   | `object[]` | Matched closed positions.              |
| `data.positions[].address`         | `string`   | Position owner address.                |
| `data.positions[].position_uid`    | `string`   | Position id.                           |
| `data.positions[].symbol`          | `string`   | Full market symbol.                    |
| `data.positions[].side`            | `string`   | Position side.                         |
| `data.positions[].size`            | `string`   | Position size as decimal string.       |
| `data.positions[].entry_price`     | `string`   | Entry price as decimal string.         |
| `data.positions[].avg_close_price` | `string`   | Average close price as decimal string. |
| `data.positions[].closed_quantity` | `string`   | Closed quantity as decimal string.     |
| `data.positions[].margin`          | `string`   | Position margin as decimal string.     |
| `data.positions[].realized_pnl`    | `string`   | Realized PnL as decimal string.        |
| `data.positions[].opened_at`       | `string`   | Position open time in UTC.             |
| `data.positions[].closed_at`       | `string`   | Position close time in UTC.            |
| `data.positions[].close_reason`    | `string`   | Close reason.                          |
| `data.total`                       | `integer`  | Total matches before pagination.       |

`insurance_level=full` adds `insurance.policies` in each closed position.

#### Errors

* `400` — Invalid request parameters.
* `503` — Service unavailable.
