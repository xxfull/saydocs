# 錯誤回應

### 統一 JSON 回應結構（`Response`）

YesFi HTTP API 使用統一的回應結構。

#### 成功回應

| 欄位        | 型別                       | 說明           |
| --------- | ------------------------ | ------------ |
| `success` | `boolean`                | 固定为 `true`。  |
| `data`    | `object` \| `array` \| … | 業務資料。為空時可省略。 |
| `code`    | `string`                 | 成功時通常省略。     |
| `message` | `string`                 | 成功時通常省略。     |

#### 錯誤回應

| 欄位        | 型別        | 說明                                                                     |
| --------- | --------- | ---------------------------------------------------------------------- |
| `success` | `boolean` | 固定為 `false`。                                                           |
| `code`    | `string`  | 機器可讀錯誤碼，通常使用 `UPPER_SNAKE_CASE`。**用戶端應基於 `code` 分支處理**，不要依賴 `message`。 |
| `message` | `string`  | 面向人的簡短說明。它不是穩定協議的一部分，文案可能變動，也不會暴露堆疊或內部細節。                              |
| `data`    | —         | 標準錯誤場景通常省略。                                                            |

範例：

成功回應：

```json
{
  "success": true,
  "data": {
    "orderId": "01HZ...",
    "status": "open"
  }
}
```

錯誤回應：

```json
{
  "success": false,
  "code": "GATEWAY_NO_UPSTREAM_ROUTE",
  "message": "no matching route"
}
```

***

### HTTP 狀態碼

HTTP 狀態碼會依場景返回。**多個 `code` 可能共用同一個狀態碼**，例如多種驗權失敗都可能返回 `401`。

| HTTP  | 典型 `code` 值（非完整清單）                                                                                                                                 |
| ----- | -------------------------------------------------------------------------------------------------------------------------------------------------- |
| `400` | `INVALID_SIGNATURE`，例如验签接口的 JSON 绑定失败                                                                                                              |
| `401` | `INVALID_SIGNATURE`、`EXPIRED_REQUEST`、`TIMESTAMP_REUSED`、`INTERNAL_AUTH_FAILED`、`INTERNAL_AUTH_REPLAYED`、`GATEWAY_MISSING_AUTHENTICATED_ADDRESS` 等 |
| `403` | `AUTH_BLACKLISTED`                                                                                                                                 |
| `404` | `GATEWAY_NO_UPSTREAM_ROUTE`、`GATEWAY_ROUTE_NOT_OWNED`                                                                                              |
| `429` | `GATEWAY_IP_RATE_LIMITED`、`AUTH_RATE_LIMITED`、`AUTH_DUPLICATE_REQUEST`                                                                             |
| `502` | `GATEWAY_UPSTREAM_SIGN_FAILED`                                                                                                                     |
| `503` | `GATEWAY_DEPENDENCY_UNAVAILABLE`、`AUTH_DEPENDENCY_UNAVAILABLE`                                                                                     |

***

### 錯誤碼

| `code`                      | 典型含義                                |
| --------------------------- | ----------------------------------- |
| `INTERNAL_AUTH_FAILED`      | 內部 HMAC 或驗權失敗，通常表現為 `unauthorized`。 |
| `INTERNAL_AUTH_UNAVAILABLE` | 內部驗權依賴不可用。                          |
| `INVALID_REQUEST`           | 請求參數格式錯誤或值無效。                       |
| `INVALID_MARKET`            | 市場不存在或不允許存取。                        |
| `INVALID_LIMIT`             | `limit` 查詢參數或請求體欄位非法。               |
| `INVALID_TIME_RANGE`        | 時間範圍無效。                             |
| `INVALID_DIRECTION`         | 排序方向或交易方向篩選值非法。                     |
| `INVALID_ACCOUNT_ID`        | 帳戶識別非法。                             |
| `INVALID_OFFSET`            | 偏移量或分頁參數非法。                         |
| `TOO_MANY_ADDRESSES`        | 公開多地址查詢超出上限，例如超過 20 個地址。            |
| `INVALID_STATUS`            | 狀態篩選值非法。                            |
| `INVALID_TYPE`              | 類型欄位非法。                             |
| `INVALID_HEIGHT`            | 區塊高度參數非法。                           |
| `INVALID_PAGE`              | 頁碼參數非法。                             |
| `INVALID_ORDER_ID`          | 訂單 ID 格式非法。                         |
| `INVALID_REQUEST_ID`        | 請求 ID 格式非法。                         |
| `BAD_REQUEST`               | 通用錯誤請求，訊息常見為 `bad_request`。         |
| `FORBIDDEN`                 | 已驗權，但沒有權限執行。                        |
| `NOT_FOUND`                 | 資源不存在。                              |
| `SERVICE_UNAVAILABLE`       | 依賴不可用，訊息常見為 `service_unavailable`。  |
| `INTERNAL_SERVER_ERROR`     | 通用伺服器端錯誤映射。                         |
| `INVALID_SIGNATURE`         | 簽名校驗失敗。                             |
| `INVALID_ADDRESS`           | EVM 地址校驗失敗，相關訊息通常以前綴 `address` 開頭。  |

