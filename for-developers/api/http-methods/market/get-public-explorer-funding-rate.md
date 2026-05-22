---
metaLinks:
  alternates:
    - >-
      https://app.gitbook.com/s/KiKbOTrmqLWnXHD7ZyeJ/mian-xiang-kai-fa-zhe/api/http-fang-fa/shi-chang/qu-de-zi-jin-feilget-publicexplorerfundingrate
---

# GET public/exchange/funding-rate

```
GET /v1/public/exchange/funding-rate
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
    "fundingRate": "...",
    "symbol": "..."
  }
}
```

#### Response Fields

| Field              | Type    | Description                       |
| ------------------ | ------- | --------------------------------- |
| `data`             | object  |                                   |
| `data.fundingRate` | string  | Funding rate as a decimal string. |
| `data.symbol`      | string  | Full market symbol.               |
| `success`          | boolean |                                   |
