---
description: Single withdrawal.
metaLinks:
  alternates:
    - >-
      https://app.gitbook.com/s/KiKbOTrmqLWnXHD7ZyeJ/mian-xiang-kai-fa-zhe/api/http-fang-fa/qian-bao-yu-zi-jin/qu-de-dan-bi-ti-xian-xiang-qing-get-walletwithdrawalsid
---

# GET wallet/withdrawals/{id}

```
GET /v1/public/exchange/wallet/withdrawals/{id}
```

#### Path Parameters

| Parameter | Required | Description                         |
| --------- | -------- | ----------------------------------- |
| `id`      | Yes      | The UUID of the withdrawal request. |

#### Query Parameters

| Parameter | Required | Description                                                    |
| --------- | -------- | -------------------------------------------------------------- |
| `address` | Yes      | The EVM address of the wallet to which the withdrawal belongs. |

#### Response

```json
{
  "success": true,
  "data": {
    "amount": "...",
    "asset": "...",
    "broadcast_tx_hash": "...",
    "chain": "...",
    "created_at": "...",
    "failure_reason": "...",
    "fee": "...",
    "hold_tx_id": "...",
    "request_id": "...",
    "status": "...",
    "to_address": "...",
    "tx_hash": "...",
    "updated_at": "..."
  }
}
```

#### Response Fields

| Field                    | Type    | Description                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     |
| ------------------------ | ------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `data`                   | object  | The business field of the single withdrawal request (the list item matches the `data` morphology of the detail response).                                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
| `data.amount`            | string  | Withdrawal amount, as a decimal string.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                         |
| `data.asset`             | string  | Token contract address (matches read-model `token_address`).                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    |
| `data.broadcast_tx_hash` | string  | On-chain tx hash after broadcast; empty if not yet available.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                   |
| `data.chain`             | string  | Chain id (lowercase slug) from `onchain_deposits.chain` / `withdraw_requests.chain`. Supported values are documented for the Explorer wallet API.                                                                                                                                                                                                                                                                                                                                                                                                                                               |
| `data.created_at`        | string  | Request creation time, UTC.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     |
| `data.failure_reason`    | string  | Failure reason text; usually empty when not failed.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                             |
| `data.fee`               | string  | Withdrawal fee, as a decimal string.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            |
| `data.hold_tx_id`        | string  | Internal hold ledger entry id.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  |
| `data.request_id`        | string  | Withdrawal request id.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                          |
| `data.status`            | string  | Display status derived from `withdraw_requests.confirm_status` and `debit_status`, consistent with `sayfi-exchange-core/internal/app/server/http/handlers.onchain_withdraw.withdrawalDisplayStatus`: - `debit_status = succeeded` → `success` (ledger finalized) - `confirm_status = failed` → `fail` - `confirm_status = confirmed` and not yet `succeeded` → `pending` (on-chain confirmed; ledger may still be processing) - `confirm_status = pending` → `pending` - `confirm_status = init` → `init` If unknown, may fall back to the raw `confirm_status` string (not in the enum below). |
| `data.to_address`        | string  | Destination address.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            |
| `data.tx_hash`           | string  | Withdrawal hold ledger tx hash, derived locally from `withdraw_hold:...`.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
| `data.updated_at`        | string  | Last update time, UTC.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                          |
| `success`                | boolean |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 |
