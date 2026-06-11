# beats matrix

### Subscribe request

| Field         | Type      | Required | Description                           |
| ------------- | --------- | -------- | ------------------------------------- |
| `event`       | string    | Yes      | `sub`.                                |
| `topic`       | string    | Yes      | `beats`.                              |
| `symbols`     | string\[] | Yes      | Non-empty; at least one valid symbol. |
| `compression` | integer   | No       | Outbound encoding.                    |
| `id`          | string    | No       | Echoed on pushes.                     |

#### Example

```json
{
  "event": "sub",
  "topic": "beats",
  "symbols": ["BTC-USD"],
  "compression": 0,
  "id": "beats-1"
}
```

### Notification

**No top-level `pair`**.

| Field                      | Type    | Description                                                       |
| -------------------------- | ------- | ----------------------------------------------------------------- |
| `topic`                    | string  | Always `beats`.                                                   |
| `t`                        | integer | Send time (Unix ms).                                              |
| `data.symbol`              | string  | Symbol (uppercase).                                               |
| `data.latencySec`          | integer | Open latency in seconds; open before `startAt - latencySec*1000`. |
| `data.matrix`              | array   | Price × time cell matrix.                                         |
| `data.matrix[].priceLower` | string  | Lower price bound.                                                |
| `data.matrix[].priceUpper` | string  | Upper price bound.                                                |
| `data.matrix[].startAt`    | integer | Window start (Unix ms).                                           |
| `data.matrix[].endAt`      | integer | Window end (Unix ms).                                             |
| `data.matrix[].odds`       | string  | Cell odds.                                                        |



### Unsubscribe beats

| Field     | Type      | Required | Description           |
| --------- | --------- | -------- | --------------------- |
| `event`   | string    | Yes      | `unsub`.              |
| `topic`   | string    | Yes      | `beats`.              |
| `symbols` | string\[] | Yes      | Symbols to tear down. |

#### Example

```json
{
  "event": "unsub",
  "topic": "beats",
  "symbols": ["BTC-USD"]
}
```
