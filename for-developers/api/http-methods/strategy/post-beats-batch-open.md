# POST beats/batch-open

Beats batch open — up to **25** cells per request; batch-level `symbol`, `margin`, `clientOrderId`.

```
POST /v1/private/beats/batch-open
```

#### Request Body

| Field               | Type      | Required | Description             |
| ------------------- | --------- | -------- | ----------------------- |
| `symbol`            | string    | Yes      | e.g. `BTC-USD`.         |
| `margin`            | string    | Yes      | Per-cell margin (USDC). |
| `clientOrderId`     | string    | Yes      | Batch idempotency key.  |
| `items`             | object\[] | Yes      | Up to 25 cells.         |
| `items[].beginTime` | integer   | Yes      | Window start (Unix ms). |
| `items[].endTime`   | integer   | Yes      | Window end (Unix ms).   |
| `items[].priceMin`  | string    | Yes      | Price band lower bound. |
| `items[].priceMax`  | string    | Yes      | Price band upper bound. |

#### Response — `data`

| Field           | Type      | Description                                                                                 |
| --------------- | --------- | ------------------------------------------------------------------------------------------- |
| `clientOrderId` | string    | Batch idempotency key.                                                                      |
| `summary`       | object    | Counts: `requested`, `succeeded`, `failed`, `replayed`, `newOpened`, `totalMarginDeducted`. |
| `results[]`     | object\[] | One entry per `items[]` element.                                                            |

#### Errors (batch-level, non-2xx)

| HTTP | Code                                          | Meaning                      |
| ---- | --------------------------------------------- | ---------------------------- |
| 400  | `BEATS_BAD_REQUEST` / `BEATS_BATCH_TOO_LARGE` | Invalid params or >25 cells. |
| 403  | `BEATS_NOT_FOUND`                             | Account not found.           |
| 409  | `BEATS_INSUFFICIENT_FUNDS`                    | Insufficient balance.        |
| 409  | `BEATS_REQUEST_IN_PROGRESS`                   | In-flight `clientOrderId`.   |
| 503  | `LITEOPTION_PRICE_UNAVAILABLE`                | Oracle mark unavailable.     |

Per-cell errors (HTTP 200): see `results[].code` (`BEATS_CELL_NOT_FOUND`, etc.).
