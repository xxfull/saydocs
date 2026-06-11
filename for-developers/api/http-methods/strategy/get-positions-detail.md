# GET positions/detail

Fetch a single **Trend/Beats** position by `positionId`.

```
GET /v1/public/beats/positions/detail?positionId=<uuid>
```

```
GET /v1/public/trend/positions/detail?positionId=<uuid>
```

#### Query Parameters

| Parameter    | Type   | Required | Description    |
| ------------ | ------ | -------- | -------------- |
| `positionId` | string | Yes      | Position UUID. |

#### Response Fields — `data.position`

| Field                     | Type    | Description            |
| ------------------------- | ------- | ---------------------- |
| `id`                      | string  | Position UUID.         |
| `symbol`                  | string  | Symbol.                |
| `begin_time` / `end_time` | integer | Prediction window.     |
| `price_min` / `price_max` | string  | Price band.            |
| `margin`                  | string  | Margin.                |
| `odds`                    | string  | Odds.                  |
| `status`                  | string  | Position status.       |
| `tx_hash`                 | string  | Open ledger tx hash.   |
| `client_order_id`         | string  | Batch idempotency key. |
| `created_at`              | integer | Created time.          |

#### Errors

| HTTP | Code                | Meaning                          |
| ---- | ------------------- | -------------------------------- |
| 400  | `BEATS_BAD_REQUEST` | Missing or invalid `positionId`. |
| 404  | `BEATS_NOT_FOUND`   | Position not found.              |
| 500  | `BEATS_INTERNAL`    | Server error.                    |
