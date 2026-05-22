---
description: Internal transfers (JSON body).
metaLinks:
  alternates:
    - >-
      https://app.gitbook.com/s/KiKbOTrmqLWnXHD7ZyeJ/mian-xiang-kai-fa-zhe/api/http-fang-fa/qian-bao-yu-zi-jin/cha-xun-nei-bu-hua-zhuan-post-publicexplorerwalletinternaltransfers
---

# POST wallet/internal-transfers

```
POST /v1/public/exchange/wallet/internal-transfers
```

#### Request Body

| Field       | Type       | Required | Description                                                                             |
| ----------- | ---------- | -------- | --------------------------------------------------------------------------------------- |
| `address`   | string     | No       | Single address mode. Choose one of two with `addresses` (`addresses` takes precedence). |
| `addresses` | string \[] | No       | Multi-address batch; ignore `address` when non-empty. Up to 20 after deduplication.     |
| `cursor`    | string     | No       | The `next_cursor` returned from the previous page.                                      |
| `direction` | string     | No       |                                                                                         |
| `endTime`   | integer    | No       | millisecond timestamp, `created_at < = endTime`.                                        |
| `limit`     | integer    | No       |                                                                                         |
| `startTime` | integer    | No       | millisecond timestamp, `created_at > = startTime`.                                      |

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

| Field                     | Type       | Description                                                                                                                                                                         |
| ------------------------- | ---------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `data`                    | object     |                                                                                                                                                                                     |
| `data.items`              | object \[] |                                                                                                                                                                                     |
| `data.items.address`      | string     | Per-row EVM address for attribution in multi-address queries (with `direction`; for `internal`, often the sender).                                                                  |
| `data.items.amount`       | string     | Transfer amount as a decimal string.                                                                                                                                                |
| `data.items.asset`        | string     | Asset symbol.                                                                                                                                                                       |
| `data.items.created_at`   | string     | Internal transfer creation time, UTC.                                                                                                                                               |
| `data.items.direction`    | string     | The relative `address' of a single address query is` in `or` out `. For multi-address queries, if both outbound and inbound are in this` addresses `collection, it is` internal \`. |
| `data.items.from_address` | string     | Sender EVM address.                                                                                                                                                                 |
| `data.items.to_address`   | string     | Recipient EVM address.                                                                                                                                                              |
| `data.items.transfer_id`  | string     | Idempotency key for internal transfer without the `transfer:` prefix.                                                                                                               |
| `data.items.tx_hash`      | string     | Internal transfer ledger tx hash, derived from `tx_id`.                                                                                                                             |
| `data.items.tx_id`        | string     | Ledger transfer id, always prefixed with `transfer:`.                                                                                                                               |
| `data.next_cursor`        | string     | Opaque cursor for the next page. Empty string means no next page.                                                                                                                   |
| `success`                 | boolean    |                                                                                                                                                                                     |
