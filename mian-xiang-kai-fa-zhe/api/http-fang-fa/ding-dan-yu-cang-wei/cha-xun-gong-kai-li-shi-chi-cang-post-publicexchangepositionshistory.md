# 查詢公開歷史持倉（POST /public/exchange/positions/history）

按 `address` 或 `addresses` 查詢已平倉倉位。

```
POST /v1/public/exchange/positions/history
```

### 請求體

| 欄位          | 類型         | 必填 | 說明                     |
| ----------- | ---------- | -- | ---------------------- |
| `address`   | string     | 否  | 單地址查詢模式下使用的 EVM 地址。    |
| `addresses` | string \[] | 否  | 多地址查詢模式。原始請求陣列最多 20 個。 |

若需使用其他查詢欄位，請以核心契約為準。

### 回應

成功時，`data.positions` 為已平倉持倉列表。

回應中的欄位命名使用 `snake_case`。

`data.total` 為匹配總數。

```json
{
  "success": true,
  "data": {
    "positions": [
      {
        "address": "0x1234567890abcdef1234567890abcdef12345678",
        "avg_close_price": "63360.00",
        "close_reason": "user_close",
        "closed_at": "2026-05-20T15:30:00Z",
        "closed_quantity": "0.5000",
        "entry_price": "62000.00",
        "margin": "3100.00",
        "opened_at": "2026-05-18T08:00:00Z",
        "opening_fee": "1.24",
        "position_uid": "9d3eb3f8-85af-42c5-8aee-56a2b86516f6",
        "realized_pnl": "680.00",
        "side": "buy",
        "size": "0.5000",
        "symbol": "BTC-USD"
      }
    ],
    "total": 1
  }
}
```

#### 回應欄位

| 欄位                               | 類型         | 說明             |
| -------------------------------- | ---------- | -------------- |
| `success`                        | boolean    | 請求是否成功。        |
| `data`                           | object     | 查詢結果。          |
| `data.positions`                 | object \[] | 已平倉持倉列表。       |
| `data.total`                     | integer    | 匹配總數。          |
| `data.positions.address`         | string     | 持倉地址。          |
| `data.positions.avg_close_price` | string     | 平均平倉價格。        |
| `data.positions.close_reason`    | string     | 平倉原因。          |
| `data.positions.closed_at`       | string     | 平倉時間，ISO 8601。 |
| `data.positions.closed_quantity` | string     | 已平倉數量。         |
| `data.positions.entry_price`     | string     | 開倉均價。          |
| `data.positions.margin`          | string     | 保證金。           |
| `data.positions.opened_at`       | string     | 開倉時間，ISO 8601。 |
| `data.positions.opening_fee`     | string     | 開倉手續費。         |
| `data.positions.position_uid`    | string     | 持倉唯一識別碼。       |
| `data.positions.realized_pnl`    | string     | 已實現盈虧。         |
| `data.positions.side`            | string     | 倉位方向，如 `buy`。  |
| `data.positions.size`            | string     | 持倉數量。          |
| `data.positions.symbol`          | string     | 交易對。           |

#### 狀態碼

| 狀態碼   | 說明                  |
| ----- | ------------------- |
| `200` | 查詢成功。               |
| `400` | 參數錯誤。回傳 core 錯誤封裝。  |
| `503` | 服務不可用。回傳 core 錯誤封裝。 |