***

| `code`                             | 命中的處理器訊息（正規化後）                                                      |
| ---------------------------------- | ------------------------------------------------------------------- |
| `INVALID_JSON`                     | `invalid json` 或 `invalid_json`                                     |
| `DATABASE_ERROR`                   | `database error`                                                    |
| `CHAIN_REQUIRED`                   | `chain is required`                                                 |
| `UNSUPPORTED_CHAIN`                | `unsupported_chain`                                                 |
| `UNSUPPORTED_ASSET`                | `unsupported_asset`                                                 |
| `UNKNOWN_SYMBOL`                   | `unknown_symbol`                                                    |
| `PRICING_UNCONFIGURED`             | `pricing_unconfigured`                                              |
| `PRICING_OR_DB_UNCONFIGURED`       | `pricing_or_db_unconfigured`                                        |
| `DB_UNCONFIGURED`                  | `db_unconfigured`                                                   |
| `ACCOUNT_NOT_FOUND`                | `account not found`                                                 |
| `INSUFFICIENT_BALANCE`             | `insufficient balance`                                              |
| `EMPTY_BATCH`                      | `empty batch`                                                       |
| `SYMBOL_REQUIRED`                  | `symbol required`                                                   |
| `READ_BODY_FAILED`                 | `read body` 或 `failed to read request body`                         |
| `INVALID_MARGIN_MODE`              | `invalid margin_mode`                                               |
| `CHAIN_SYNC_UPSTREAM_FAILED`       | `failed to fetch deposit address from chain-sync`                   |
| `CHAIN_SYNC_UNCONFIGURED`          | `chain-sync deposit address service not configured`                 |
| `INSURANCE_CONFIG_SNAPSHOT_FAILED` | `insurance_config_snapshot_failed`                                  |
| `INSURANCE_CONFIG_LIST_FAILED`     | `insurance_config_list_failed`                                      |
| `FUNDING_EXTERNAL_UNRECOGNIZED`    | `funding_external_unrecognized`                                     |
| `MISSING_KEY`                      | `missing key`                                                       |
| `INVALID_BODY`                     | `invalid body`                                                      |
| `INVALID_JSON_VALUE`               | `value must be non-empty valid json`                                |
| `TRANSFER_SELF_FORBIDDEN`          | `cannot transfer to self`                                           |
| `CLIENT_WITHDRAW_ID_CONFLICT`      | `client_withdraw_id already used with different request parameters` |
| `WITHDRAW_LEDGER_FAILED`           | `failed to create withdraw hold ledger entries`                     |
| `REQUEST_TIMEOUT`                  | `request timeout`                                                   |
| `DATABASE_UNAVAILABLE`             | `database temporarily unavailable`                                  |
| `INSURANCE_UPSTREAM_FAILED`        | `insurance service temporarily unavailable`                         |
| `TRADING_UPSTREAM_FAILED`          | `trading service temporarily unavailable`                           |
| `TRANSFER_UPSTREAM_FAILED`         | `transfer service temporarily unavailable`                          |
| `WITHDRAW_UPSTREAM_FAILED`         | `withdraw service temporarily unavailable`                          |
| `WITHDRAW_WHITELIST_UNAVAILABLE`   | `withdraw caller whitelist unavailable`                             |
| `WITHDRAW_LEDGER_UNAVAILABLE`      | `withdraw ledger temporarily unavailable`                           |
| `DEPOSIT_UPSTREAM_FAILED`          | `deposit service temporarily unavailable`                           |
| `FUNDS_CONFIG_UNAVAILABLE`         | `funds configuration unavailable`                                   |
| `ACCOUNT_RESOLUTION_UNAVAILABLE`   | `account resolution temporarily unavailable`                        |
| `WITHDRAW_CALLER_NOT_WHITELISTED`  | `caller is not allowed to withdraw`                                 |
| `BATCH_SIZE_EXCEEDED`              | 消息以前缀 `batch size exceeds` 开头                                       |

