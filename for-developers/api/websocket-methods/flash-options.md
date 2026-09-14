# flash-option

### Subscribe request

| Field         | Type    | Required | Description                                                                                      |
| ------------- | ------- | -------- | ------------------------------------------------------------------------------------------------ |
| `event`       | string  | Yes      | `sub`.                                                                                           |
| `topic`       | string  | Yes      | `flash-option`.                                                                                  |
| `compression` | integer | No       | Outbound encoding: `0` plain JSON; `1` gzip then Latin-1 text frame. Invalid → `WS_BAD_REQUEST`. |
| `id`          | string  | No       | Echoed on pushes when set.                                                                       |

Do not send `symbols` or `addresses` for this topic.

#### Example

```json
{
  "event": "sub",
  "topic": "flash-option",
  "compression": 0,
  "id": "flash-option-1"
}
```

### Notification: flash-option push

**No top-level `pair`** — identify content via `data`.

| Field         | Type    | Required | Description                                                               |
| ------------- | ------- | -------- | ------------------------------------------------------------------------- |
| `topic`       | string  | Yes      | Always `flash-option`.                                                    |
| `t`           | integer | Yes      | Server send time, Unix ms.                                                |
| `id`          | string  | No       | Subscription id echo.                                                     |
| `compression` | integer | No       | `0` or `1`.                                                               |
| `data`        | object  | Yes      | Equals the business MQ envelope **`payload`** (no server-side reshaping). |

When `compression` is `1`, decompress per **PROTOCOL.md** before JSON parse.

#### Current `data` event: `flash_option.product_active.v1`

| Field                | Type    | Description                                         |
| -------------------- | ------- | --------------------------------------------------- |
| `event_type`         | string  | Always `flash_option.product_active.v1`.            |
| `id`                 | string  | Product ID.                                         |
| `symbol`             | string  | e.g. `BTC-USDT`.                                    |
| `touch_mode`         | string  | `long`, `short`, or `breakout`.                     |
| `upper_barrier`      | string  | Optional; `long` / `breakout`.                      |
| `lower_barrier`      | string  | Optional; `short` / `breakout`.                     |
| `start_price`        | string  | Reference start price.                              |
| `started_at`         | integer | Start time (Unix ms).                               |
| `settled_at`         | integer | Scheduled settlement (Unix ms).                     |
| `duration_sec`       | integer | Duration in seconds.                                |
| `odds`               | string  | Payout multiplier.                                  |
| `max_shares`         | integer | Max sellable shares.                                |
| `sold_shares`        | integer | Sold shares at push time (often `0` on activation). |
| `price_per_share`    | string  | Premium per share.                                  |
| `available_distance` | string  | Purchasable distance threshold.                     |
| `status`             | string  | Usually `active`.                                   |
| `published_at`       | integer | Optional strategy publish time (Unix ms).           |
| `sent_at`            | integer | lite-option MQ send time (Unix ms).                 |

Pushes do **not** include `mark_price`; use `price` or HTTP product list for live marks.

#### Push example

```json
{
  "id": "flash-option-1",
  "topic": "flash-option",
  "compression": 0,
  "t": 1712908800456,
  "data": {
    "event_type": "flash_option.product_active.v1",
    "id": "100000001",
    "symbol": "BTC-USDT",
    "touch_mode": "long",
    "upper_barrier": "68000",
    "start_price": "67000",
    "started_at": 1779870000000,
    "settled_at": 1779870300000,
    "duration_sec": 300,
    "odds": "1.8",
    "max_shares": 1000,
    "sold_shares": 0,
    "price_per_share": "1",
    "available_distance": "50",
    "status": "active",
    "sent_at": 1779870000123
  }
}
```

### Subscription counting

On one connection, the entire **`flash-option` topic counts as 1 subscription slot** (not per symbol).

### vs `ledger` topic

| Topic          | Purpose                                                                                               |
| -------------- | ----------------------------------------------------------------------------------------------------- |
| `flash-option` | Product activation and other business broadcasts (MQ `topic=flash-option`).                           |
| `ledger`       | Ledger events including flash option `OPTION_OPEN` / `OPTION_PAYOUT`; read `data.entries[].biz_type`. |

### Unsubscribe

#### Request

| Field         | Type    | Required | Description     |
| ------------- | ------- | -------- | --------------- |
| `event`       | string  | Yes      | `unsub`.        |
| `topic`       | string  | Yes      | `flash-option`. |
| `compression` | integer | No       | Optional.       |
| `id`          | string  | No       | Optional.       |

Do not send `symbols` or `addresses`.

#### Example

```json
{
  "event": "unsub",
  "topic": "flash-option"
}
```

#### Response

No dedicated JSON ack in production; after a successful unsub, no further `flash-option` pushes are delivered.
