# 查詢內部劃轉（POST /wallet/internal-transfers）

```
POST /v1/public/exchange/wallet/internal-transfers
```

#### 請求體

| 欄位          | 類型         | 必填 | 說明                                              |
| ----------- | ---------- | -- | ----------------------------------------------- |
| `address`   | string     | 否  | 單地址模式。與 `addresses` 二選一，若兩者同時存在，`addresses` 優先。 |
| `addresses` | string \[] | 否  | 多地址批次查詢。非空時忽略 `address`。去重後最多 20 個。             |
| `cursor`    | string     | 否  | 上一頁回傳的 `next_cursor`。                           |
| `direction` | string     | 否  | 過濾流入、流出或全部內部劃轉。                                 |
| `endTime`   | integer    | 否  | 毫秒時間戳上界，條件為 `created_at <= endTime`。            |
| `limit`     | integer    | 否  | 每頁最大返回記錄數。                                      |
| `startTime` | integer    | 否  | 毫秒時間戳下界，條件為 `created_at >= startTime`。          |

#### 回應

```json
{
  "success": true,
  "data": {
    "items": [],
    "next_cursor": "..."
  }
}
```

#### 回應欄位

| 欄位                        | 類型         | 說明                                                                                          |
| ------------------------- | ---------- | ------------------------------------------------------------------------------------------- |
| `data`                    | object     | 查詢結果。                                                                                       |
| `data.items`              | object \[] | 內部劃轉記錄列表。                                                                                   |
| `data.items.address`      | string     | 多地址查詢時，用於歸屬判斷的逐列 EVM 地址。若搭配 `direction`，在 `internal` 情況下通常為發送方。                             |
| `data.items.amount`       | string     | 劃轉金額，以十進位字串表示。                                                                              |
| `data.items.asset`        | string     | 資產符號。                                                                                       |
| `data.items.created_at`   | string     | 內部劃轉建立時間，UTC。                                                                               |
| `data.items.direction`    | string     | 對單地址查詢而言，表示相對於該 `address` 是 `in` 或 `out`。對多地址查詢而言，若流出與流入雙方都在這組 `addresses` 內，則為 `internal`。 |
| `data.items.from_address` | string     | 發送方 EVM 地址。                                                                                 |
| `data.items.to_address`   | string     | 接收方 EVM 地址。                                                                                 |
| `data.items.transfer_id`  | string     | 內部劃轉的冪等鍵，不含 `transfer:` 前綴。                                                                 |
| `data.items.tx_hash`      | string     | 內部劃轉帳本交易雜湊，由 `tx_id` 派生。                                                                    |
| `data.items.tx_id`        | string     | 帳本劃轉 ID，固定帶有 `transfer:` 前綴。                                                                |
| `data.next_cursor`        | string     | 下一頁的不透明游標。空字串表示沒有下一頁。                                                                       |
| `success`                 | boolean    | 請求是否成功。                                                                                     |
