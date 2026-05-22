---
description: Mark price for one market.
metaLinks:
  alternates:
    - >-
      https://app.gitbook.com/s/KiKbOTrmqLWnXHD7ZyeJ/mian-xiang-kai-fa-zhe/api/http-fang-fa/shi-chang/qu-de-biao-ji-jia-ge-get-publicexplorermarkprice
---

# GET public/exchange/mark-price

```
GET /v1/public/exchange/mark-price
```

#### Query Parameters

| Parameter | Required | Description |
| --------- | -------- | ----------- |
| `market`  | Yes      |             |

#### Response

```json
{
  "success": true,
  "data": {
    "price": "...",
    "symbol": "..."
  }
}
```

#### Response Fields

| Field         | Type    | Description                                                                                        |
| ------------- | ------- | -------------------------------------------------------------------------------------------------- |
| `data`        | object  |                                                                                                    |
| `data.price`  | string  | mark price, represented by decimal string; truncated by the market \`pxDecimals' without rounding. |
| `data.symbol` | string  | Full market symbol.                                                                                |
| `success`     | boolean |                                                                                                    |
