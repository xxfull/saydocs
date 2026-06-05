# 誤充取回（POST wallet/recovery）

誤充错誤的 ERC20 token取回。

須經 gateway 以 EIP-712 簽名存取（`X-Address`、`X-Signature`、`X-Signature-Type`、`X-Timestamp`、`X-Eip712-Chain-Id`）。

```
POST /v1/private/exchange/wallet/recovery
```

#### Request Body

| Field          | Type   | Required | Description                      |
| -------------- | ------ | -------- | -------------------------------- |
| `chain`        | string | Yes      | 取回目標鏈識別符（小寫）；須在服務端允許列表中。         |
| `token`        | string | Yes      | 誤充 token 在目標鏈上的合約地址；須為有效 EVM 地址。 |
| `dest_address` | string | No       | 取回目的地址；省略時預設為 caller 地址。         |

#### Response

```json
{
  "success": true,
  "data": {
    "chain": "bsc",
    "token": "0x55d398326f99059ff775485246999027b3197955",
    "deposit_address": "0xc1144a95fa623d7076ecc65ee8104c6c0cffe7fc",
    "dest_address": "0x4a7bbd82b7dd6ce9a810e430b292815138bb420c",
    "amount": "100.5",
    "fee": "2",
    "symbol": "USDT",
    "decimals": 18,
    "accepted": true
  }
}
```

#### Response Fields

| Field                  | Type    | Description                  |
| ---------------------- | ------- | ---------------------------- |
| `success`              | boolean | 成功時固定為 `true`。               |
| `data`                 | object  |                              |
| `data.chain`           | string  | 歸一化後的鏈識別符。                   |
| `data.token`           | string  | token 合約地址。                  |
| `data.deposit_address` | string  | 誤充資金所在的鏈上充值地址。               |
| `data.dest_address`    | string  | 取回目的地址。                      |
| `data.amount`          | string  | 可取回 token 數量（十進位字串）。         |
| `data.fee`             | string  | 取回手續費，計價資產單位（十進位字串）。         |
| `data.symbol`          | string  | token 展示符號。                  |
| `data.decimals`        | integer | token 精度。                    |
| `data.accepted`        | boolean | 是否已被 chain-sync 受理（尚未到鏈上終態）。 |

#### Errors

| HTTP | Code                                | Description                                  |
| ---- | ----------------------------------- | -------------------------------------------- |
| 400  | `SVC_CORE_INVALID_CHAIN`            | `chain` 缺失或無效。                               |
| 400  | `SVC_CORE_UNSUPPORTED_CHAIN`        | 鏈不在允許列表中。                                    |
| 400  | `SVC_CORE_INVALID_TOKEN_ADDRESS`    | `token` 缺失或非有效 EVM 地址。                       |
| 400  | `SVC_CORE_INVALID_DEST_ADDRESS`     | `dest_address` 非有效 EVM 地址。                   |
| 400  | `SVC_CORE_INSUFFICIENT_BALANCE`     | USDC 餘額不足以支付取回手續費。                           |
| 401  | —                                   | EIP-712 簽名缺失或無效。                             |
| 404  | `SVC_CORE_ACCOUNT_NOT_FOUND`        | 找不到 caller 地址對應帳戶。                           |
| 409  | `SVC_CORE_RECOVERY_IN_PROGRESS`     | 該鏈與 token 已有進行中的取回請求。                        |
| 502  | `SVC_CORE_RECOVERY_INVALID_FEE`     | 上游回傳無效手續費。                                   |
| 503  | `SVC_CORE_RECOVERY_NOT_CONFIGURED`  | 取回服務未配置。                                     |
| 503  | `SVC_CORE_RECOVERY_EXECUTE_PENDING` | execute 結果不確定，請求保留於 `pending_execute`，請稍後重試。 |

其他 chain-sync 錯誤碼可能原樣轉發其 `code` 與 `message`。
