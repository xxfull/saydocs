---
description: Order detail with fills.
metaLinks:
  alternates:
    - >-
      https://app.gitbook.com/s/KiKbOTrmqLWnXHD7ZyeJ/mian-xiang-kai-fa-zhe/api/http-fang-fa/ding-dan-yu-cang-wei/qu-de-ding-dan-xiang-qing-get-privateexplorerordersid
---

# GET orders/{id}

```
GET /v1/private/exchange/orders/{id}
```

#### Path Parameters

| Parameter | Required | Description     |
| --------- | -------- | --------------- |
| `id`      | Yes      | The order UUID. |

#### Response

```json
{
  "success": true,
  "data": {
    "executed_at": "...",
    "execution_price": "...",
    "execution_slippage_bps": "...",
    "filled_quantity": "...",
    "fills": [],
    "limit_price": "...",
    "mark_price": "...",
    "order_id": "...",
    "order_type": "...",
    "position_uid": "...",
    "quantity": "...",
    "reason": "...",
    "remaining_quantity": "...",
    "reserve_remaining": "...",
    "side": "...",
    "status": "...",
    "stop_loss_price": "...",
    "stop_loss_quantity": "...",
    "symbol": "...",
    "take_profit_price": "...",
    "take_profit_quantity": "...",
    "trigger_price": "..."
  }
}
```

#### Response Fields

| Field                               | Type       | Description                                                                                                                    |
| ----------------------------------- | ---------- | ------------------------------------------------------------------------------------------------------------------------------ |
| `data`                              | object     | The structure of the order details containing the list of deals.                                                               |
| `data.executed_at`                  | string     | Fill time, UTC.                                                                                                                |
| `data.execution_price`              | string     | Execution price as a decimal string; truncated per `pxDecimals`.                                                               |
| `data.execution_slippage_bps`       | string     | Slippage used for this execution, in bps, as a decimal string.                                                                 |
| `data.filled_quantity`              | string     | The cumulative number of trades, expressed as a decimal string; press `szDecimals` to truncate the return.                     |
| `data.fills`                        | object \[] | List of transactions, in the order of server-side implementation.                                                              |
| `data.fills.execution_slippage_bps` | string     | The slippage parameter used for this transaction, in bps, is represented by a decimal string.                                  |
| `data.fills.fee`                    | string     | Commission, expressed in decimal string; truncated by quote asset 8 bits.                                                      |
| `data.fills.id`                     | string     | Deal identification.                                                                                                           |
| `data.fills.ledger_tx_id`           | string     | The ledger flow identification corresponding to the transaction.                                                               |
| `data.fills.mark_price`             | string     | The tagged price snapshot used for this transaction, expressed as a decimal string; press `pxDecimals` to truncate the return. |
| `data.fills.price`                  | string     | Transaction price, represented by decimal string; press `pxDecimals` to truncate the return.                                   |
| `data.fills.quantity`               | string     | Number of trades, represented by decimal string; truncated by \`szDecimals'.                                                   |
| `data.limit_price`                  | string     | Limit price when applicable, expressed in decimal string; press `pxDecimals` to truncate return.                               |
| `data.mark_price`                   | string     | Mark price snapshot at execution, as a decimal string; truncated per `pxDecimals`.                                             |
| `data.order_id`                     | string     | Order id.                                                                                                                      |
| `data.order_type`                   | string     | Order type.                                                                                                                    |
| `data.position_uid`                 | string     | `position_uid` of the linked position; only when the order is tied to a position.                                              |
| `data.quantity`                     | string     | Original order quantity as a decimal string; truncated per `szDecimals`.                                                       |
| `data.reason`                       | string     | Reason the order filled or closed; e.g. user, take\_profit, stop\_loss, insurance, adl, liquidation.                           |
| `data.remaining_quantity`           | string     | Result of `quantity - filled_quantity`, as a decimal string; truncated per `szDecimals`.                                       |
| `data.reserve_remaining`            | string     | Remaining reserve, as a decimal string; truncated to 8 decimals in quote asset.                                                |
| `data.side`                         | string     | Order side.                                                                                                                    |
| `data.status`                       | string     | Current order status.                                                                                                          |
| `data.stop_loss_price`              | string     | Stop-loss trigger from the parent order or historical, as a decimal string; truncated per `pxDecimals`.                        |
| `data.stop_loss_quantity`           | string     | Stop-loss quantity from the parent order, as a decimal string; truncated per `szDecimals`.                                     |
| `data.symbol`                       | string     | Full market symbol.                                                                                                            |
| `data.take_profit_price`            | string     | Take-profit trigger from the parent order or historical, as a decimal string; truncated per `pxDecimals`.                      |
| `data.take_profit_quantity`         | string     | Take-profit quantity from the parent order, as a decimal string; truncated per `szDecimals`.                                   |
| `data.trigger_price`                | string     | Historical trigger price for conditional orders, as a decimal string; truncated per `pxDecimals`; legacy field.                |
| `success`                           | boolean    |                                                                                                                                |
