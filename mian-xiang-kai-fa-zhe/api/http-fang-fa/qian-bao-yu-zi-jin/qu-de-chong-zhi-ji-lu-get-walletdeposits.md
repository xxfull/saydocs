---
description: 查詢某地址的充值記錄。
---

# 取得充值記錄（GET /wallet/deposits）

```
GET /v1/public/exchange/wallet/deposits
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

| 欄位                                  | 類型         | 說明                                                                                                                          |
| ----------------------------------- | ---------- | --------------------------------------------------------------------------------------------------------------------------- |
| `data`                              | object     | 查詢結果。                                                                                                                       |
| `data.items`                        | object \[] | 充值記錄列表。                                                                                                                     |
| `data.items.amount`                 | string     | 充值金額，以十進位字串表示。                                                                                                              |
| `data.items.asset`                  | string     | 資產符號。                                                                                                                       |
| `data.items.chain`                  | string     | 鏈 ID，為小寫 slug，來源於 `onchain_deposits.chain` / `withdraw_requests.chain`。支援值以 Explorer 錢包 API 文件為準。                           |
| `data.items.confirmations`          | integer    | 目前確認數。                                                                                                                      |
| `data.items.created_at`             | string     | 記錄建立時間，UTC。                                                                                                                 |
| `data.items.id`                     | string     | 充值記錄 ID。                                                                                                                    |
| `data.items.ledger_tx_id`           | string     | 為該充值建立的帳本分錄 ID。                                                                                                             |
| `data.items.log_index`              | integer    | 該交易中的事件日誌索引。                                                                                                                |
| `data.items.required_confirmations` | integer    | 所需確認數門檻。                                                                                                                    |
| `data.items.source_tx_hash`         | string     | 原始鏈上充值交易雜湊。                                                                                                                 |
| `data.items.status`                 | string     | 錢包 API 對 `onchain_deposits.status` 的標準化結果。目前只會返回 `credited` 或 `confirming`，其中也包含鏈上偵測、入帳等未終態，以及像 `detected`、`ignored` 等來源狀態。 |
| `data.items.tx_hash`                | string     | 充值帳本交易雜湊，由 `ledger_tx_id` 派生。                                                                                               |
| `data.next_cursor`                  | string     | 下一頁的不透明游標。空字串表示沒有下一頁。                                                                                                       |
| `success`                           | boolean    | 請求是否成功。                                                                                                                     |
