# 訂閱策略產品

### 訂閱請求

| 欄位            | 類型        | 必填 | 說明                                                             |
| ------------- | --------- | -- | -------------------------------------------------------------- |
| `event`       | string    | 是  | `sub`。                                                         |
| `topic`       | string    | 是  | `lite_odds`。                                                   |
| `product`     | string    | 是  | 產品類型：`trend` / `range` / `pair` / `combo` / `moves` / `steps`。 |
| `symbols`     | string\[] | 是  | 非空；至少一個合法 symbol（大寫規範化）。                                       |
| `compression` | integer   | 否  | 出站推送：`0` 明文 JSON；`1` gzip 後 Latin-1 文本幀。                       |
| `id`          | string    | 否  | 若提供，下行推送會回顯。                                                   |

#### 示例

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

### 下行推送：lite\_odds

**沒有頂層 `pair`** — 透過 `data.product` 與 `data.symbol` 辨識。

| 欄位            | 類型      | 必填 | 說明                |
| ------------- | ------- | -- | ----------------- |
| `topic`       | string  | 是  | 固定 `lite_odds`。   |
| `t`           | integer | 是  | 本服務發送該幀的 Unix 毫秒。 |
| `id`          | string  | 否  | 訂閱時的 `id` 回顯。     |
| `compression` | integer | 否  | `0` 或 `1`。        |
| `data`        | object  | 是  | 賠率快照，見下表。         |

#### `data` 公共欄位

| 欄位              | 類型      | 說明                          |
| --------------- | ------- | --------------------------- |
| `product`       | string  | 產品類型（與訂閱 `product` 一致）。     |
| `symbol`        | string  | 交易對（大寫）。                    |
| `compute_ts`    | integer | 定價計算時刻（Unix ms）。            |
| `volatility`    | string  | 年化波動率 σ（decimal string）。    |
| `current_price` | string  | 當前價格（秒級 ZSET 最新收盤價）。        |
| `durations`     | array   | 各持倉週期賠率；元素欄位隨 `product` 而異。 |

#### `durations[]` 按產品類型

| 產品        | 主要欄位                                                                                                               |
| --------- | ------------------------------------------------------------------------------------------------------------------ |
| **trend** | `duration_sec`、`odds`、`target_price`、`amplitude_pct`、`target_amplitude_pct`、`tiers[]`（`light`/`medium`/`heavy` 三檔） |
| **range** | `duration_sec`、`odds`、`lower_price`、`upper_price`、`win_bands[]`、`ring_pct`、`target_ring_pct`                       |
| **pair**  | `duration_sec`、`odds`、`target_diff_pct`、`handicap`                                                                 |
| **moves** | `duration_sec`、`odds`、`tier_lower_pct`、`tier_upper_pct`                                                            |
| **steps** | `duration_sec`、`odds`、`tier_prices[]`（長度 4）、`tier_odds[]`、`tier1-4_pct`、`target_tier1-4_pct`                       |
| **combo** | WS 暫不推送 combo 賠率                                                                                                   |

**Trend 說明**：`durations[]` 條數等於 symbol 配置 `duration_opts` 長度；每條含 `tiers[]` 一次性給出 light/medium/heavy 三檔賠率。頂層 `odds`/`target_price`/`amplitude_pct` 取 **medium** 檔作向後兼容。

#### Trend 推送示例

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

### 訂閱計數

每 **`(product, symbol)`** 計 **1** 個訂閱槽位。

### 相關 HTTP

開倉前可先查 GET symbols 等接口確認 `duration_opts` 與檔位配置；下單走對應 POST open 私有路由。

### 退訂

退訂時須提供與訂閱時相同的 **`product`** 與 **`symbols`**。

#### 請求

| 欄位            | 類型        | 必填 | 說明              |
| ------------- | --------- | -- | --------------- |
| `event`       | string    | 是  | `unsub`。        |
| `topic`       | string    | 是  | `lite_odds`。    |
| `product`     | string    | 是  | 與訂閱一致。          |
| `symbols`     | string\[] | 是  | 要退訂的 symbol 列表。 |
| `compression` | integer   | 否  | 可選。             |
| `id`          | string    | 否  | 可選。             |

#### 示例

```json
{
  "event": "unsub",
  "topic": "lite_odds",
  "product": "trend",
  "symbols": ["BTC-USD"]
}
```

#### 回應

**沒有**單獨的 JSON 確認幀；退訂成功後不再收到對應 `(product, symbol)` 的推送。

