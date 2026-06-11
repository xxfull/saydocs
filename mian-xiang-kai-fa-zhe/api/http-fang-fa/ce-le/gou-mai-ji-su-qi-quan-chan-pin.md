---
hidden: true
---

# 購買極速期權產品

購買 active 狀態的極速期權產品份額，並建立 **open** 狀態的使用者倉位。

```
POST /v1/private/flashoption/orders
```

#### 請求體

| Field             | Type    | Required | Description            |
| ----------------- | ------- | -------- | ---------------------- |
| `product_id`      | string  | 是        | 要購買的產品 ID。             |
| `shares`          | integer | 是        | 購買份數；最小 1。             |
| `client_order_id` | string  | 否        | 可選冪等鍵；同一帳戶重複使用時返回已有倉位。 |

#### 回應

```json
{
  "success": true,
  "data": {
    "position": {
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
      "status": "open",
      "tx_hash": "0x1111111111111111111111111111111111111111111111111111111111111111",
      "client_order_id": "0x658ef23ceca717a14cddb3689b96014148992825-100000001-001",
      "created_at": 1779870012500
    }
  }
}
```

#### 回應欄位 — `data.position`

| Field             | Type    | Description                                                  |
| ----------------- | ------- | ------------------------------------------------------------ |
| `product_id`      | string  | 產品 ID。                                                       |
| `symbol`          | string  | 交易對。                                                         |
| `touch_mode`      | string  | `long` / `short` / `breakout`。                               |
| `shares`          | integer | 購買份數。                                                        |
| `price_per_share` | string  | 每份保費。                                                        |
| `premium_amount`  | string  | 總保費（`shares × price_per_share`）。                             |
| `odds`            | string  | 賠率倍數。                                                        |
| `start_price`     | string  | 產品起始參考價。                                                     |
| `opened_price`    | string  | 開倉時 mark price 快照。                                           |
| `opened_price_ts` | integer | 開倉價格時間戳（Unix 毫秒）。                                            |
| `started_at`      | integer | 產品開始時間（Unix 毫秒）。                                             |
| `settled_at`      | integer | 預定結算時間（Unix 毫秒）。                                             |
| `status`          | string  | 新建倉位為 `open`。                                                |
| `tx_hash`         | string  | 內部帳本 tx\_id 的 SHA3-256 哈希（`0x` + 64 hex）；不暴露原始 ledger tx id。 |
| `client_order_id` | string  | 若請求有提供則回傳。                                                   |
| `created_at`      | integer | 倉位建立時間（Unix 毫秒）。                                             |

#### 錯誤碼

| HTTP | Code                                    | 說明                     |
| ---- | --------------------------------------- | ---------------------- |
| 401  | `LITEOPTION_UNAUTHORIZED`               | 缺少有效身份或 gateway 驗簽失敗。  |
| 404  | `LITEOPTION_NOT_FOUND`                  | 帳戶或產品不存在。              |
| 409  | `LITEOPTION_PRODUCT_NOT_ACTIVE`         | 產品非 active。            |
| 409  | `LITEOPTION_PRODUCT_NOT_STARTED`        | 產品尚未開始。                |
| 409  | `LITEOPTION_PRODUCT_EXPIRED`            | 產品已到期或已結算。             |
| 409  | `LITEOPTION_PRODUCT_SOLD_OUT`           | 剩餘份額不足。                |
| 409  | `LITEOPTION_PRODUCT_PRICE_OUT_OF_RANGE` | mark price 超出可購買距離。    |
| 409  | `LITEOPTION_PRODUCT_INVALID_CONFIG`     | 產品配置異常。                |
| 409  | `LITEOPTION_INSUFFICIENT_FUNDS`         | USDC 餘額不足。             |
| 503  | `LITEOPTION_PRICE_UNAVAILABLE`          | Oracle mark price 不可用。 |
| 503  | `LITEOPTION_PRICE_SYMBOL_MISMATCH`      | 價格快照 symbol 與產品不一致。    |
| 500  | `LITEOPTION_INTERNAL`                   | 服務端內部錯誤。               |
