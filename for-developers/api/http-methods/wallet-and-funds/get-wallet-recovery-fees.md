# GET wallet/recovery/fees

Returns per-chain fixed recovery fees and the list of tokens eligible for mis-deposit recovery.&#x20;

```
GET /v1/public/exchange/wallet/recovery/fees
```

No query parameters required. No authentication required.

#### Response

```json
{
  "success": true,
  "data": {
    "chains": [
      {
        "chain": "ethereum",
        "chain_id": 1,
        "fee": "5",
        "tokens": [
          {
            "address": "0xdac17f958d2ee523a2206206994597c13d831ec7",
            "symbol": "USDT",
            "decimals": 6
          }
        ]
      },
      {
        "chain": "bsc",
        "chain_id": 56,
        "fee": "2",
        "tokens": [
          {
            "address": "0x55d398326f99059ff775485246999027b3197955",
            "symbol": "USDT",
            "decimals": 18
          }
        ]
      }
    ]
  }
}
```

#### Response Fields

| Field                             | Type       | Description                                                                     |
| --------------------------------- | ---------- | ------------------------------------------------------------------------------- |
| `success`                         | boolean    | Always `true` on success.                                                       |
| `data`                            | object     |                                                                                 |
| `data.chains`                     | object \[] | Per-chain fee and token allowlist.                                              |
| `data.chains[].chain`             | string     | Chain identifier (lowercase).                                                   |
| `data.chains[].chain_id`          | integer    | EVM chain ID.                                                                   |
| `data.chains[].fee`               | string     | Fixed recovery fee as a decimal string in quote-asset units (e.g. USDC amount). |
| `data.chains[].tokens`            | object \[] | Tokens eligible for recovery on this chain.                                     |
| `data.chains[].tokens[].address`  | string     | Token contract address.                                                         |
| `data.chains[].tokens[].symbol`   | string     | Token display symbol.                                                           |
| `data.chains[].tokens[].decimals` | integer    | Token decimal places.                                                           |

#### Errors

| HTTP | Code                               | Description                         |
| ---- | ---------------------------------- | ----------------------------------- |
| 502  | —                                  | Upstream chain-sync error.          |
| 503  | `SVC_CORE_RECOVERY_NOT_CONFIGURED` | Recovery service is not configured. |
