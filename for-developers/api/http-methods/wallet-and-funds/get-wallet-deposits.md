---
description: Deposits for an address.
metaLinks:
  alternates:
    - >-
      https://app.gitbook.com/s/KiKbOTrmqLWnXHD7ZyeJ/mian-xiang-kai-fa-zhe/api/http-fang-fa/qian-bao-yu-zi-jin/qu-de-chong-zhi-ji-lu-get-walletdeposits
---

# GET wallet/deposits

```
GET /v1/public/exchange/wallet/deposits
```

#### Query Parameters

| Parameter | Required | Description                                                      |
| --------- | -------- | ---------------------------------------------------------------- |
| `address` | Yes      | EVM wallet address to query.                                     |
| `limit`   | No       | Maximum number of records per page.                              |
| `cursor`  | No       | Opaque pagination cursor from the previous page's `next_cursor`. |

#### Response

```json
{
  "success": true,
  "data": {
    "items": [],
    "next_cursor": "..."
  }
}
```

#### Response Fields

| Field                               | Type       | Description                                                                                                                                                                                                                                           |
| ----------------------------------- | ---------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `data`                              | object     |                                                                                                                                                                                                                                                       |
| `data.items`                        | object \[] |                                                                                                                                                                                                                                                       |
| `data.items.amount`                 | string     | Deposit amount as a decimal string.                                                                                                                                                                                                                   |
| `data.items.asset`                  | string     | Asset symbol.                                                                                                                                                                                                                                         |
| `data.items.chain`                  | string     | Chain id (lowercase slug) from `onchain_deposits.chain` / `withdraw_requests.chain`. Supported values are documented for the Explorer wallet API.                                                                                                     |
| `data.items.confirmations`          | integer    | Current confirmation count.                                                                                                                                                                                                                           |
| `data.items.created_at`             | string     | Record creation time, UTC.                                                                                                                                                                                                                            |
| `data.items.id`                     | string     | Deposit record id.                                                                                                                                                                                                                                    |
| `data.items.ledger_tx_id`           | string     | Ledger entry id created for the deposit.                                                                                                                                                                                                              |
| `data.items.log_index`              | integer    | Event log index in the transaction.                                                                                                                                                                                                                   |
| `data.items.required_confirmations` | integer    | Required confirmations threshold.                                                                                                                                                                                                                     |
| `data.items.source_tx_hash`         | string     | Original on-chain deposit transaction hash.                                                                                                                                                                                                           |
| `data.items.status`                 | string     | The normalized result of the wallet API for `onchain_deposits.status': only` credited `or 'confirming` is returned (including non-terminal states such as on-chain detection and entry, and the remaining source states such as`detected`/`ignored`). |
| `data.items.tx_hash`                | string     | Deposit ledger tx hash, derived from `ledger_tx_id`.                                                                                                                                                                                                  |
| `data.next_cursor`                  | string     | Opaque cursor for the next page. Empty string means no next page.                                                                                                                                                                                     |
| `success`                           | boolean    |                                                                                                                                                                                                                                                       |