| `code`                                       | 命中條件（基於正規化訊息的子字串匹配）                                           |
| -------------------------------------------- | ------------------------------------------------------------- |
| `ORDER_NOT_FOUND`                            | `order not found`                                             |
| `ORDER_NOT_OPEN`                             | `order not open`                                              |
| `ORDER_WRONG_OWNER`                          | `order wrong owner`                                           |
| `ORDER_NOT_MARKETABLE`                       | `order not marketable`                                        |
| `INSUFFICIENT_FUNDS`                         | `insufficient user_balance`                                   |
| `OPEN_POSITION_MARGIN_TOO_SMALL`             | `open position margin is below minimum allowed`               |
| `POSITION_NOT_FOUND`                         | `position not found`                                          |
| `POSITION_PROTECTION_NOT_FOUND`              | `position protection not found`                               |
| `CLOSE_QUANTITY_INVALID`                     | `close quantity invalid`                                      |
| `PARTIAL_CLOSE_ID_REQUIRED`                  | `client_close_id`                                             |
| `ORDER_NOT_CANCELLABLE`                      | `order cannot be cancelled`                                   |
| `RISK_MAINTENANCE_MARGIN`                    | `post-trade position below maintenance`                       |
| `CONDITIONAL_ORDER_NOT_EXECUTABLE`           | `stop_loss/take_profit orders are triggered`                  |
| `NO_POSITION_FOR_CONDITIONAL`                | `conditional order requires an open position`                 |
| `POSITION_TOO_SMALL_FOR_CONDITIONAL`         | `open position size is less than`                             |
| `LEVERAGE_NOT_POSITIVE`                      | `leverage must be positive`                                   |
| `LEVERAGE_EXCEEDS_CAP`                       | `leverage exceeds maximum`                                    |
| `LEVERAGE_PRECISION`                         | `leverage must be a positive integer`                         |
| `LEVERAGE_FORBIDDEN_FOR_CONDITIONAL`         | `leverage is not applicable`                                  |
| `MARGIN_MODE_FORBIDDEN_WITH_POSITIONS`       | `cannot change margin_mode while positions are open`          |
| `MARGIN_ADJUST_REQUIRES_ISOLATED`            | `margin adjustment is only supported for isolated`            |
| `LEVERAGE_ADJUST_REQUIRES_ISOLATED`          | `leverage adjustment is only supported for isolated`          |
| `CLOSE_MARK_EXPIRED`                         | `close mark snapshot expired`                                 |
| `PROTECTION_STOP_LOSS_NOT_BELOW_ENTRY`       | `stop-loss price must be strictly below entry price`          |
| `PROTECTION_STOP_LOSS_NOT_ABOVE_LIQUIDATION` | `stop-loss price must be strictly above liquidation price`    |
| `PROTECTION_TAKE_PROFIT_NOT_ABOVE_ENTRY`     | `take-profit price must be strictly above entry price`        |
| `PROTECTION_STOP_LOSS_NOT_ABOVE_ENTRY`       | `stop-loss price must be strictly above entry price`          |
| `PROTECTION_STOP_LOSS_NOT_BELOW_LIQUIDATION` | `stop-loss price must be strictly below liquidation price`    |
| `PROTECTION_TAKE_PROFIT_NOT_BELOW_ENTRY`     | `take-profit price must be strictly below entry price`        |
| `PROTECTION_LIQUIDATION_PRICE_UNAVAILABLE`   | `liquidation price is unavailable; cannot validate stop-loss` |
| `TRADING_ERROR`                              | 其他以 `trading:` 开头的消息，消息体会去掉此前缀                                |

| `code`                       | 說明                                            |
| ---------------------------- | --------------------------------------------- |
| `PRICING_OR_DB_UNCONFIGURED` | 報價或購買依賴未配置，規範中通常對應 `503`。                     |
| `INS_001`                    | 倉位不存在。                                        |
| `INS_004`                    | 槓桿不在可投保範圍內。                                   |
| `INS_005`                    | 該倉位已存在有效保單。                                   |
| `INS_011`                    | 命中全域保險開關或熔斷。                                  |
| `INS_013`                    | 保單不存在。                                        |
| `INS_015`                    | 時長參數非法，單位為小時。                                 |
| `INS_018`                    | 不支援的保險類型。                                     |
| `INS_019`                    | 保費或倉位參數非法。                                    |
| `INS_020`                    | 該代幣暫不支援保險。                                    |
| `INS_021`                    | 該代幣暫不支援目前保險類型。                                |
| `INS_022`                    | 尚未接受保險協議。                                     |
| `INS_024`                    | `premiumLimit` 非法。                            |
| `INS_030`                    | 保費超過上限。                                       |
| `INS_032`                    | 支付保費餘額不足。                                     |
| `INS_034`                    | 續保時未找到有效保單。                                   |
| `INS_035`                    | 保險模式非法。                                       |
| `INS_038`                    | 續保前要求前一張保單已結算。                                |
| `INS_049`                    | 市場風險敞口容量超限。                                   |
| `INS_050`                    | 市場日承保容量超限。                                    |
| `INS_054`                    | 目前保單不可退費。                                     |
| `INS_056`                    | 風控阻止退費。                                       |
| `INS_057`                    | `acceptUnlimitedPremium` 與 `premiumLimit` 衝突。 |
