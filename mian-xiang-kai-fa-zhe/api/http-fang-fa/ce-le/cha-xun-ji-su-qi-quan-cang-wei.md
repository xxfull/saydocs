---
hidden: true
---

# 查詢極速期權倉位

查詢使用者極速期權倉位歷史。

* 可在請求體透過 `addresses` 指定多個錢包地址批量查詢；
* 多地址模式會將 EVM 地址小寫去重，**最多 10 個**；當請求至少兩個地址時，每筆 `items[]` 額外回傳 `address` 欄位。

```
POST /v1/public/flashoption/positions/history
```

#### 請求體

| Field               | Type      | Required | Description                                      |
| ------------------- | --------- | -------- | ------------------------------------------------ |
| `address`           | string    | 否\*      | 單地址查詢；未傳 `addresses` 時可用；亦兼容 `X-Address`。        |
| `addresses`         | string\[] | 否        | 多地址查詢；非空時優先於 `address` 與 `X-Address`，去重後最多 10 個。 |
| `status`            | string    | 否        | 倉位狀態篩選，見下方枚舉。                                    |
| `symbol`            | string    | 否        | 交易對篩選。                                           |
| `touch_mode`        | string    | 否        | 方向篩選：`long`、`short`、`breakout`。                  |
| `product_id`        | string    | 否        | 產品 ID 篩選。                                        |
| `page_size`         | integer   | 否        | 每頁筆數；預設 20，最大 100。                               |
| `cursor_created_at` | integer   | 否        | 上一頁 `next_cursor.created_at`。                    |
| `cursor_id`         | string    | 否        | 上一頁 `next_cursor.id`（UUID）。                      |

\* 必須提供 `address`、`addresses` 或 `X-Address` 之一。

**`status` 允許值**

| Value               | 說明      |
| ------------------- | ------- |
| `open`              | 持有中     |
| `settling`          | 結算中     |
| `won`               | 中獎已賠付   |
| `lost`              | 未中獎     |
| `settlement_failed` | 結算失敗待重試 |
| `cancelled`         | 已取消     |
| `refunded`          | 已退款     |

#### 回應

```json
{
  "success": true,
  "data": {
    "items": [
      {
        "address": "0x658ef23ceca717a14cddb3689b96014148992825",
        "product_id": "100000001",
        "symbol": "BTC-USDT",
        "touch_mode": "long",
        "shares": 10,
        "price_per_share": "1",
        "premium_amount": "10",
        "odds": "1.8",
        "start_price": "67000",
        "opened_price": "67120.5",
        "opened_price_ts": 1779870012345,
        "started_at": 1779870000000,
        "settled_at": 1779870300000,
        "actual_settled_at": 1779870300123,
        "settlement_price": "68120.5",
        "status": "won",
        "payout_amount": "18",
        "tx_hash": "0x1111111111111111111111111111111111111111111111111111111111111111",
        "settlement_tx_hash": "0x2222222222222222222222222222222222222222222222222222222222222222",
        "client_order_id": "0x658ef23ceca717a14cddb3689b96014148992825-100000001-001",
        "created_at": 1779870012500
      }
    ],
    "page_size": 20,
    "has_more": true,
    "next_cursor": {
      "created_at": 1779870012500,
      "id": "019704dd-6c80-7000-8000-000000000001"
    }
  }
}
```

#### 回應欄位

| Field                           | Type      | Description                 |
| ------------------------------- | --------- | --------------------------- |
| `data.items`                    | object\[] | 倉位記錄列表。                     |
| `data.items.address`            | string    | 多地址查詢（≥2 個地址）時回傳，標明歸屬錢包。    |
| `data.items.product_id`         | string    | 產品 ID。                      |
| `data.items.symbol`             | string    | 交易對。                        |
| `data.items.touch_mode`         | string    | 產品方向。                       |
| `data.items.shares`             | integer   | 份數。                         |
| `data.items.price_per_share`    | string    | 每份保費。                       |
| `data.items.premium_amount`     | string    | 總保費。                        |
| `data.items.odds`               | string    | 賠率倍數。                       |
| `data.items.start_price`        | string    | 產品起始參考價。                    |
| `data.items.opened_price`       | string    | 開倉 mark price。              |
| `data.items.opened_price_ts`    | integer   | 開倉價格時間戳。                    |
| `data.items.started_at`         | integer   | 產品開始時間。                     |
| `data.items.settled_at`         | integer   | 預定結算時間。                     |
| `data.items.actual_settled_at`  | integer   | 實際結算完成時間；`0` 表示尚未結算。        |
| `data.items.settlement_price`   | string    | 結算 mark price；未結算時可能省略。     |
| `data.items.status`             | string    | 倉位狀態，見上方枚舉。                 |
| `data.items.payout_amount`      | string    | 結算賠付金額；結算前通常為 `0`。          |
| `data.items.tx_hash`            | string    | 開倉帳本 tx 哈希。                 |
| `data.items.settlement_tx_hash` | string    | 結算帳本 tx 哈希。                 |
| `data.items.client_order_id`    | string    | 客戶端冪等鍵（若有）。                 |
| `data.items.created_at`         | integer   | 倉位建立時間。                     |
| `data.page_size`                | integer   | 本頁請求的 page size。            |
| `data.has_more`                 | boolean   | 是否還有下一頁。                    |
| `data.next_cursor`              | object    | 下一頁 cursor；無下一頁時可能為 `null`。 |
| `data.next_cursor.created_at`   | integer   | Cursor 時間戳。                 |
| `data.next_cursor.id`           | string    | Cursor 倉位 ID（UUID）。         |

#### 錯誤碼

| HTTP | Code                            | 說明                |
| ---- | ------------------------------- | ----------------- |
| 400  | `LITEOPTION_ADDRESS_REQUIRED`   | 未提供查詢地址。          |
| 400  | `LITEOPTION_INVALID_ADDRESS`    | 地址格式非法。           |
| 400  | `LITEOPTION_TOO_MANY_ADDRESSES` | 去重後地址超過 10 個。     |
| 400  | `LITEOPTION_INVALID_STATUS`     | `status` 不在允許枚舉中。 |
| 400  | `LITEOPTION_INVALID_TOUCH_MODE` | `touch_mode` 非法。  |
| 400  | `LITEOPTION_INVALID_CURSOR`     | cursor 參數不合法。     |
| 404  | `LITEOPTION_NOT_FOUND`          | 資源不存在。            |
| 500  | `LITEOPTION_INTERNAL`           | 服務端內部錯誤。          |
