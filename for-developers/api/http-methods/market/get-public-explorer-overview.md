---
description: Markets overview visible to explorer.
metaLinks:
  alternates:
    - >-
      https://app.gitbook.com/s/KiKbOTrmqLWnXHD7ZyeJ/mian-xiang-kai-fa-zhe/api/http-fang-fa/shi-chang/qu-de-shi-chang-zong-lan-get-publicexploreroverview
---

# GET public/exchange/overview

```
GET /v1/public/exchange/overview
```

No query parameters required.

#### Response

```json
{
  "success": true,
  "data": {
    "fundingRate": "...",
    "openInterest": "...",
    "price": "...",
    "symbol": "..."
  }
}
```

#### Response Fields

| Field               | Type       | Description                                                                                                    |
| ------------------- | ---------- | -------------------------------------------------------------------------------------------------------------- |
| `data`              | object \[] |                                                                                                                |
| `data.fundingRate`  | string     | Current funding rate, using decimal string; `null` when not available.                                         |
| `data.openInterest` | string     | open interest, using decimal string; truncated by `szDecimals` for this market, `null` when not available.     |
| `data.price`        | string     | Latest market price, using decimal string; truncated by `pxDecimals` for this market, `null` when unavailable. |
| `data.symbol`       | string     | Full market symbol.                                                                                            |
| `success`           | boolean    |                                                                                                                |
