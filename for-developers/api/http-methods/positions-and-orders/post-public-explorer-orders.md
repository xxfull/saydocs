---
description: listPublic order list by address(es).
metaLinks:
  alternates:
    - >-
      https://app.gitbook.com/s/KiKbOTrmqLWnXHD7ZyeJ/mian-xiang-kai-fa-zhe/api/http-fang-fa/ding-dan-yu-cang-wei/cha-xun-ding-dan-lie-biao-post-publicexplorerorders
---

# POST orders/list

```
POST /v1/public/exchange/orders/list
```

#### Request Body

| Field       | Type       | Required | Description                                                                                 |
| ----------- | ---------- | -------- | ------------------------------------------------------------------------------------------- |
| `address`   | string     | No       | Required in single-address mode. Target EVM address, lowercase `0x` + 40 hex chars.         |
| `addresses` | string \[] | No       | Multi-address mode; when non-empty, `address` is ignored. At most 20 addresses after dedup. |
| `endTime`   | integer    | No       | End time (Unix milliseconds, inclusive).                                                    |
| `limit`     | integer    | No       | Max rows to return. `0` uses the server default page limit.                                 |
| `offset`    | integer    | No       | Page offset starting at 0.                                                                  |
| `startTime` | integer    | No       | Start time (Unix milliseconds, inclusive).                                                  |
| `status`    |            | No       | Order status filter. Single string or string array.                                         |
| `symbols`   | string \[] | No       | Batch filter for symbols (max 20).                                                          |
| `timeField` | string     | No       | Time field for filtering; default `created_at`.                                             |
| `type`      |            | No       | Order type filter. Single string or string array.                                           |

#### Response

```json
{
  "success": true,
  "data": {
    "orders": [],
    "total": 0
  }
}
```

#### Response Fields

| Field                                | Type       | Description                                                                                                                                                |
| ------------------------------------ | ---------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `data`                               | object     |                                                                                                                                                            |
| `data.orders`                        | object \[] |                                                                                                                                                            |
| `data.orders.address`                | string     | Present on each order only for multi-address `/orders` when at least two addresses were requested; EVM address owning the order (lowercase `0x` + 40 hex). |
| `data.orders.created_at`             | string     | Order creation time, UTC.                                                                                                                                  |
| `data.orders.executed_at`            | string     | Fill time, UTC.                                                                                                                                            |
| `data.orders.execution_price`        | string     | Execution price as a decimal string; truncated per `pxDecimals`.                                                                                           |
| `data.orders.execution_slippage_bps` | string     | Slippage used for this execution, in bps, as a decimal string.                                                                                             |
| `data.orders.filled_quantity`        | string     | Filled quantity as a decimal string; truncated per `szDecimals`.                                                                                           |
| `data.orders.limit_price`            | string     | Limit price when applicable, as a decimal string; truncated per `pxDecimals`.                                                                              |
| `data.orders.mark_price`             | string     | Mark price snapshot at execution, as a decimal string; truncated per `pxDecimals`.                                                                         |
| `data.orders.order_id`               | string     | Order id.                                                                                                                                                  |
| `data.orders.order_type`             | string     | Order type.                                                                                                                                                |
| `data.orders.position_uid`           | string     | `position_uid` of the linked position; only when the order is tied to a position.                                                                          |
| `data.orders.quantity`               | string     | Original order quantity as a decimal string; truncated per `szDecimals`.                                                                                   |
| `data.orders.reason`                 | string     | Reason the order filled or closed; e.g. user, take\_profit, stop\_loss, insurance, adl, liquidation.                                                       |
| `data.orders.remaining_quantity`     | string     | Result of `quantity - filled_quantity`, as a decimal string; truncated per `szDecimals`.                                                                   |
| `data.orders.reserve_remaining`      | string     | Remaining reserve, as a decimal string; truncated to 8 decimals in quote asset.                                                                            |
| `data.orders.side`                   | string     | Order side.                                                                                                                                                |
| `data.orders.status`                 | string     | Current order status.                                                                                                                                      |
| `data.orders.stop_loss_price`        | string     | Stop-loss trigger from the parent order or historical, as a decimal string; truncated per `pxDecimals`.                                                    |
| `data.orders.stop_loss_quantity`     | string     | Stop-loss quantity from the parent order, as a decimal string; truncated per `szDecimals`.                                                                 |
| `data.orders.symbol`                 | string     | Full market symbol.                                                                                                                                        |
| `data.orders.take_profit_price`      | string     | Take-profit trigger from the parent order or historical, as a decimal string; truncated per `pxDecimals`.                                                  |
| `data.orders.take_profit_quantity`   | string     | Take-profit quantity from the parent order, as a decimal string; truncated per `szDecimals`.                                                               |
| `data.orders.trigger_price`          | string     | Historical trigger price for conditional orders, as a decimal string; truncated per `pxDecimals`; legacy field.                                            |
| `data.orders.tx_hash`                | string     | Ledger tx hash for the first fill, derived from its `ledger_tx_id`; omitted if no fills.                                                                   |
| `data.orders.updated_at`             | string     | Last update time, UTC.                                                                                                                                     |
| `data.total`                         | integer    | Total count for the current filter (not limited by pagination).                                                                                            |
| `success`                            | boolean    |                                                                                                                                                            |
