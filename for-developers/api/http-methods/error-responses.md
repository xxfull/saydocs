---
metaLinks:
  alternates:
    - >-
      https://app.gitbook.com/s/KiKbOTrmqLWnXHD7ZyeJ/mian-xiang-kai-fa-zhe/api/http-fang-fa/cuo-wu-hui-ying
---

# Error responses

### Unified JSON envelope (`Response`)

YesFi HTTP APIs use the same struct

#### Success

| Field     | Type                     | Description                          |
| --------- | ------------------------ | ------------------------------------ |
| `success` | `boolean`                | `true`                               |
| `data`    | `object` \| `array` \| … | Business payload (optional if empty) |
| `code`    | `string`                 | Usually omitted on success           |
| `message` | `string`                 | Usually omitted on success           |

#### Error

| Field     | Type      | Description                                                                                                                        |
| --------- | --------- | ---------------------------------------------------------------------------------------------------------------------------------- |
| `success` | `boolean` | `false`                                                                                                                            |
| `code`    | `string`  | Machine-readable code, typically `UPPER_SNAKE_CASE`. **Clients should branch on `code`**, not on `message` text.                   |
| `message` | `string`  | Short, safe English description for humans. **Not** a stable API contract—wording may change; no stack traces or internal details. |
| `data`    | —         | Omitted for standard errors                                                                                                        |

Example:

```json
{
  "success": true,
  "data": {
    "orderId": "01HZ...",
    "status": "open"
  }
}
{
  "success": false,
  "code": "GATEWAY_NO_UPSTREAM_ROUTE",
  "message": "no matching route"
}
```

***

### HTTP status

HTTP status is chosen per scenario; **multiple `code` values can share one status** (e.g. several auth failures → `401`).

| HTTP  | Typical `code` values (non-exhaustive)                                                                                                                   |
| ----- | -------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `400` | `INVALID_SIGNATURE` (e.g. JSON bind failure on verify endpoint)                                                                                          |
| `401` | `INVALID_SIGNATURE`, `EXPIRED_REQUEST`, `TIMESTAMP_REUSED`, `INTERNAL_AUTH_FAILED`, `INTERNAL_AUTH_REPLAYED`, `GATEWAY_MISSING_AUTHENTICATED_ADDRESS`, … |
| `403` | `AUTH_BLACKLISTED`                                                                                                                                       |
| `404` | `GATEWAY_NO_UPSTREAM_ROUTE`, `GATEWAY_ROUTE_NOT_OWNED`                                                                                                   |
| `429` | `GATEWAY_IP_RATE_LIMITED`, `AUTH_RATE_LIMITED`, `AUTH_DUPLICATE_REQUEST`                                                                                 |
| `502` | `GATEWAY_UPSTREAM_SIGN_FAILED`                                                                                                                           |
| `503` | `GATEWAY_DEPENDENCY_UNAVAILABLE`, `AUTH_DEPENDENCY_UNAVAILABLE`                                                                                          |

***

### ErrorCode

| `code`                      | Typical meaning                                               |
| --------------------------- | ------------------------------------------------------------- |
| `INTERNAL_AUTH_FAILED`      | Internal HMAC / auth failed (`unauthorized`).                 |
| `INTERNAL_AUTH_UNAVAILABLE` | Internal auth dependency unavailable.                         |
| `INVALID_REQUEST`           | Malformed or invalid request parameters.                      |
| `INVALID_MARKET`            | Unknown or disallowed market.                                 |
| `INVALID_LIMIT`             | Bad `limit` query/body.                                       |
| `INVALID_TIME_RANGE`        | Invalid time window.                                          |
| `INVALID_DIRECTION`         | Invalid sort or trade direction filter.                       |
| `INVALID_ACCOUNT_ID`        | Bad account identifier.                                       |
| `INVALID_OFFSET`            | Bad offset / pagination.                                      |
| `TOO_MANY_ADDRESSES`        | Public multi-address query exceeds cap (e.g. > 20).           |
| `INVALID_STATUS`            | Invalid status filter.                                        |
| `INVALID_TYPE`              | Invalid type discriminator.                                   |
| `INVALID_HEIGHT`            | Invalid block height parameter.                               |
| `INVALID_PAGE`              | Invalid page parameter.                                       |
| `INVALID_ORDER_ID`          | Malformed order id.                                           |
| `INVALID_REQUEST_ID`        | Malformed request id.                                         |
| `BAD_REQUEST`               | Generic bad request (`bad_request`).                          |
| `FORBIDDEN`                 | Authenticated but not allowed.                                |
| `NOT_FOUND`                 | Resource missing.                                             |
| `SERVICE_UNAVAILABLE`       | Dependency unavailable (`service_unavailable`).               |
| `INTERNAL_SERVER_ERROR`     | Generic server error mapping.                                 |
| `INVALID_SIGNATURE`         | Signature verification failed.                                |
| `INVALID_ADDRESS`           | EVM address validation failed (messages prefixed `address` ). |

***

| `code`                             | Triggering handler message (normalized)                             |
| ---------------------------------- | ------------------------------------------------------------------- |
| `INVALID_JSON`                     | `invalid json` / `invalid_json`                                     |
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
| `READ_BODY_FAILED`                 | `read body` / `failed to read request body`                         |
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
| `BATCH_SIZE_EXCEEDED`              | Message prefix `batch size exceeds`                                 |

| `code`                                       | Condition (substring match on normalized message)             |
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
| `TRADING_ERROR`                              | Other `trading:` messages (message text trimmed after prefix) |

| `code`                       | Notes                                                   |
| ---------------------------- | ------------------------------------------------------- |
| `PRICING_OR_DB_UNCONFIGURED` | Quote/purchase deps not configured (`503` in spec).     |
| `INS_001`                    | Position not found.                                     |
| `INS_004`                    | Leverage outside insurable range.                       |
| `INS_005`                    | Active policy already exists for position.              |
| `INS_011`                    | Global insurance switch / circuit breaker.              |
| `INS_013`                    | Policy not found.                                       |
| `INS_015`                    | Invalid duration (hours).                               |
| `INS_018`                    | Unsupported insurance type.                             |
| `INS_019`                    | Invalid premium / position parameters.                  |
| `INS_020`                    | Insurance not available for token.                      |
| `INS_021`                    | Insurance type not available for token.                 |
| `INS_022`                    | Agreement not accepted.                                 |
| `INS_024`                    | Invalid `premiumLimit`.                                 |
| `INS_030`                    | Premium limit exceeded.                                 |
| `INS_032`                    | Insufficient balance for premium.                       |
| `INS_034`                    | No active policy for renew.                             |
| `INS_035`                    | Invalid insurance mode.                                 |
| `INS_038`                    | Renew requires settled prior policy.                    |
| `INS_049`                    | Market exposure capacity exceeded.                      |
| `INS_050`                    | Market daily written capacity exceeded.                 |
| `INS_054`                    | Policy not refundable.                                  |
| `INS_056`                    | Refund blocked by risk control.                         |
| `INS_057`                    | `acceptUnlimitedPremium` conflicts with `premiumLimit`. |
