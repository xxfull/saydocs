---
hidden: true
---

# 查詢極速期權產品

查詢當前 **active** 且尚未結算的極速期權產品列表。

```
POST /v1/public/flashoption/products
```

#### 請求體

* 請求體可為空 `{}`；若提供篩選條件，各條件之間為 **AND** 關係。

| Field        | Type   | Required | Description                                  |
| ------------ | ------ | -------- | -------------------------------------------- |
| `id`         | string | 否        | 產品 ID 精確篩選。                                  |
| `symbol`     | string | 否        | 交易對篩選；服務端會統一轉成大寫，例如 `BTC-USDT`。              |
| `touch_mode` | string | 否        | 方向篩選。允許值：`long`、`short`、`breakout`；空字串表示不篩選。 |

#### 回應

```json
{
  "success": true,
  "data": {
    "items": [
      {
        "id": "100000001",
        "symbol": "BTC-USDT",
        "touch_mode": "long",
        "upper_barrier": "68000",
        "start_price": "67000",
        "started_at": 1779870000000,
        "settled_at": 1779870300000,
        "duration_sec": 300,
        "odds": "1.8",
        "max_shares": 1000,
        "sold_shares": 12,
        "price_per_share": "1",
        "available_distance": "50",
        "mark_price": "67120.5",
        "status": "active"
      }
    ]
  }
}
```

#### 回應欄位 — `data.items[]`

| Field                | Type    | Description                           |
| -------------------- | ------- | ------------------------------------- |
| `id`                 | string  | 產品 ID。                                |
| `symbol`             | string  | 完整交易對，例如 `BTC-USDT`。                  |
| `touch_mode`         | string  | 產品方向：`long`、`short`、`breakout`。       |
| `upper_barrier`      | string  | `long` / `breakout` 產品的上障；其他方向可能省略。   |
| `lower_barrier`      | string  | `short` / `breakout` 產品的下障；其他方向可能省略。  |
| `start_price`        | string  | 產品起始參考價（decimal string）。              |
| `started_at`         | integer | 產品開始時間（Unix 毫秒）。                      |
| `settled_at`         | integer | 預定結算時間（Unix 毫秒）。                      |
| `duration_sec`       | integer | 產品持續秒數。                               |
| `odds`               | string  | 賠率倍數（decimal string）。                 |
| `max_shares`         | integer | 產品最大可售份數。                             |
| `sold_shares`        | integer | 已售份數。                                 |
| `price_per_share`    | string  | 每份保費（decimal string）。                 |
| `available_distance` | string  | 當前 mark price 距離障礙仍可購買的最大距離門檻。        |
| `mark_price`         | string  | 當前 oracle mark price（decimal string）。 |
| `status`             | string  | 列表中產品固定為 `active`。                    |

#### 錯誤碼

| HTTP | Code                            | 說明                                    |
| ---- | ------------------------------- | ------------------------------------- |
| 400  | `LITEOPTION_INVALID_TOUCH_MODE` | `touch_mode` 非法。                      |
| 503  | `LITEOPTION_PRICE_UNAVAILABLE`  | 某產品對應 symbol 的 mark price 缺失、過期或不可解析。 |
| 500  | `LITEOPTION_INTERNAL`           | 服務端內部錯誤。                              |
