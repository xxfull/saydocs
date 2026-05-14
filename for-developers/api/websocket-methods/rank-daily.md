---
description: Full-table daily rank streams pct_rank and volume_rank.
metaLinks:
  alternates:
    - >-
      https://app.gitbook.com/s/KiKbOTrmqLWnXHD7ZyeJ/mian-xiang-kai-fa-zhe/api/websocket-fang-fa/mei-ri-pai-xing-ding-yue
---

# rank (daily)

## Subscribe rank (daily)

Send a **WebSocket text frame** with JSON.

Topics:

| `topic`           | Description                                                                |
| ----------------- | -------------------------------------------------------------------------- |
| `pct_rank`        | Daily percent-change ranking table.                                        |
| `volume_rank`     | Daily volume / quote turnover ranking table.                               |
| `pct_rank_asc`    | Daily percent-change ranking table in ascending order.                     |
| `volume_rank_asc` | Daily trading volume/quote turnover rate ranking table in ascending order. |

### Subscribe request

<table><thead><tr><th width="140.82421875">Field</th><th width="111.81640625">Type</th><th width="123.93359375">Required</th><th>Description</th></tr></thead><tbody><tr><td><code>event</code></td><td>string</td><td>Yes</td><td><code>sub</code>.</td></tr><tr><td><code>topic</code></td><td>string</td><td>Yes</td><td><code>pct_rank</code>、<code>pct_rank_asc</code>、<code>volume_rank</code>、<code>volume_rank_asc</code></td></tr><tr><td><code>symbols</code></td><td>string[]</td><td>No</td><td>For rank topics: <strong>omit</strong>, <code>[]</code>, or <code>["*"]</code> only — not a per-symbol list.</td></tr><tr><td><code>compression</code></td><td>integer</td><td>No</td><td><p>Optional. Outbound push compression: <code>0</code> Normal UTF-8 JSON text; <code>1</code> First gzip, then Latin-1 mapped to a <strong>text frame</strong> (still a text frame).</p><p>Illegal values ​​(not 0/1) return <code>WS_BAD_REQUEST</code>.</p></td></tr><tr><td><code>id</code></td><td>string</td><td>No</td><td>Optional. Client-side custom request associated ID. Server-side <strong>returns the original content</strong> in the corresponding topic's push notifications (if provided), facilitating front-end matching of subscriptions and push notifications.</td></tr><tr><td><code>limit</code></td><td>integer</td><td>Yes</td><td>Use only for ranking topics.The number of rows returned by the request; <code>0</code> or omitted indicates using the server's default <code>rank_top_n</code>.</td></tr><tr><td><code>crypto_scope</code></td><td>string</td><td>No</td><td><code>all</code> 、<code>only</code> or <code>exclude</code>。'only' means including only cryptocurrencies, 'exclude' means excluding cryptocurrencies. The default is 'all', which means including everything.</td></tr></tbody></table>

#### Example

```json
{
  "event": "sub",
  "topic": "volume_rank",
  "symbols": ["*"],
  "id": "rank-day-1"
}
```

### Notification: rank push

Top-level:

| Field         | Type    | Required | Description                                        |
| ------------- | ------- | -------- | -------------------------------------------------- |
| `topic`       | string  | Yes      | `pct_rank` or `volume_rank`.                       |
| `pair`        | string  | Yes      | Full-table subscription often uses literal `TOPN`. |
| `t`           | integer | Yes      | Server send time, Unix ms.                         |
| `id`          | string  | No       | Echo.                                              |
| `compression` | integer | No       | Encoding.                                          |
| `data`        | object  | Yes      | Table payload.                                     |

#### `data` object

| Field      | Type    | Description                                    |
| ---------- | ------- | ---------------------------------------------- |
| `as_of_ms` | integer | Cutoff time for the table, Unix ms.            |
| `top_n`    | integer | Row count in frame (config e.g. `rank_top_n`). |
| `rows`     | array   | Sorted by `rank` ascending.                    |

#### `rows[]` element

| Field    | Type    | Description                                                                                                  |
| -------- | ------- | ------------------------------------------------------------------------------------------------------------ |
| `rank`   | integer | 1-based rank.                                                                                                |
| `symbol` | string  | Instrument.                                                                                                  |
| `score`  | string  | ZSET score string (semantics differ for pct vs volume).                                                      |
| `kline`  | object  | Display subset from **`oracle:kline:rt:{SYMBOL}:1d`** latest bar: fields such as `bv`, `q`, `c`, `pct`, `s`. |

## Unsubscribe rank (daily)

Send a **WebSocket text frame** with JSON.

### Request

| Field     | Type      | Required | Description                                                   |
| --------- | --------- | -------- | ------------------------------------------------------------- |
| `event`   | string    | Yes      | `unsub`.                                                      |
| `topic`   | string    | Yes      | `pct_rank` or `volume_rank` (must match active subscription). |
| `symbols` | string\[] | No       | Omit, `[]`, or `["*"]` — same rule as subscribe.              |
| `id`      | string    | No       | Optional.                                                     |

#### Example

```json
{
  "event": "unsub",
  "topic": "volume_rank",
  "symbols": ["*"]
}
```

### Response

No dedicated JSON ack.
