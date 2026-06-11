# 查詢产品倉位列表

查詢**秒動合約 /** **連擊 /** **波動率 / 配對 / 區間 / 階梯 / 趨勢**倉位列表。

```
GET /v1/public/beats/positions
```

```
GET /v1/public/combo/positions
```

```
GET /v1/public/pair/positions
```

```
GET /v1/public/moves/positions
```

```
GET /v1/public/range/positions
```

```
GET /v1/public/steps/positions
```

```
GET /v1/public/trend/positions
```

#### Query Parameters

| 參數                  | 類型        | 必填 | 說明                                                                         |
| ------------------- | --------- | -- | -------------------------------------------------------------------------- |
| `phase`             | string    | 是  | `open`（未結算，預設 `open`/`settlement_failed`）或 `settled`（已結算，預設 `won`/`lost`）。 |
| `status`            | string\[] | 否  | 可重複傳參；須在 `phase` 允許集合內。                                                    |
| `wallet_address`    | string\[] | 否  | EVM 地址，可重複；與 `account_id` 合計去重後最多 10 個。                                    |
| `account_id`        | string\[] | 否  | 帳戶 UUID，可重複。                                                               |
| `symbol`            | string    | 否  | 交易對或組合標識篩選。                                                                |
| `created_after_ms`  | integer   | 否  | 僅回傳 `created_at` ≥ 該毫秒時間戳的倉位。                                              |
| `created_before_ms` | integer   | 否  | 僅回傳 `created_at` ≤ 該毫秒時間戳的倉位。                                              |
| `cursor`            | string    | 否  | 上一頁 `data.pagination.next_cursor`。                                         |
| `page_size`         | integer   | 否  | 每頁條數，預設 20，最大 100。                                                         |
| `has_total`         | integer   | 否  | 不支援；非 0 回傳 `PAGINATION_HAS_TOTAL_UNSUPPORTED`。                             |

#### Response Fields

| 欄位                            | 類型        | 說明                                               |
| ----------------------------- | --------- | ------------------------------------------------ |
| `data.phase`                  | string    | 當前查詢階段。                                          |
| `data.pagination.page_size`   | integer   | 本頁 page size。                                    |
| `data.pagination.next_cursor` | string    | 下一頁 cursor；無更多時可能為空。                             |
| `data.pagination.has_more`    | boolean   | 是否還有下一頁。                                         |
| `data.list[]`                 | object\[] | 倉位列表（snake\_case）。                               |
| `data.list[].id`              | string    | 倉位 UUID。                                         |
| `data.list[].account_id`      | string    | 帳戶 UUID。                                         |
| `data.list[].wallet_address`  | string    | 錢包地址。                                            |
| `data.list[].symbol`          | string    | 交易對或組合標識。                                        |
| `data.list[].margin`          | string    | 保證金。                                             |
| `data.list[].odds`            | string    | 賠率。                                              |
| `data.list[].opened_price`    | string    | 開倉價快照。                                           |
| `data.list[].opened_price_ts` | integer   | 開倉價時間戳。                                          |
| `data.list[].status`          | string    | `open` / `settlement_failed` / `won` / `lost` 等。 |
| `data.list[].begin_time`      | integer   | 持倉開始（Unix ms）。                                   |
| `data.list[].end_time`        | integer   | 持倉結束（Unix ms）。                                   |
| `data.list[].tx_hash`         | string    | 開倉帳本 tx 哈希。                                      |
| `data.list[].payout_amount`   | string    | 賠付金額；未結算通常為 `0`。                                 |
| `data.list[].created_at`      | integer   | 建立時間。                                            |
| `data.list[].updated_at`      | integer   | 更新時間。                                            |

產品特有欄位見 OpenAPI `ComboPositionListItem`；列表項為 snake\_case。

#### Errors

| HTTP | Code                               | 說明                               |
| ---- | ---------------------------------- | -------------------------------- |
| 400  | `COMBO_BAD_REQUEST`                | 參數非法、phase/status 不匹配或身份過濾為空/過多。 |
| 400  | `PAGINATION_INVALID_REQUEST`       | cursor 非法或與 phase 不一致。           |
| 400  | `PAGINATION_HAS_TOTAL_UNSUPPORTED` | 請求了不支援的 `has_total`。             |
| 500  | `COMBO_INTERNAL`                   | 服務端內部錯誤。                         |
