# 查詢產品已啟用交易對列表

查詢 **連擊**（Combo）/ **波動率**（Moves）/ **配對**（Pair）/ **區間**（Range）/ **階梯**（Steps）/ **趨勢**（Trend）產品下所有已啟用的交易對列表。

```
GET /v1/public/combo/symbols
```

```
GET /v1/public/moves/symbols
```

```
GET /v1/public/pair/symbols
```

```
GET /v1/public/range/symbols
```

```
GET /v1/public/steps/symbols
```

```
GET /v1/public/trend/symbols
```

#### Response



**趨勢：**

```json
{
  "success": true,
  "data": {
    "items": [
      {
        "symbol": "BTC-USD",
        "trading_session": "24x7",
        "duration_opts": [30, 60, 180, 300, 600, 900],
        "config": {
          "house_edge": "0.05",
          "min_margin": "1.0",
          "max_margin": "1000.0",
          "pricing_params_key": "trend_default",//combo_default，range_default，steps_default，pair_default，moves_default
          "tiers": {
            "light": { "amplitude_pct": "0.0005", "max_margin": "500.0" },
            "medium": { "amplitude_pct": "0.0012", "max_margin": "500.0" },
            "heavy": { "amplitude_pct": "0.0020", "max_margin": "500.0" }
          }
        }
      }
    ]
  }
}
```

#### Response Fields — `data.items[]`

| Field                       | Type       | Description                                |
| --------------------------- | ---------- | ------------------------------------------ |
| `symbol`                    | string     | 交易對標識，例如 `BTC-USD`。                        |
| `trading_session`           | string     | 交易時段，例如 `24x7`。                            |
| `duration_opts`             | integer\[] | 支援的持倉時長列表（秒）。                              |
| `config`                    | object     | 業務配置；見 OpenAPI `SymbolExtraConfig`。        |
| `config.house_edge`         | string     | 莊家優勢比率（decimal string）。                    |
| `config.min_margin`         | string     | 最小保證金（USDC）。                               |
| `config.max_margin`         | string     | 最大保證金（USDC）。                               |
| `config.pricing_params_key` | string     | 定價參數快取 key。                                |
| `config.tiers`              | object     | 檔位 → 振幅映射（如 `light` / `medium` / `heavy`）。 |

#### Errors

| HTTP | Code             | 說明                      |
| ---- | ---------------- | ----------------------- |
| 500  | `TREND_INTERNAL` | Redis / DB 不可用等服務端內部錯誤。 |



