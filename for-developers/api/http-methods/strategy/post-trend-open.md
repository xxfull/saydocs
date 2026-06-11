# POST trend/open

Open a **Trend** position.

```
POST /v1/private/trend/open
```

#### Request Body

| Field           | Type    | Required | Description                                                  |
| --------------- | ------- | -------- | ------------------------------------------------------------ |
| `symbol`        | string  | Yes      | Symbol, e.g. `BTC-USD`.                                      |
| `margin`        | string  | Yes      | Margin amount (decimal string).                              |
| `durationSec`   | integer | Yes      | Hold duration in seconds; must be in symbol `duration_opts`. |
| `direction`     | string  | Yes      | `up` or `down`.                                              |
| `tier`          | string  | Yes      | Amplitude tier: `light` / `medium` / `heavy`.                |
| `clientOrderId` | string  | Yes      | User-scoped idempotency key.                                 |

#### Response

On success `data.position` contains open snapshot; `data.replayed=true` on idempotent replay.

#### Errors

| HTTP | Code                                                | Meaning                                |
| ---- | --------------------------------------------------- | -------------------------------------- |
| 400  | `TREND_BAD_REQUEST`                                 | Invalid params or trading constraints. |
| 401  | `TREND_UNAUTHORIZED`                                | Missing or failed auth.                |
| 404  | `TREND_NOT_FOUND` / `TREND_SYMBOL_NOT_FOUND`        | Account or symbol not found.           |
| 409  | `TREND_INSUFFICIENT_FUNDS`                          | Insufficient USDC.                     |
| 429  | `TREND_REQUEST_IN_PROGRESS`                         | In-flight idempotency key.             |
| 503  | `TREND_PRICING_UNAVAILABLE` / `TREND_MARKET_HALTED` | Pricing or market unavailable.         |
| 500  | `TREND_INTERNAL`                                    | Internal server error.                 |
