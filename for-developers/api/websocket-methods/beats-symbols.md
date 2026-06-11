# beats symbols

### Subscribe request

| Field         | Type    | Required | Description        |
| ------------- | ------- | -------- | ------------------ |
| `event`       | string  | Yes      | `sub`.             |
| `topic`       | string  | Yes      | `beats_symbols`.   |
| `compression` | integer | No       | Outbound encoding. |
| `id`          | string  | No       | Echoed on pushes.  |

#### Example

```json
{
  "event": "sub",
  "topic": "beats_symbols",
  "compression": 0,
  "id": "beats-symbols-1"
}
```

### Notification

| Field              | Type    | Description                                            |
| ------------------ | ------- | ------------------------------------------------------ |
| `data.ts_ms`       | integer | Assembly time (Unix ms).                               |
| `data.crypto`      | array   | Crypto symbols.                                        |
| `data.traditional` | array   | Traditional symbols.                                   |
| `data.unknown`     | array   | Listed in directory but no PG instrument type.         |
| `*[].symbol`       | string  | Symbol.                                                |
| `*[].price`        | string  | From `oracle:ticker24h` field `c`; omitted if missing. |
| `*[].pct_24h`      | string  | From `P` or `pct`; omitted if missing.                 |

### Unsubscribe beats\_symbols

| Field   | Type   | Required | Description      |
| ------- | ------ | -------- | ---------------- |
| `event` | string | Yes      | `unsub`.         |
| `topic` | string | Yes      | `beats_symbols`. |

#### Example

```json
{
  "event": "unsub",
  "topic": "beats_symbols"
}
```
