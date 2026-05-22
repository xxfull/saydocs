# 查詢訂單列表（POST  /orders/list）

```
POST /v1/public/exchange/orders/list
```

#### 請求體

| 欄位          | 類型         | 必填 | 說明                                          |
| ----------- | ---------- | -- | ------------------------------------------- |
| `address`   | string     | 否  | 單地址模式下必填。目標 EVM 地址，格式為小寫 `0x` 加 40 位十六進位字元。 |
| `addresses` | string \[] | 否  | 多地址模式。非空時忽略 `address`。去重後最多 20 個地址。         |
| `endTime`   | integer    | 否  | 結束時間，Unix 毫秒，含邊界。                           |
| `limit`     | integer    | 否  | 最大返回筆數。`0` 表示使用伺服器端預設分頁大小。                  |
| `offset`    | integer    | 否  | 分頁偏移，從 0 開始。                                |
| `startTime` | integer    | 否  | 開始時間，Unix 毫秒，含邊界。                           |
| `status`    |            | 否  | 訂單狀態過濾。支援單一字串或字串陣列。                         |
| `symbols`   | string \[] | 否  | 交易對批次過濾，最多 20 個。                            |
| `timeField` | string     | 否  | 用於過濾的時間欄位，預設為 `created_at`。                 |
| `type`      |            | 否  | 訂單類型過濾。支援單一字串或字串陣列。                         |

#### 回應

```json
{
  "success": true,
  "data": {
    "orders": [],
    "total": 0
  }
}
```

#### 回應欄位

| 欄位                                   | 類型         | 說明                                                                             |
| ------------------------------------ | ---------- | ------------------------------------------------------------------------------ |
| `data`                               | object     | 查詢結果。                                                                          |
| `data.orders`                        | object \[] | 訂單列表。                                                                          |
| `data.orders.address`                | string     | 僅在多地址 `/orders` 查詢且請求至少兩個地址時返回；表示該訂單所屬的 EVM 地址，格式為小寫 `0x` 加 40 位十六進位字元。        |
| `data.orders.created_at`             | string     | 訂單建立時間，UTC。                                                                    |
| `data.orders.executed_at`            | string     | 成交時間，UTC。                                                                      |
| `data.orders.execution_price`        | string     | 成交價格，以十進位字串表示；依 `pxDecimals` 截斷。                                               |
| `data.orders.execution_slippage_bps` | string     | 本次執行使用的滑點，以基點表示，為十進位字串。                                                        |
| `data.orders.filled_quantity`        | string     | 成交數量，以十進位字串表示；依 `szDecimals` 截斷。                                               |
| `data.orders.limit_price`            | string     | 限價價格，以十進位字串表示；依 `pxDecimals` 截斷。                                               |
| `data.orders.mark_price`             | string     | 執行時的標記價格快照，以十進位字串表示；依 `pxDecimals` 截斷。                                         |
| `data.orders.order_id`               | string     | 訂單 ID。                                                                         |
| `data.orders.order_type`             | string     | 訂單類型。                                                                          |
| `data.orders.position_uid`           | string     | 關聯倉位的 `position_uid`；僅在訂單綁定倉位時返回。                                              |
| `data.orders.quantity`               | string     | 原始訂單數量，以十進位字串表示；依 `szDecimals` 截斷。                                             |
| `data.orders.reason`                 | string     | 訂單成交或關閉原因，例如 `user`、`take_profit`、`stop_loss`、`insurance`、`adl`、`liquidation`。 |
| `data.orders.remaining_quantity`     | string     | `quantity - filled_quantity` 的結果，以十進位字串表示；依 `szDecimals` 截斷。                   |
| `data.orders.reserve_remaining`      | string     | 剩餘預留金額，以十進位字串表示；按計價資產截斷為 8 位小數。                                                |
| `data.orders.side`                   | string     | 訂單方向。                                                                          |
| `data.orders.status`                 | string     | 目前訂單狀態。                                                                        |
| `data.orders.stop_loss_price`        | string     | 來自主訂單或歷史資料的止損觸發價，以十進位字串表示；依 `pxDecimals` 截斷。                                   |
| `data.orders.stop_loss_quantity`     | string     | 來自主訂單的止損數量，以十進位字串表示；依 `szDecimals` 截斷。                                         |
| `data.orders.symbol`                 | string     | 完整市場交易對。                                                                       |
| `data.orders.take_profit_price`      | string     | 來自主訂單或歷史資料的止盈觸發價，以十進位字串表示；依 `pxDecimals` 截斷。                                   |
| `data.orders.take_profit_quantity`   | string     | 來自主訂單的止盈數量，以十進位字串表示；依 `szDecimals` 截斷。                                         |
| `data.orders.trigger_price`          | string     | 條件單的歷史觸發價，以十進位字串表示；依 `pxDecimals` 截斷；舊版欄位。                                     |
| `data.orders.tx_hash`                | string     | 首筆成交對應的帳本交易雜湊，由其 `ledger_tx_id` 派生；若沒有成交則省略。                                   |
| `data.orders.updated_at`             | string     | 最後更新時間，UTC。                                                                    |
| `data.total`                         | integer    | 目前過濾條件下的總筆數，不受分頁限制。                                                            |
| `success`                            | boolean    | 請求是否成功。                                                                        |
