---
description: Query funding fee events for positions.
---

# POST positions/funding-fees

```
POST /v1/public/exchange/positions/funding-fees
```

Batch query funding fee events by `position_uids`.

#### Request body

| Field           | Type       | Required | Description          |
| --------------- | ---------- | -------- | -------------------- |
| `position_uids` | `string[]` | Yes      | Target position ids. |

#### Response

```json
{
  "success": true,
  "data": {
    "items": [
      {
        "position_uid": "9d3eb3f8-85af-42c5-8aee-56a2b86516f6",
        "total": "-1.85",
        "events": [
          {
            "amount": "-0.92",
            "created_at": "2026-05-21T00:00:00Z"
          },
          {
            "amount": "-0.93",
            "created_at": "2026-05-21T08:00:00Z"
          }
        ]
      },
      {
        "position_uid": "b2c3d4e5-f6a7-8901-bcde-f12345678901",
        "total": "0",
        "events": []
      }
    ]
  }
}
```

#### Response fields

| Field                              | Type       | Description                                     |
| ---------------------------------- | ---------- | ----------------------------------------------- |
| `success`                          | `boolean`  | Request result.                                 |
| `data`                             | `object`   | Response payload.                               |
| `data.items`                       | `object[]` | Funding fee result for each requested position. |
| `data.items[].position_uid`        | `string`   | Position id.                                    |
| `data.items[].total`               | `string`   | Total funding fee amount as decimal string.     |
| `data.items[].events`              | `object[]` | Funding fee events.                             |
| `data.items[].events[].amount`     | `string`   | Funding fee amount as decimal string.           |
| `data.items[].events[].created_at` | `string`   | Event time in UTC.                              |

#### Errors

* `400` — Invalid request parameters.
* `503` — Service unavailable.
