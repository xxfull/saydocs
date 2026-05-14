---
description: Full-table 24h rank streams pct_rank_24h and volume_rank_24h.
metaLinks:
  alternates:
    - >-
      https://app.gitbook.com/s/KiKbOTrmqLWnXHD7ZyeJ/mian-xiang-kai-fa-zhe/api/websocket-fang-fa/24-xiao-shi-pai-xing-ding-yue
---

# rank (24h)

## Subscribe rank (24h)

Send a **WebSocket text frame** with JSON.

Topics:

| `topic`               | Description                                          |
| --------------------- | ---------------------------------------------------- |
| `pct_rank_24h`        | 24h percent-change ranking table.                    |
| `volume_rank_24h`     | 24h quote-volume ranking table.                      |
| `pct_rank_24h_asc`    | 24h percent-change ranking table in ascending order. |
| `volume_rank_24h_asc` | 24h quote-volume ranking table in ascending order.   |

### Subscribe request

<table><thead><tr><th width="131.5390625">Field</th><th width="112.69140625">Type</th><th width="125.02734375">Required</th><th>Description</th></tr></thead><tbody><tr><td><code>event</code></td><td>string</td><td>Yes</td><td><code>sub</code>.</td></tr><tr><td><code>topic</code></td><td>string</td><td>Yes</td><td><code>pct_rank_24h</code> \<code>volume_rank_24h_asc</code>\<code>pct_rank_24h_asc</code> <code>volume_rank_24h</code></td></tr><tr><td><code>symbols</code></td><td>string[]</td><td>No</td><td>Omit, <code>[]</code>, or <code>["*"]</code> only.</td></tr><tr><td><code>compression</code></td><td>integer</td><td>No</td><td><p>Optional. Outbound push compression: <code>0</code> Normal UTF-8 JSON text; <code>1</code> First gzip, then Latin-1 mapped to a <strong>text frame</strong> (still a text frame).</p><p>Illegal values ​​(not 0/1) return <code>WS_BAD_REQUEST</code>.</p></td></tr><tr><td><code>id</code></td><td>string</td><td>No</td><td>Optional. Client-side custom request associated ID. Server-side <strong>returns the original content</strong> in the corresponding topic's push notifications (if provided), facilitating front-end matching of subscriptions and push notifications.</td></tr><tr><td><code>limit</code></td><td>integer</td><td>Yes</td><td>Use only for ranking topics.The number of rows returned by the request; <code>0</code> or omitted indicates using the server's default <code>rank_top_n</code>.</td></tr><tr><td><code>crypto_scope</code></td><td>string</td><td>No</td><td><code>all</code> 、<code>only</code> or <code>exclude</code>。'only' means including only cryptocurrencies, 'exclude' means excluding cryptocurrencies. The default is 'all', which means including everything.</td></tr></tbody></table>

#### Example

```json
{
  "event": "sub",
  "topic": "pct_rank_24h",
  "symbols": ["*"]
}
```

### Notification: rank push

Same envelope as Subscribe rank (daily): `topic`, `pair` (often `TOPN`), `t`, `id`, `compression`, `data` with `as_of_ms`, `top_n`, `rows`.

#### Row `kline` subset (24h)

For **24h** rank rows, nested `kline` fields come from **`oracle:ticker24h`** subset — **not** from the 1d K-line bar (unlike daily rank).

## Unsubscribe rank (24h)

Send a **WebSocket text frame** with JSON.

### Request

| Field     | Type      | Required | Description                          |
| --------- | --------- | -------- | ------------------------------------ |
| `event`   | string    | Yes      | `unsub`.                             |
| `topic`   | string    | Yes      | `pct_rank_24h` or `volume_rank_24h`. |
| `symbols` | string\[] | No       | Omit, `[]`, or `["*"]`.              |
| `id`      | string    | No       | Optional.                            |

#### Example

```json
{
  "event": "unsub",
  "topic": "pct_rank_24h",
  "symbols": ["*"]
}
```

### Response

No dedicated JSON ack.
