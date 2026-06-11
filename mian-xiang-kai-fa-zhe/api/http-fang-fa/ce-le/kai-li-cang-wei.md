# 開立倉位

開立 **連擊**（Combo）/ **波動率**（Moves）/ **配對**（Pair）/ **區間**（Range）/ **階梯**（Steps）/ **趨勢**（Trend）倉位。

```
POST /v1/private/combo/open
```

```
POST /v1/private/moves/open
```

```
POST /v1/private/pair/open
```

```
POST /v1/private/range/open
```

```
POST /v1/private/steps/open
```

```
POST /v1/private/trend/open
```

#### Request Body

| 欄位              | 類型      | 必填 | 說明                                       |
| --------------- | ------- | -- | ---------------------------------------- |
| `symbol`        | string  | 是  | 交易對，如 `BTC-USD`。                         |
| `margin`        | string  | 是  | 保證金金額（decimal string）。                   |
| `durationSec`   | integer | 是  | 持倉時長（秒），須在 symbol 配置的 `duration_opts` 內。 |
| `direction`     | string  | 是  | `up` 或 `down`。                           |
| `tier`          | string  | 是  | 振幅檔位：`light` / `medium` / `heavy`。       |
| `clientOrderId` | string  | 是  | 使用者維度冪等鍵。                                |

#### Response

成功時 `data.position` 含開倉快照；`data.replayed=true` 表示冪等重放。

#### Errors

| HTTP | Code                                                | 說明                    |
| ---- | --------------------------------------------------- | --------------------- |
| 400  | `TREND_BAD_REQUEST`                                 | 請求參數非法或交易時段/時長/配置不滿足。 |
| 401  | `TREND_UNAUTHORIZED`                                | 缺少或未通過鑑權 header。      |
| 404  | `TREND_NOT_FOUND` / `TREND_SYMBOL_NOT_FOUND`        | 帳戶或標的不存在。             |
| 409  | `TREND_INSUFFICIENT_FUNDS`                          | USDC 餘額不足。            |
| 429  | `TREND_REQUEST_IN_PROGRESS`                         | 相同冪等鍵請求進行中。           |
| 503  | `TREND_PRICING_UNAVAILABLE` / `TREND_MARKET_HALTED` | 定價或市場狀態不可用。           |
| 500  | `TREND_INTERNAL`                                    | 服務端內部錯誤。              |
