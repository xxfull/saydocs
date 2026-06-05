# POST wallet/recovery

Initiates recovery of tokens that were deposited to the wrong ERC20 token.&#x20;

Requires EIP-712–signed private access via the gateway (`X-Address`, `X-Signature`, `X-Signature-Type`, `X-Timestamp`, `X-Eip712-Chain-Id`).

```
POST /v1/private/exchange/wallet/recovery
```

#### Request Body

| Field          | Type   | Required | Description                                                                            |
| -------------- | ------ | -------- | -------------------------------------------------------------------------------------- |
| `chain`        | string | Yes      | Target chain identifier (lowercase); must be in the server allowlist.                  |
| `token`        | string | Yes      | Mis-deposited token contract address on the target chain; must be a valid EVM address. |
| `dest_address` | string | No       | Destination address for recovered tokens; defaults to the caller address when omitted. |

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

| Field                  | Type    | Description                                                       |
| ---------------------- | ------- | ----------------------------------------------------------------- |
| `success`              | boolean | Always `true` on success.                                         |
| `data`                 | object  |                                                                   |
| `data.chain`           | string  | Normalized chain identifier.                                      |
| `data.token`           | string  | Token contract address.                                           |
| `data.deposit_address` | string  | On-chain deposit address where the mis-deposited funds reside.    |
| `data.dest_address`    | string  | Destination address for recovered tokens.                         |
| `data.amount`          | string  | Recoverable token amount (decimal string).                        |
| `data.fee`             | string  | Recovery fee charged in quote asset (decimal string).             |
| `data.symbol`          | string  | Token display symbol.                                             |
| `data.decimals`        | integer | Token decimal places.                                             |
| `data.accepted`        | boolean | Whether chain-sync accepted the request (not yet final on-chain). |

#### Errors

| HTTP | Code                                | Description                                                                |
| ---- | ----------------------------------- | -------------------------------------------------------------------------- |
| 400  | `SVC_CORE_INVALID_CHAIN`            | `chain` is missing or invalid.                                             |
| 400  | `SVC_CORE_UNSUPPORTED_CHAIN`        | Chain is not in the allowlist.                                             |
| 400  | `SVC_CORE_INVALID_TOKEN_ADDRESS`    | `token` is missing or not a valid EVM address.                             |
| 400  | `SVC_CORE_INVALID_DEST_ADDRESS`     | `dest_address` is not a valid EVM address.                                 |
| 400  | `SVC_CORE_INSUFFICIENT_BALANCE`     | USDC balance is insufficient to cover the recovery fee.                    |
| 401  | —                                   | Missing or invalid EIP-712 signature.                                      |
| 404  | `SVC_CORE_ACCOUNT_NOT_FOUND`        | No account for the caller address.                                         |
| 409  | `SVC_CORE_RECOVERY_IN_PROGRESS`     | A recovery for this chain and token is already in progress.                |
| 502  | `SVC_CORE_RECOVERY_INVALID_FEE`     | Upstream returned an invalid fee.                                          |
| 503  | `SVC_CORE_RECOVERY_NOT_CONFIGURED`  | Recovery service is not configured.                                        |
| 503  | `SVC_CORE_RECOVERY_EXECUTE_PENDING` | Execute result uncertain; request left in `pending_execute` — retry later. |
