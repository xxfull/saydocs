---
metaLinks:
  alternates:
    - >-
      https://app.gitbook.com/s/KiKbOTrmqLWnXHD7ZyeJ/mian-xiang-kai-fa-zhe/api/http-fang-fa/shi-chang/qu-de-jiao-yi-dui-lie-biao-get-publicexplorersymbols
---

# GET public/exchange/symbols

Returns the list of trading pairs visible in the Explorer, with optional fuzzy filtering.

```
GET /v1/public/exchange/symbols
```

### Query Parameters

| Parameter | Required | Description                                                                                                                                                                                      |
| --------- | -------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| `query`   | No       | Fuzzy filter by base asset or full symbol. Supports repeated `query` params for OR filtering. Max 20 non-empty values, max 64 chars each. Omitting or passing empty returns all visible symbols. |

### Response

```json
{
  "success": true,
  "data": [
    {
      "name": "BTC-USD",
      "hlCoin": "BTC",
      "mark_price": "65000.5",
      "maxLeverage": 50,
      "openPositionMinMargin": "10",
      "pxDecimals": 1,
      "szDecimals": 4,
      "source": "hyperliquid",
      "tag": "major"
    }
  ]
}
```

#### Response Fields (per item)

| Field                   | Type    | Description                                                                                   |
| ----------------------- | ------- | --------------------------------------------------------------------------------------------- |
| `name`                  | string  | Full market symbol, e.g. `BTC-USD`                                                            |
| `hlCoin`                | string  | Upstream base asset identifier                                                                |
| `mark_price`            | string  | Current mark price (decimal string, truncated to `pxDecimals`). May be absent if unavailable. |
| `maxLeverage`           | integer | Maximum leverage for this symbol (≥ 1)                                                        |
| `openPositionMinMargin` | string  | Minimum margin required to open a position                                                    |
| `pxDecimals`            | integer | Price precision (decimal places)                                                              |
| `szDecimals`            | integer | Quantity precision (decimal places)                                                           |
| `source`                | string  | Upstream data source tag                                                                      |
| `tag`                   | string  | Informational grouping label                                                                  |
