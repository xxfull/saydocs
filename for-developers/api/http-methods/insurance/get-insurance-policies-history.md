---
metaLinks:
  alternates:
    - >-
      https://app.gitbook.com/s/KiKbOTrmqLWnXHD7ZyeJ/mian-xiang-kai-fa-zhe/api/http-fang-fa/bao-xian/qu-de-li-shi-bao-dan-get-insurancepolicieshistory
---

# GET insurance/policies/history

List non-active (historical) policies for the current user.

```
GET /v1/public/insurance/policies/history
```

#### Query Parameters

| Parameter      | Required | Default | Description                                 |
| -------------- | -------- | ------- | ------------------------------------------- |
| `symbol`       | No       | —       | Filter by symbol                            |
| `limit`        | No       | 20      | Max 200                                     |
| `offset`       | No       | 0       | Pagination offset                           |
| `expireAtFrom` | No       | —       | Lower bound for `expire_at` (ms, inclusive) |
| `expireAtTo`   | No       | —       | Upper bound for `expire_at` (ms, inclusive) |

***
