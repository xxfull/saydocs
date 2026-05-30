# 策略訂閱

### 訂閱請求

| 欄位            | 類型      | 必填 | 說明                                                                |
| ------------- | ------- | -- | ----------------------------------------------------------------- |
| `event`       | string  | 是  | `sub`。                                                            |
| `topic`       | string  | 是  | `flash-option`。                                                   |
| `compression` | integer | 否  | 出站推送編碼：`0` 明文 JSON；`1` gzip 後 Latin-1 文本幀。非法值 → `WS_BAD_REQUEST`。 |
| `id`          | string  | 否  | 若提供，下行推送會回顯。                                                      |

請勿為本 topic 傳 `symbols` 或 `addresses`。

#### 示例

```json
{
  "event": "sub",
  "topic": "flash-option",
  "compression": 0,
  "id": "flash-option-1"
}
```

### 下行推送：flash-option

**沒有頂層 `pair`** — 業務內容在 `data` 內辨識。

| 欄位            | 類型      | 必填 | 說明                                           |
| ------------- | ------- | -- | -------------------------------------------- |
| `topic`       | string  | 是  | 固定 `flash-option`。                           |
| `t`           | integer | 是  | 本服務發送該幀的 Unix 毫秒。                            |
| `id`          | string  | 否  | 訂閱時的 `id` 回顯。                                |
| `compression` | integer | 否  | `0` 或 `1`，與本幀編碼一致。                           |
| `data`        | object  | 是  | 直接等於業務 MQ envelope 的 **`payload`**（服務端不再加工）。 |

#### 當前 `data` 事件：`flash_option.product_active.v1`

| 欄位                   | 類型      | 說明                                   |
| -------------------- | ------- | ------------------------------------ |
| `event_type`         | string  | 固定 `flash_option.product_active.v1`。 |
| `id`                 | string  | 產品 ID。                               |
| `symbol`             | string  | 交易對，例如 `BTC-USDT`。                   |
| `touch_mode`         | string  | `long` / `short` / `breakout`。       |
| `upper_barrier`      | string  | 可選；`long` / `breakout` 產品。           |
| `lower_barrier`      | string  | 可選；`short` / `breakout` 產品。          |
| `start_price`        | string  | 起始參考價。                               |
| `started_at`         | integer | 開始時間（Unix 毫秒）。                       |
| `settled_at`         | integer | 預定結算時間（Unix 毫秒）。                     |
| `duration_sec`       | integer | 持續秒數。                                |
| `odds`               | string  | 賠率倍數。                                |
| `max_shares`         | integer | 最大可售份數。                              |
| `sold_shares`        | integer | 推送時已售份數（激活事件通常為 `0`）。                |
| `price_per_share`    | string  | 每份保費。                                |
| `available_distance` | string  | 可購買距離門檻。                             |
| `status`             | string  | 通常為 `active`。                        |
| `published_at`       | integer | 可選；策略側發布時間（Unix 毫秒）。                 |
| `sent_at`            | integer | lite-option 發送 MQ 的時間（Unix 毫秒）。      |

推送中**不含** `mark_price`；即時 mark 請訂閱 `price` 或輪詢 HTTP 產品列表。

#### 推送示例

```json
{
  "id": "flash-option-1",
  "topic": "flash-option",
  "compression": 0,
  "t": 1712908800456,
  "data": {
    "event_type": "flash_option.product_active.v1",
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
    "sold_shares": 0,
    "price_per_share": "1",
    "available_distance": "50",
    "status": "active",
    "sent_at": 1779870000123
  }
}
```

### 訂閱計數

單連線上 **`flash-option` 整個 topic 計 1 個訂閱槽位**（不按 symbol 拆分）。

### 退訂

#### 請求

| 欄位            | 類型      | 必填 | 說明              |
| ------------- | ------- | -- | --------------- |
| `event`       | string  | 是  | `unsub`。        |
| `topic`       | string  | 是  | `flash-option`。 |
| `compression` | integer | 否  | 可選。             |
| `id`          | string  | 否  | 可選。             |

請勿傳 `symbols` 或 `addresses`。

#### 示例

```json
{
  "event": "unsub",
  "topic": "flash-option"
}
```

#### 回應

生產環境**沒有**單獨的 JSON 確認幀；退訂成功後不再收到後續 `flash-option` 推送。
