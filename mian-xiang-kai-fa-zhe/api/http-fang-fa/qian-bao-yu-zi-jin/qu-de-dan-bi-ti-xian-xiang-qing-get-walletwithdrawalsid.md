# 取得單筆提現詳情（GET /wallet/withdrawals/{id}）

```
GET /v1/public/exchange/wallet/withdrawals/{id}
```

#### 路徑參數

| 參數   | 必填 | 說明          |
| ---- | -- | ----------- |
| `id` | 是  | 提現請求的 UUID。 |

#### 查詢參數

| 參數        | 必填 | 說明               |
| --------- | -- | ---------------- |
| `address` | 是  | 該提現所屬錢包的 EVM 地址。 |

#### 回應

```json
{
  "success": true,
  "data": {
    "amount": "...",
    "asset": "...",
    "broadcast_tx_hash": "...",
    "chain": "...",
    "created_at": "...",
    "failure_reason": "...",
    "fee": "...",
    "hold_tx_id": "...",
    "request_id": "...",
    "status": "...",
    "to_address": "...",
    "tx_hash": "...",
    "updated_at": "..."
  }
}
```

#### 回應欄位

| 欄位                       | 類型      | 說明                                                                                                                                                                                                                                                                                                                                                                                                                      |
| ------------------------ | ------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `data`                   | object  | 單筆提現請求的業務欄位。其結構與列表介面中的單筆項目一致。                                                                                                                                                                                                                                                                                                                                                                                           |
| `data.amount`            | string  | 提現金額，以十進位字串表示。                                                                                                                                                                                                                                                                                                                                                                                                          |
| `data.asset`             | string  | 代幣合約地址，對應讀模型中的 `token_address`。                                                                                                                                                                                                                                                                                                                                                                                         |
| `data.broadcast_tx_hash` | string  | 廣播後的鏈上交易雜湊；若尚未取得則為空字串。                                                                                                                                                                                                                                                                                                                                                                                                  |
| `data.chain`             | string  | 鏈 ID，為小寫 slug，來源於 `onchain_deposits.chain` / `withdraw_requests.chain`。支援值以 Explorer 錢包 API 文件為準。                                                                                                                                                                                                                                                                                                                       |
| `data.created_at`        | string  | 請求建立時間，UTC。                                                                                                                                                                                                                                                                                                                                                                                                             |
| `data.failure_reason`    | string  | 失敗原因文字；未失敗時通常為空字串。                                                                                                                                                                                                                                                                                                                                                                                                      |
| `data.fee`               | string  | 提現手續費，以十進位字串表示。                                                                                                                                                                                                                                                                                                                                                                                                         |
| `data.hold_tx_id`        | string  | 內部 hold 帳本分錄 ID。                                                                                                                                                                                                                                                                                                                                                                                                        |
| `data.request_id`        | string  | 提現請求 ID。                                                                                                                                                                                                                                                                                                                                                                                                                |
| `data.status`            | string  | 顯示狀態，根據 `withdraw_requests.confirm_status` 與 `debit_status` 推導，與 `sayfi-exchange-core/internal/app/server/http/handlers.onchain_withdraw.withdrawalDisplayStatus` 一致：`debit_status = succeeded` 時為 `success`；`confirm_status = failed` 時為 `fail`；`confirm_status = confirmed` 且尚未 `succeeded` 時為 `pending`；`confirm_status = pending` 時為 `pending`；`confirm_status = init` 時為 `init`。若為未知值，可能回退為原始 `confirm_status` 字串。 |
| `data.to_address`        | string  | 目標地址。                                                                                                                                                                                                                                                                                                                                                                                                                   |
| `data.tx_hash`           | string  | 提現 hold 帳本交易雜湊，由 `withdraw_hold:...` 在本地派生。                                                                                                                                                                                                                                                                                                                                                                             |
| `data.updated_at`        | string  | 最後更新時間，UTC。                                                                                                                                                                                                                                                                                                                                                                                                             |
| `success`                | boolean | 請求是否成功。                                                                                                                                                                                                                                                                                                                                                                                                                 |
