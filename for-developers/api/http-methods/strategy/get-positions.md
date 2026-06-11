# GET positions

Paginated **Trend/Beats** position list by wallet address / account ID.

```
GET /v1/public/beats/positions
```

```
GET /v1/public/trend/positions
```

#### Query Parameters

| Parameter           | Type      | Required | Description                                                                               |
| ------------------- | --------- | -------- | ----------------------------------------------------------------------------------------- |
| `phase`             | string    | Yes      | `open` (default statuses `open`/`settlement_failed`) or `settled` (default `won`/`lost`). |
| `status`            | string\[] | No       | Repeatable; must be in the allowed set for `phase`.                                       |
| `wallet_address`    | string\[] | No       | EVM addresses; max 10 combined with `account_id` after dedup.                             |
| `account_id`        | string\[] | No       | Account UUIDs; repeatable.                                                                |
| `symbol`            | string    | No       | Symbol or combo identifier filter.                                                        |
| `created_after_ms`  | integer   | No       | Only positions with `created_at` ≥ this Unix ms.                                          |
| `created_before_ms` | integer   | No       | Only positions with `created_at` ≤ this Unix ms.                                          |
| `cursor`            | string    | No       | Previous page `data.pagination.next_cursor`.                                              |
| `page_size`         | integer   | No       | Page size; default 20, max 100.                                                           |
| `has_total`         | integer   | No       | Unsupported; non-zero → `PAGINATION_HAS_TOTAL_UNSUPPORTED`.                               |

#### Response Fields

| Field                         | Type      | Description                                      |
| ----------------------------- | --------- | ------------------------------------------------ |
| `data.phase`                  | string    | Query phase.                                     |
| `data.pagination.page_size`   | integer   | Page size.                                       |
| `data.pagination.next_cursor` | string    | Next-page cursor; empty when no more.            |
| `data.pagination.has_more`    | boolean   | Whether more pages exist.                        |
| `data.list[]`                 | object\[] | Position rows (snake\_case).                     |
| `data.list[].id`              | string    | Position UUID.                                   |
| `data.list[].account_id`      | string    | Account UUID.                                    |
| `data.list[].wallet_address`  | string    | Wallet address.                                  |
| `data.list[].symbol`          | string    | Symbol or combo id.                              |
| `data.list[].margin`          | string    | Margin.                                          |
| `data.list[].odds`            | string    | Odds.                                            |
| `data.list[].opened_price`    | string    | Open price snapshot.                             |
| `data.list[].opened_price_ts` | integer   | Open price timestamp.                            |
| `data.list[].status`          | string    | e.g. `open`, `settlement_failed`, `won`, `lost`. |
| `data.list[].begin_time`      | integer   | Position start (Unix ms).                        |
| `data.list[].end_time`        | integer   | Position end (Unix ms).                          |
| `data.list[].tx_hash`         | string    | Open ledger tx hash.                             |
| `data.list[].payout_amount`   | string    | Payout; usually `0` before settlement.           |
| `data.list[].created_at`      | integer   | Created time.                                    |
| `data.list[].updated_at`      | integer   | Updated time.                                    |

Product-specific fields: OpenAPI `TrendPositionListItem` (snake\_case in list).

#### Errors

| HTTP | Code                               | Meaning                             |
| ---- | ---------------------------------- | ----------------------------------- |
| 400  | `TREND_BAD_REQUEST`                | Invalid params or identity filters. |
| 400  | `PAGINATION_INVALID_REQUEST`       | Invalid cursor.                     |
| 400  | `PAGINATION_HAS_TOTAL_UNSUPPORTED` | Unsupported `has_total`.            |
| 500  | `TREND_INTERNAL`                   | Internal server error.              |
