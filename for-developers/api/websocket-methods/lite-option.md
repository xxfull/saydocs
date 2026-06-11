# Lite option

### Subscribe request

| Field         | Type      | Required | Description                                                             |
| ------------- | --------- | -------- | ----------------------------------------------------------------------- |
| `event`       | string    | Yes      | `sub`.                                                                  |
| `topic`       | string    | Yes      | `lite_odds`.                                                            |
| `product`     | string    | Yes      | Product type: `trend` / `range` / `pair` / `combo` / `moves` / `steps`. |
| `symbols`     | string\[] | Yes      | Non-empty; at least one valid symbol after normalization.               |
| `compression` | integer   | No       | Outbound: `0` plain JSON; `1` gzip then Latin-1 text frame.             |
| `id`          | string    | No       | Echoed on pushes when set.                                              |

#### Example

```json
{
  "event": "sub",
  "topic": "lite_odds",
  "product": "trend",
  "symbols": ["BTC-USD"],
  "compression": 0,
  "id": "lite-odds-1"
}
```

### Notification: lite\_odds push

**No top-level `pair`** — identify via `data.product` and `data.symbol`.

| Field         | Type    | Required | Description                |
| ------------- | ------- | -------- | -------------------------- |
| `topic`       | string  | Yes      | Always `lite_odds`.        |
| `t`           | integer | Yes      | Server send time, Unix ms. |
| `id`          | string  | No       | Subscription id echo.      |
| `compression` | integer | No       | `0` or `1`.                |
| `data`        | object  | Yes      | Odds snapshot; see below.  |

#### Common `data` fields

| Field           | Type    | Description                                           |
| --------------- | ------- | ----------------------------------------------------- |
| `product`       | string  | Product type (matches subscription `product`).        |
| `symbol`        | string  | Symbol (uppercase).                                   |
| `compute_ts`    | integer | Pricing compute time (Unix ms).                       |
| `volatility`    | string  | Annualized volatility σ (decimal string).             |
| `current_price` | string  | Latest close from second-level price ZSET.            |
| `durations`     | array   | Per-duration odds; element shape varies by `product`. |

#### `durations[]` by product

| Product   | Key fields                                                                                                            |
| --------- | --------------------------------------------------------------------------------------------------------------------- |
| **trend** | `duration_sec`, `odds`, `target_price`, `amplitude_pct`, `target_amplitude_pct`, `tiers[]` (`light`/`medium`/`heavy`) |
| **range** | `duration_sec`, `odds`, `lower_price`, `upper_price`, `win_bands[]`, `ring_pct`, `target_ring_pct`                    |
| **pair**  | `duration_sec`, `odds`, `target_diff_pct`, `handicap`                                                                 |
| **moves** | `duration_sec`, `odds`, `tier_lower_pct`, `tier_upper_pct`                                                            |
| **steps** | `duration_sec`, `odds`, `tier_prices[]` (len 4), `tier_odds[]`, `tier1-4_pct`, `target_tier1-4_pct`                   |
| **combo** | Combo odds not pushed over WS yet                                                                                     |

**Trend note:** `durations[]` length equals symbol `duration_opts`. Each element includes `tiers[]` with all three amplitude tiers. Top-level `odds`/`target_price`/`amplitude_pct` mirror the **medium** tier for backward compatibility.

#### Trend push example

```json
{
  "id": "lite-odds-1",
  "topic": "lite_odds",
  "compression": 0,
  "t": 1712908800456,
  "data": {
    "product": "trend",
    "symbol": "BTC-USD",
    "compute_ts": 1712908800123,
    "volatility": "0.45",
    "current_price": "63500.12",
    "durations": [
      {
        "duration_sec": 60,
        "odds": "6.40",
        "target_price": "63576.24",
        "amplitude_pct": "0.0012",
        "target_amplitude_pct": "0.0012",
        "tiers": [
          { "tier": "light", "odds": "8.20", "target_price": "63532.70", "amplitude_pct": "0.0005", "target_amplitude_pct": "0.0005" },
          { "tier": "medium", "odds": "6.40", "target_price": "63576.24", "amplitude_pct": "0.0012", "target_amplitude_pct": "0.0012" },
          { "tier": "heavy", "odds": "4.90", "target_price": "63627.12", "amplitude_pct": "0.0020", "target_amplitude_pct": "0.0020" }
        ]
      }
    ]
  }
}
```

#### Subscription counting

Each **`(product, symbol)`** counts as **1** slot.



### Unsubscribe lite\_odds

#### Request

| Field         | Type      | Required | Description           |
| ------------- | --------- | -------- | --------------------- |
| `event`       | string    | Yes      | `unsub`.              |
| `topic`       | string    | Yes      | `lite_odds`.          |
| `product`     | string    | Yes      | Same as subscribe.    |
| `symbols`     | string\[] | Yes      | Symbols to tear down. |
| `compression` | integer   | No       | Optional.             |
| `id`          | string    | No       | Optional.             |

#### Example

```json
{
  "event": "unsub",
  "topic": "lite_odds",
  "product": "trend",
  "symbols": ["BTC-USD"]
}
```
