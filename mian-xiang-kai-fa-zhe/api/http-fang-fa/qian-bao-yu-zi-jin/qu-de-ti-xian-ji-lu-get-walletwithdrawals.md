# 取得提現記錄（GET /wallet/withdrawals）

```
GET /v1/public/exchange/wallet/withdrawals
```

#### 查詢參數

| 參數        | 必填 | 說明                             |
| --------- | -- | ------------------------------ |
| `address` | 是  | 要查詢的 EVM 錢包地址。                 |
| `limit`   | 否  | 每頁最大返回記錄數。                     |
| `cursor`  | 否  | 上一頁回傳的 `next_cursor`，為不透明分頁游標。 |

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

| 欄位                             | 類型         | 說明                                                                                                                                                                                                                                                                                                                |
| ------------------------------ | ---------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `data`                         | object     | 查詢結果。                                                                                                                                                                                                                                                                                                             |
| `data.items`                   | object \[] | 提現記錄列表。                                                                                                                                                                                                                                                                                                           |
| `data.items.amount`            | string     | 提現金額，以十進位字串表示。                                                                                                                                                                                                                                                                                                    |
| `data.items.asset`             | string     | 代幣合約地址，對應讀模型中的 `token_address`。                                                                                                                                                                                                                                                                                   |
| `data.items.broadcast_tx_hash` | string     | 廣播後的鏈上交易雜湊；若尚未取得則為空字串。                                                                                                                                                                                                                                                                                            |
| `data.items.chain`             | string     | 鏈 ID，為小寫 slug，來源於 `onchain_deposits.chain` / `withdraw_requests.chain`。支援值以 Explorer 錢包 API 文件為準。                                                                                                                                                                                                                 |
| `data.items.created_at`        | string     | 請求建立時間，UTC。                                                                                                                                                                                                                                                                                                       |
| `data.items.failure_reason`    | string     | 失敗原因文字；未失敗時通常為空字串。                                                                                                                                                                                                                                                                                                |
| `data.items.fee`               | string     | 提現手續費，以十進位字串表示。                                                                                                                                                                                                                                                                                                   |
| `data.items.hold_tx_id`        | string     | 內部 hold 帳本分錄 ID。                                                                                                                                                                                                                                                                                                  |
| `data.items.request_id`        | string     | 提現請求 ID。                                                                                                                                                                                                                                                                                                          |
| `data.items.status`            | string     | 顯示狀態，根據 `withdraw_requests.confirm_status` 與 `debit_status` 推導：`debit_status = succeeded` 時為 `success`；`confirm_status = failed` 時為 `fail`；`confirm_status = confirmed` 且尚未 `succeeded` 時為 `pending`；`confirm_status = pending` 時為 `pending`；`confirm_status = init` 時為 `init`。若為未知值，可能回退為原始 `confirm_status` 字串。 |
| `data.items.to_address`        | string     | 目標地址。                                                                                                                                                                                                                                                                                                             |
| `data.items.tx_hash`           | string     | 提現 hold 帳本交易雜湊，由 `withdraw_hold:...` 在本地派生。                                                                                                                                                                                                                                                                       |
| `data.items.updated_at`        | string     | 最後更新時間，UTC。                                                                                                                                                                                                                                                                                                       |
| `data.next_cursor`             | string     | 下一頁的不透明游標。空字串表示沒有下一頁。                                                                                                                                                                                                                                                                                             |
| `success`                      | boolean    | 請求是否成功。                                                                                                                                                                                                                                                                                                           |
