# 秒動合約批量開倉

秒動合約（Beats）批量開倉。單次最多 **25** 格；`symbol`、`margin`、`clientOrderId` 為批次級統一。

```
POST /v1/private/beats/batch-open
```



#### Request Body

| 欄位                  | 類型        | 必填 | 說明               |
| ------------------- | --------- | -- | ---------------- |
| `symbol`            | string    | 是  | 交易對，如 `BTC-USD`。 |
| `margin`            | string    | 是  | 每格統一保證金（USDC）。   |
| `clientOrderId`     | string    | 是  | 批次冪等鍵。           |
| `items`             | object\[] | 是  | 坐標列表，最多 25 項。    |
| `items[].beginTime` | integer   | 是  | 預測窗口開始（Unix ms）。 |
| `items[].endTime`   | integer   | 是  | 預測窗口結束（Unix ms）。 |
| `items[].priceMin`  | string    | 是  | 價帶下限。            |
| `items[].priceMax`  | string    | 是  | 價帶上限。            |

#### Response — `data`

| 欄位                            | 類型        | 說明                |
| ----------------------------- | --------- | ----------------- |
| `clientOrderId`               | string    | 批次冪等鍵。            |
| `summary.requested`           | integer   | 請求格數。             |
| `summary.succeeded`           | integer   | 成功格數（含重放）。        |
| `summary.failed`              | integer   | 失敗格數。             |
| `summary.replayed`            | integer   | 冪等重放格數。           |
| `summary.newOpened`           | integer   | 本批新開倉格數。          |
| `summary.totalMarginDeducted` | string    | 本批扣款總額。           |
| `results[]`                   | object\[] | 與 `items` 順序一一對應。 |

#### Errors（整批級，非 2xx）

| HTTP | Code                                          | 說明                                          |
| ---- | --------------------------------------------- | ------------------------------------------- |
| 400  | `BEATS_BAD_REQUEST` / `BEATS_BATCH_TOO_LARGE` | 參數非法或超過 25 格。                               |
| 403  | `BEATS_NOT_FOUND`                             | 帳戶不存在。                                      |
| 409  | `BEATS_INSUFFICIENT_FUNDS`                    | 餘額不足（含 `data.required` / `data.available`）。 |
| 409  | `BEATS_REQUEST_IN_PROGRESS`                   | 同 `clientOrderId` 進行中。                      |
| 503  | `LITEOPTION_PRICE_UNAVAILABLE`                | Oracle mark price 不可用。                      |

單格級錯誤（HTTP 200）：`BEATS_CELL_NOT_FOUND`、`BEATS_OPEN_WINDOW_CLOSED`、`BEATS_DUPLICATE_CELL_IN_REQUEST` 等，見 `results[].code`。

**部分成功語意**：單格失敗仍回傳 HTTP 200，見 `data.results[].status=failed`；整批級錯誤（餘額不足、並發鎖等）回傳非 2xx。
