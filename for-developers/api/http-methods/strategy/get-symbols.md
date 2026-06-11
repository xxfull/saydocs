# GET symbols

List enabled symbols for **flash** **option（trend）**.

```
GET /v1/public/trend/symbols
```

#### Response

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
          "pricing_params_key": "trend_default",
          "tiers": {}
        }
      }
    ]
  }
}
```

#### Response Fields — `data.items[]`

| Field                       | Type       | Description                            |
| --------------------------- | ---------- | -------------------------------------- |
| `symbol`                    | string     | Symbol identifier, e.g. `BTC-USD`.     |
| `trading_session`           | string     | Trading session, e.g. `24x7`.          |
| `duration_opts`             | integer\[] | Supported hold durations (seconds).    |
| `config`                    | object     | Business config (`SymbolExtraConfig`). |
| `config.house_edge`         | string     | House edge ratio (decimal string).     |
| `config.min_margin`         | string     | Minimum margin (USDC).                 |
| `config.max_margin`         | string     | Maximum margin (USDC).                 |
| `config.pricing_params_key` | string     | Pricing params cache key.              |
| `config.tiers`              | object     | Tier → amplitude map.                  |

#### Errors

| HTTP | Code             | Meaning                              |
| ---- | ---------------- | ------------------------------------ |
| 500  | `COMBO_INTERNAL` | Server error (Redis/DB unavailable). |
