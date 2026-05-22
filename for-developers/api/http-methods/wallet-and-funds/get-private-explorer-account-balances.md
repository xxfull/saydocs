---
description: Balances by ledger account kind.
metaLinks:
  alternates:
    - >-
      https://app.gitbook.com/s/KiKbOTrmqLWnXHD7ZyeJ/mian-xiang-kai-fa-zhe/api/http-fang-fa/qian-bao-yu-zi-jin/qu-de-zhang-hu-yueget-privateexploreraccountbalances
---

# GET  account/balances

```
GET /v1/private/exchange/account/balances
```

No query parameters required.

#### Response

```json
{
  "success": true,
  "data": {
    "address": "...",
    "asset": "...",
    "by_kind": {}
  }
}
```

#### Response Fields

| Field          | Type    | Description                                              |
| -------------- | ------- | -------------------------------------------------------- |
| `data`         | object  |                                                          |
| `data.address` | string  | The address of the current authentication caller.        |
| `data.asset`   | string  | The quote asset used in this balance view.               |
| `data.by_kind` | object  | Map from internal ledger kind to balance decimal string. |
| `success`      | boolean |                                                          |
