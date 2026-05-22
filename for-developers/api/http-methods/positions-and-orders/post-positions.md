---
description: Batch query public open positions.
---

# POST positions

```
POST /v1/public/exchange/positions
```

Batch query open positions by `addresses`.

#### Request body

| Field            | Type       | Required | Description                                                                                            |
| ---------------- | ---------- | -------- | ------------------------------------------------------------------------------------------------------ |
| `addresses`      | `string[]` | Yes      | Target EVM addresses. Only `addresses` is supported. Single `address` is not supported.                |
| `symbols`        | `string[]` | No       | Optional symbol filter. Raw input accepts at most 20 items. The server applies `trim + upper + dedup`. |
| `insuranceLevel` | `string`   | No       | Insurance detail level. Default is `summary`.                                                          |
| `offset`         | `integer`  | No       | Page offset. Default `0`.                                                                              |
| `limit`          | `integer`  | No       | Page size. Default `100`. Maximum `500`.                                                               |

#### Request rules

* `addresses` raw input accepts at most 20 items.
* The server normalizes addresses by EVM rules, deduplicates them, and converts them to lowercase.
* If `insuranceLevel` is omitted, the server uses `summary`.

#### Response

```json
{
  "success": true,
  "data": {
    "positions": [
      {
        "address": "0x1234567890abcdef1234567890abcdef12345678",
        "avg_close_price": null,
        "closed_quantity": "0",
        "entry_price": "62000.00",
        "insurance": {
          "policies": [
            {
              "closureReason": "",
              "displayStatus": "active",
              "expireAt": 1716604800000,
              "insuranceType": "REVIVAL",
              "lifecycleStatus": "active",
              "paymentStatus": "paid",
              "payoutAmount": "500.00",
              "payoutPercent": 100,
              "policyId": "a1b2c3d4-e5f6-7890-abcd-ef1234567890",
              "premium": "12.50",
              "replacementHint": "",
              "startAt": 1716000000000,
              "status": "active",
              "triggerPercent": 10,
              "triggerPrice": "60000.00",
              "tx_hash": "0xabc..."
            }
          ]
        },
        "margin": "3100.00",
        "mark": "63500.00",
        "mark_stale": false,
        "opened_at": "2026-05-20T10:00:00.123456789Z",
        "opening_fee": "1.24",
        "positionUid": "9d3eb3f8-85af-42c5-8aee-56a2b86516f6",
        "realized_pnl": "0",
        "side": "buy",
        "size": "0.5000",
        "symbol": "BTC-USD",
        "unrealized_pnl": "750.00"
      }
    ],
    "total": 1
  }
}
```

#### Response fields

| Field                             | Type       | Description                                                 |
| --------------------------------- | ---------- | ----------------------------------------------------------- |
| `success`                         | `boolean`  | Request result.                                             |
| `data`                            | `object`   | Response payload.                                           |
| `data.positions`                  | `object[]` | Matched open positions.                                     |
| `data.positions[].address`        | `string`   | Position owner address.                                     |
| `data.positions[].positionUid`    | `string`   | Position id.                                                |
| `data.positions[].symbol`         | `string`   | Full market symbol.                                         |
| `data.positions[].side`           | `string`   | Position side.                                              |
| `data.positions[].size`           | `string`   | Position size as decimal string.                            |
| `data.positions[].margin`         | `string`   | Position margin as decimal string.                          |
| `data.positions[].entry_price`    | `string`   | Entry price as decimal string.                              |
| `data.positions[].mark`           | `string`   | Current mark price as decimal string.                       |
| `data.positions[].mark_stale`     | `boolean`  | Whether the mark price is stale.                            |
| `data.positions[].unrealized_pnl` | `string`   | Unrealized PnL as decimal string.                           |
| `data.positions[].realized_pnl`   | `string`   | Realized PnL as decimal string.                             |
| `data.positions[].opened_at`      | `string`   | Position open time in UTC.                                  |
| `data.positions[].opening_fee`    | `string`   | Opening fee as decimal string.                              |
| `data.positions[].insurance`      | `object`   | Insurance summary or detail, depending on `insuranceLevel`. |
| `data.total`                      | `integer`  | Total matches before pagination.                            |

#### Errors

* `400` — Invalid request parameters.
* `503` — Service unavailable.
