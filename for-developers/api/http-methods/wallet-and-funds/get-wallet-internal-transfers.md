---
description: Internal transfers (query).
metaLinks:
  alternates:
    - >-
      https://app.gitbook.com/s/KiKbOTrmqLWnXHD7ZyeJ/mian-xiang-kai-fa-zhe/api/http-fang-fa/qian-bao-yu-zi-jin/qu-de-nei-bu-hua-zhuan-ji-lu-get-walletinternaltransfers
---

# GET wallet/internal-transfers

```
GET /v1/public/exchange/wallet/internal-transfers
```

#### Query Parameters

| Parameter   | Required | Description                                                                                                                                                                                                                                      |
| ----------- | -------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| `address`   | No       | Single address mode is required (when `addresses` is not used). EVM wallet address to query.                                                                                                                                                     |
| `addresses` | No       | <p>Multi-address bulk query: Repeat <code>addresses = 0x... &#x26; addresses = 0x...</code>, or separate individual <code>addresses</code> with commas.<br><code>address</code> is ignored when non-empty. Up to 20 after deduplication.<br></p> |
| `direction` | No       | Filter incoming, outgoing, or all internal transfers.                                                                                                                                                                                            |
| `startTime` | No       | The lower bound of the millisecond timestamp for `created_at > = startTime`.                                                                                                                                                                     |
| `endTime`   | No       | The upper bound of the millisecond timestamp for `created_at < = endTime`.                                                                                                                                                                       |
| `limit`     | No       | Maximum number of records per page.                                                                                                                                                                                                              |
| `cursor`    | No       | Opaque pagination cursor from the previous page's `next_cursor`.                                                                                                                                                                                 |

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
