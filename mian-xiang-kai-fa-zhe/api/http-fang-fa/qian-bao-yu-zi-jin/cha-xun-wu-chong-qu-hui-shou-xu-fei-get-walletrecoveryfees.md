# 查詢誤充取回手續費（GET wallet/recovery/fees）

誤充取回各鏈固定手續費與可取回 token 白名單。

```
GET /v1/public/exchange/wallet/recovery/fees
```

無 query 參數。無需認證。

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

| Field                             | Type       | Description                      |
| --------------------------------- | ---------- | -------------------------------- |
| `success`                         | boolean    | 成功時固定為 `true`。                   |
| `data`                            | object     |                                  |
| `data.chains`                     | object \[] | 各鏈手續費與 token 白名單。                |
| `data.chains[].chain`             | string     | 鏈識別符（小寫）。                        |
| `data.chains[].chain_id`          | integer    | EVM chain ID。                    |
| `data.chains[].fee`               | string     | 取回固定手續費，十進位字串（計價資產單位，如 USDC 金額）。 |
| `data.chains[].tokens`            | object \[] | 該鏈上可取回的 token 列表。                |
| `data.chains[].tokens[].address`  | string     | token 合約地址。                      |
| `data.chains[].tokens[].symbol`   | string     | token 展示符號。                      |
| `data.chains[].tokens[].decimals` | integer    | token 精度。                        |

#### Errors

| HTTP | Code                               | Description       |
| ---- | ---------------------------------- | ----------------- |
| 502  | —                                  | 上游 chain-sync 錯誤。 |
| 503  | `SVC_CORE_RECOVERY_NOT_CONFIGURED` | 取回服務未配置。          |
