# 取得訂單詳情（GET /exchange/orders/{id}）

```
GET /v1/private/exchange/orders/{id}
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
    "executed_at": "...",
    "execution_price": "...",
    "execution_slippage_bps": "...",
    "filled_quantity": "...",
    "fills": [],
    "limit_price": "...",
    "mark_price": "...",
    "order_id": "...",
    "order_type": "...",
    "position_uid": "...",
    "quantity": "...",
    "reason": "...",
    "remaining_quantity": "...",
    "reserve_remaining": "...",
    "side": "...",
    "status": "...",
    "stop_loss_price": "...",
    "stop_loss_quantity": "...",
    "symbol": "...",
    "take_profit_price": "...",
    "take_profit_quantity": "...",
    "trigger_price": "..."
  }
}
```

#### 回應欄位

| 欄位                                  | 類型         | 說明                                                                             |
| ----------------------------------- | ---------- | ------------------------------------------------------------------------------ |
| `data`                              | object     | 訂單詳情結構，包含成交列表。                                                                 |
| `data.executed_at`                  | string     | 成交時間，UTC。                                                                      |
| `data.execution_price`              | string     | 成交價格，以十進位字串表示；依 `pxDecimals` 截斷。                                               |
| `data.execution_slippage_bps`       | string     | 本次執行使用的滑點，以基點表示，為十進位字串。                                                        |
| `data.filled_quantity`              | string     | 累計成交數量，以十進位字串表示；依 `szDecimals` 截斷。                                             |
| `data.fills`                        | object \[] | 成交列表，順序以伺服器端實作為準。                                                              |
| `data.fills.execution_slippage_bps` | string     | 本筆成交使用的滑點參數，以基點表示，為十進位字串。                                                      |
| `data.fills.fee`                    | string     | 手續費，以十進位字串表示；按計價資產截斷為 8 位小數。                                                   |
| `data.fills.id`                     | string     | 成交 ID。                                                                         |
| `data.fills.ledger_tx_id`           | string     | 對應此成交的帳本流水 ID。                                                                 |
| `data.fills.mark_price`             | string     | 本筆成交使用的標記價格快照，以十進位字串表示；依 `pxDecimals` 截斷。                                      |
| `data.fills.price`                  | string     | 成交價格，以十進位字串表示；依 `pxDecimals` 截斷。                                               |
| `data.fills.quantity`               | string     | 成交數量，以十進位字串表示；依 `szDecimals` 截斷。                                               |
| `data.limit_price`                  | string     | 限價價格，以十進位字串表示；依 `pxDecimals` 截斷。                                               |
| `data.mark_price`                   | string     | 執行時的標記價格快照，以十進位字串表示；依 `pxDecimals` 截斷。                                         |
| `data.order_id`                     | string     | 訂單 ID。                                                                         |
| `data.order_type`                   | string     | 訂單類型。                                                                          |
| `data.position_uid`                 | string     | 關聯倉位的 `position_uid`；僅在訂單綁定倉位時返回。                                              |
| `data.quantity`                     | string     | 原始訂單數量，以十進位字串表示；依 `szDecimals` 截斷。                                             |
| `data.reason`                       | string     | 訂單成交或關閉原因，例如 `user`、`take_profit`、`stop_loss`、`insurance`、`adl`、`liquidation`。 |
| `data.remaining_quantity`           | string     | `quantity - filled_quantity` 的結果，以十進位字串表示；依 `szDecimals` 截斷。                   |
| `data.reserve_remaining`            | string     | 剩餘預留金額，以十進位字串表示；按計價資產截斷為 8 位小數。                                                |
| `data.side`                         | string     | 訂單方向。                                                                          |
| `data.status`                       | string     | 目前訂單狀態。                                                                        |
| `data.stop_loss_price`              | string     | 來自主訂單或歷史資料的止損觸發價，以十進位字串表示；依 `pxDecimals` 截斷。                                   |
| `data.stop_loss_quantity`           | string     | 來自主訂單的止損數量，以十進位字串表示；依 `szDecimals` 截斷。                                         |
| `data.symbol`                       | string     | 完整市場交易對。                                                                       |
| `data.take_profit_price`            | string     | 來自主訂單或歷史資料的止盈觸發價，以十進位字串表示；依 `pxDecimals` 截斷。                                   |
| `data.take_profit_quantity`         | string     | 來自主訂單的止盈數量，以十進位字串表示；依 `szDecimals` 截斷。                                         |
| `data.trigger_price`                | string     | 條件單的歷史觸發價，以十進位字串表示；依 `pxDecimals` 截斷；舊版欄位。                                     |
| `success`                           | boolean    | 請求是否成功。                                                                        |
