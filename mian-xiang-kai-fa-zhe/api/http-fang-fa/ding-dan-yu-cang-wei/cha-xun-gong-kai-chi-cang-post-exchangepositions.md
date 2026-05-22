# 查詢公開持倉（POST /public/exchange/positions）

按 `addresses` 批量查詢公開的未平倉倉位。

```
POST /v1/public/exchange/positions
```

### 請求體

| 欄位               | 類型         | 必填 | 說明                                            |
| ---------------- | ---------- | -- | --------------------------------------------- |
| `addresses`      | string \[] | 是  | 目標地址列表。原始請求最多 20 個。服務端會按 EVM 地址規則歸一化、去重並轉為小寫。 |
| `symbols`        | string \[] | 否  | 交易對過濾列表。原始請求最多 20 個。服務端會自動做 `trim`、轉大寫與去重。    |
| `insuranceLevel` | string     | 否  | 保險資訊返回層級。省略時預設為 `summary`。                    |
| `offset`         | integer    | 否  | 分頁偏移。預設為 `0`。                                 |
| `limit`          | integer    | 否  | 最大返回筆數。預設為 `100`，上限為 `500`。                   |

#### 請求規則

* 僅支援 body 中的 `addresses` 陣列。
* 不支援單獨 `address` 欄位。
* 服務端會先做地址與交易對的標準化，再執行查詢。

### 回應

成功時，`data.positions` 為目前頁的公開 open positions 列表。

`data.total` 為匹配總數。

金額與數量欄位均以 decimal string 返回。

```json
{
  "success": true,
  "data": {
    "positions": [
      {
        "address": "0x1234567890abcdef1234567890abcdef12345678",
        "avg_close_price": null,
        "closed_quantity": "0",
        "entry_price": "62000.00",
        "insurance": {
          "policies": [
            {
              "closureReason": "",
              "displayStatus": "active",
              "expireAt": 1716604800000,
              "insuranceType": "REVIVAL",
              "lifecycleStatus": "active",
              "paymentStatus": "paid",
              "payoutAmount": "500.00",
              "payoutPercent": 100,
              "policyId": "a1b2c3d4-e5f6-7890-abcd-ef1234567890",
              "premium": "12.50",
              "replacementHint": "",
              "startAt": 1716000000000,
              "status": "active",
              "triggerPercent": 10,
              "triggerPrice": "60000.00",
              "tx_hash": "0xabc..."
            }
          ]
        },
        "margin": "3100.00",
        "mark": "63500.00",
        "mark_stale": false,
        "opened_at": "2026-05-20T10:00:00.123456789Z",
        "opening_fee": "1.24",
        "positionUid": "9d3eb3f8-85af-42c5-8aee-56a2b86516f6",
        "realized_pnl": "0",
        "side": "buy",
        "size": "0.5000",
        "symbol": "BTC-USD",
        "unrealized_pnl": "750.00"
      }
    ],
    "total": 1
  }
}
```

#### 回應欄位

| 欄位                                                  | 類型             | 說明                                      |
| --------------------------------------------------- | -------------- | --------------------------------------- |
| `success`                                           | boolean        | 請求是否成功。                                 |
| `data`                                              | object         | 查詢結果。                                   |
| `data.positions`                                    | object \[]     | 目前頁的公開未平倉倉位列表。                          |
| `data.total`                                        | integer        | 匹配總數。                                   |
| `data.positions.address`                            | string         | 持倉地址。                                   |
| `data.positions.avg_close_price`                    | string \| null | 平均平倉價格。未平倉時通常為 `null`。                  |
| `data.positions.closed_quantity`                    | string         | 已平倉數量。                                  |
| `data.positions.entry_price`                        | string         | 開倉均價。                                   |
| `data.positions.margin`                             | string         | 當前保證金。                                  |
| `data.positions.mark`                               | string         | 當前標記價格。                                 |
| `data.positions.mark_stale`                         | boolean        | 標記價格是否過期。                               |
| `data.positions.opened_at`                          | string         | 開倉時間，ISO 8601。                          |
| `data.positions.opening_fee`                        | string         | 開倉手續費。                                  |
| `data.positions.positionUid`                        | string         | 持倉唯一識別碼。                                |
| `data.positions.realized_pnl`                       | string         | 已實現盈虧。                                  |
| `data.positions.side`                               | string         | 倉位方向，如 `buy`。                           |
| `data.positions.size`                               | string         | 持倉數量。                                   |
| `data.positions.symbol`                             | string         | 交易對。                                    |
| `data.positions.unrealized_pnl`                     | string         | 未實現盈虧。                                  |
| `data.positions.insurance`                          | object         | 保險資訊。當 `insuranceLevel=full` 時可返回更完整內容。 |
| `data.positions.insurance.policies`                 | object \[]     | 保單列表。                                   |
| `data.positions.insurance.policies.closureReason`   | string         | 保單結束原因。                                 |
| `data.positions.insurance.policies.displayStatus`   | string         | 顯示狀態。                                   |
| `data.positions.insurance.policies.expireAt`        | integer        | 到期時間，Unix 毫秒時間戳。                        |
| `data.positions.insurance.policies.insuranceType`   | string         | 保險類型。                                   |
| `data.positions.insurance.policies.lifecycleStatus` | string         | 保單生命週期狀態。                               |
| `data.positions.insurance.policies.paymentStatus`   | string         | 付款狀態。                                   |
| `data.positions.insurance.policies.payoutAmount`    | string         | 赔付金額。                                   |
| `data.positions.insurance.policies.payoutPercent`   | integer        | 赔付百分比。                                  |
| `data.positions.insurance.policies.policyId`        | string         | 保單 ID。                                  |
| `data.positions.insurance.policies.premium`         | string         | 保費。                                     |
| `data.positions.insurance.policies.replacementHint` | string         | 替換提示。                                   |
| `data.positions.insurance.policies.startAt`         | integer        | 生效時間，Unix 毫秒時間戳。                        |
| `data.positions.insurance.policies.status`          | string         | 保單狀態。                                   |
| `data.positions.insurance.policies.triggerPercent`  | integer        | 觸發百分比。                                  |
| `data.positions.insurance.policies.triggerPrice`    | string         | 觸發價格。                                   |
| `data.positions.insurance.policies.tx_hash`         | string         | 相關交易哈希。                                 |

#### 狀態碼

| 狀態碼   | 說明                  |
| ----- | ------------------- |
| `200` | 查詢成功。               |
| `400` | 參數錯誤。回傳 core 錯誤封裝。  |
| `503` | 服務不可用。回傳 core 錯誤封裝。 |
