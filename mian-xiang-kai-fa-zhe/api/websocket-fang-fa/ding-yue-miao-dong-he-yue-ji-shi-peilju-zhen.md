# 訂閱秒動合約即時賠率矩陣

### 訂閱請求

| 欄位            | 類型        | 必填 | 說明                |
| ------------- | --------- | -- | ----------------- |
| `event`       | string    | 是  | `sub`。            |
| `topic`       | string    | 是  | `beats`。          |
| `symbols`     | string\[] | 是  | 非空；至少一個合法 symbol。 |
| `compression` | integer   | 否  | 出站推送編碼。           |
| `id`          | string    | 否  | 下行回顯。             |

#### 示例

```json
{
  "event": "sub",
  "topic": "beats",
  "symbols": ["BTC-USD"],
  "compression": 0,
  "id": "beats-1"
}
```

### 下行推送

**沒有頂層 `pair`**。

| 欄位                         | 類型      | 說明                                           |
| -------------------------- | ------- | -------------------------------------------- |
| `topic`                    | string  | 固定 `beats`。                                  |
| `t`                        | integer | 發送時刻（Unix ms）。                               |
| `data.symbol`              | string  | 交易對（大寫）。                                     |
| `data.latencySec`          | integer | 開倉延遲秒數；須在 `startAt - latencySec*1000` 前完成開倉。 |
| `data.matrix`              | array   | 價格×時間格子矩陣。                                   |
| `data.matrix[].priceLower` | string  | 價格下界。                                        |
| `data.matrix[].priceUpper` | string  | 價格上界。                                        |
| `data.matrix[].startAt`    | integer | 時間窗口起始（Unix ms）。                             |
| `data.matrix[].endAt`      | integer | 時間窗口結束（Unix ms）。                             |
| `data.matrix[].odds`       | string  | 該格賠率。                                        |

#### 推送示例

```json
{
  "id": "beats-1",
  "topic": "beats",
  "compression": 0,
  "t": 1712908800456,
  "data": {
    "symbol": "BTC-USD",
    "latencySec": 5,
    "matrix": [
      {
        "priceLower": "63000",
        "priceUpper": "63100",
        "startAt": 1717000000000,
        "endAt": 1717000030000,
        "odds": "1.85"
      }
    ]
  }
}
```

### 相關 HTTP

選格後下單：POST beats/batch-open（EIP-712）。

### 退訂 beats

| 欄位        | 類型        | 必填 | 說明              |
| --------- | --------- | -- | --------------- |
| `event`   | string    | 是  | `unsub`。        |
| `topic`   | string    | 是  | `beats`。        |
| `symbols` | string\[] | 是  | 要退訂的 symbol 列表。 |

#### 示例

```json
{
  "event": "unsub",
  "topic": "beats",
  "symbols": ["BTC-USD"]
}
```
