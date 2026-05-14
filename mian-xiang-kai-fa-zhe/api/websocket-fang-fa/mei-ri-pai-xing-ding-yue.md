# 每日排行訂閱

傳送一個 **WebSocket 文字幀**，訊息體為 JSON。

可訂閱的主題如下：

| `topic`           | 說明            |
| ----------------- | ------------- |
| `pct_rank`        | 每日漲跌幅排行。      |
| `volume_rank`     | 每日報價成交額排行。    |
| `pct_rank_asc`    | 每日漲跌幅排行升序排名表。 |
| `volume_rank_asc` | 每日報價成交額升序排名表。 |

### 訂閱請求

| 欄位             | 型別        | 必填 | 說明                                                                      |
| -------------- | --------- | -- | ----------------------------------------------------------------------- |
| `event`        | string    | 是  | 固定為 `sub`。                                                              |
| `topic`        | string    | 是  | `pct_rank` 、`pct_rank_asc、volume_rank_asc`或 `volume_rank`。              |
| `symbols`      | string\[] | 否  | 排行主題只能省略、傳空陣列 `[]`，或傳 `["*"]`，不支援按單一交易對訂閱。                              |
| `compression`  | integer   | 否  | 下行壓縮標記。可選 `0` 或 `1`。                                                    |
| `id`           | string    | 否  | 客戶端請求 ID。若設定，會在推送中回顯。                                                   |
| `limit`        | integer   | 否  | **僅排行類 topic 使用**。請求的回傳行數；省略表示使用伺服器預設 `rank_top_n`。                     |
| `crypto_scope` | string    | 否  | `all` 、`only`或 `exclude`。only是指只包含加密貨幣，exclude 是指排除加密貨幣，預設是 all 代表包含全部。 |

#### 範例

```json
{
  "event": "sub",
  "topic": "volume_rank",
  "symbols": ["*"],
  "id": "rank-day-1"
}
```

### 推送訊息：排行更新

#### 頂層欄位

| 欄位            | 型別      | 必填 | 說明                          |
| ------------- | ------- | -- | --------------------------- |
| `topic`       | string  | 是  | `pct_rank` 或 `volume_rank`。 |
| `pair`        | string  | 是  | 全表訂閱時通常固定為 `TOPN`。          |
| `t`           | integer | 是  | 伺服器傳送時間，Unix 毫秒。            |
| `id`          | string  | 否  | 請求 ID 回顯。                   |
| `compression` | integer | 否  | 編碼標記。                       |
| `data`        | object  | 是  | 排行表資料。                      |

#### `data` 物件

| 欄位         | 型別      | 說明                 |
| ---------- | ------- | ------------------ |
| `as_of_ms` | integer | 排行截面時間，Unix 毫秒。    |
| `top_n`    | integer | 當前幀包含的行數。          |
| `rows`     | array   | 按 `rank` 升序排列的行列表。 |

#### `rows[]` 元素

| 欄位       | 型別      | 說明                                                                                      |
| -------- | ------- | --------------------------------------------------------------------------------------- |
| `rank`   | integer | 從 1 開始的排名。                                                                              |
| `symbol` | string  | 交易對。                                                                                    |
| `score`  | string  | 排行分數字串。不同主題下含義不同。                                                                       |
| `kline`  | object  | 用於展示的行情摘要，來自 **`oracle:kline:rt:{SYMBOL}:1d`** 最新一根 K 線的欄位子集，例如 `bv`、`q`、`c`、`pct`、`s`。 |

## 取消訂閱每日排行

傳送一個 **WebSocket 文字幀**，訊息體為 JSON。

### 請求

| 欄位        | 型別        | 必填 | 說明                                    |
| --------- | --------- | -- | ------------------------------------- |
| `event`   | string    | 是  | 固定為 `unsub`。                          |
| `topic`   | string    | 是  | `pct_rank` 或 `volume_rank`，必須與目前訂閱一致。 |
| `symbols` | string\[] | 否  | 只能省略、傳空陣列 `[]`，或傳 `["*"]`。            |
| `id`      | string    | 否  | 可選請求 ID。                              |

#### 範例

```json
{
  "event": "unsub",
  "topic": "volume_rank",
  "symbols": ["*"]
}
```

### 回應

通常不會回傳專門的 JSON 確認幀。
