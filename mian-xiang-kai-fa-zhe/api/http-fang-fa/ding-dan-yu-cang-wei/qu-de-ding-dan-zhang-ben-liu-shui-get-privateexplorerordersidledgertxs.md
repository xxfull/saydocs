# 取得訂單帳本流水（GET /exchange/orders/{id}/ledger-txs）

```
GET /v1/private/exchange/orders/{id}/ledger-txs
```

#### 路徑參數

| 參數   | 必填 | 說明       |
| ---- | -- | -------- |
| `id` | 是  | 訂單 UUID。 |

#### 回應

```json
{
  "success": true,
  "data": {
    "order_id": "...",
    "transactions": []
  }
}
```

#### 回應欄位

| 欄位                             | 類型         | 說明                                   |
| ------------------------------ | ---------- | ------------------------------------ |
| `data`                         | object     | 查詢結果。                                |
| `data.order_id`                | string     | 訂單 ID。                               |
| `data.transactions`            | object \[] | 帳本流水列表。                              |
| `data.transactions.created_at` | string     | 流水建立時間，UTC。                          |
| `data.transactions.kind`       | string     | 帳本流水類型。                              |
| `data.transactions.line_count` | integer    | 該流水包含的帳本分錄數量。                        |
| `data.transactions.tx_hash`    | string     | 帳本流水雜湊。由真實 `tx_id` 派生，不返回原始 `tx_id`。 |
| `success`                      | boolean    | 請求是否成功。                              |
