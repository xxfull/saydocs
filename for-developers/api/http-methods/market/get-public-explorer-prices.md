---
description: Latest prices for supported markets.
metaLinks:
  alternates:
    - >-
      https://app.gitbook.com/s/KiKbOTrmqLWnXHD7ZyeJ/mian-xiang-kai-fa-zhe/api/http-fang-fa/shi-chang/qu-de-zui-xin-jia-ge-get-publicexplorerprices
---

# GET public/exchange/prices

```
GET /v1/public/exchange/prices
```

No query parameters required.

#### Response

```json
{
  "success": true,
  "data": {}
}
```

#### Response Fields

| Field     | Type    | Description                                                                                                                  |
| --------- | ------- | ---------------------------------------------------------------------------------------------------------------------------- |
| `data`    | object  | Map from full symbol to latest price decimal string. Prices are cut off and not rounded to the nearest market \`pxDecimals'. |
| `success` | boolean |                                                                                                                              |
