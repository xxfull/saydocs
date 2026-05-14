# 24 小時排行訂閱

傳送一個 **WebSocket 文字幀**，訊息體為 JSON。

可訂閱的主題如下：

| `topic`               | 說明                   |
| --------------------- | -------------------- |
| `pct_rank_24h`        | 24 小時漲跌幅排行，全表推送。     |
| `volume_rank_24h`     | 24 小時報價成交額排行，全表推送。   |
| `pct_rank_24h_asc`    | 24 小時漲跌幅排行，全表升序推送。   |
| `volume_rank_24h_asc` | 24 小時報價成交額排行，全表升序推送。 |

### 訂閱請求

<table><thead><tr><th width="119.8125">欄位</th><th width="106.19140625">型別</th><th width="122.640625">必填</th><th>說明</th></tr></thead><tbody><tr><td><code>event</code></td><td>string</td><td>是</td><td>固定為 <code>sub</code>。</td></tr><tr><td><code>topic</code></td><td>string</td><td>是</td><td><code>pct_rank_24h</code> 、<code>pct_rank_24h_asc、volume_rank_24h_asc</code>或 <code>volume_rank_24h</code>。</td></tr><tr><td><code>symbols</code></td><td>string[]</td><td>否</td><td>交易對列表。<code>price</code>/<code>kline</code>/<code>ticker_24h</code>/<code>ticker_multi</code>：必填且須包含有效 symbol（正規化後字元集為 A-Z、0-9、<code>.</code>、<code>-</code>、<code>_</code>）。排行類 topic：須省略、空陣列或僅 <code>["*"]</code>。</td></tr><tr><td><code>compression</code></td><td>integer</td><td>否</td><td>可選。出站推送是否壓縮：<code>0</code> 普通 UTF-8 JSON 文字；<code>1</code> 先 gzip 再 Latin-1 映射為<strong>文字幀</strong>（仍為 text frame）。非法值（非 0/1）回傳 <code>WS_BAD_REQUEST</code>。</td></tr><tr><td><code>id</code></td><td>string</td><td>否</td><td>客戶端請求 ID。若設定，會在推送中回顯。</td></tr><tr><td><code>limit</code></td><td>integer</td><td>否</td><td><strong>僅排行類 topic 使用</strong>。請求的回傳行數；<code>0</code>/省略表示使用伺服器預設 <code>rank_top_n</code>。</td></tr><tr><td><code>crypto_scope</code></td><td>string</td><td>否</td><td><code>all</code> 、<code>only</code>或 <code>exclude</code>。only是指只包含加密貨幣，exclude 是指排除加密貨幣，預設是 all 代表包含全部。</td></tr></tbody></table>

#### 範例

```json
{
  "event": "sub",
  "topic": "pct_rank_24h",
  "symbols": ["*"]
}
```

### 推送訊息：排行更新

訊息外層結構與[每日排行訂閱](mei-ri-pai-xing-ding-yue.md)一致，包含 `topic`、`pair`、`t`、`id`、`compression` 和 `data`。其中 `data` 包含 `as_of_ms`、`top_n` 和 `rows`。

#### 行內 `kline` 欄位說明

24 小時排行中，每一行的 `kline` 子物件來自 **`oracle:ticker24h`** 的欄位子集，**不是** 1 天 K 線條目。

## 取消訂閱 24 小時排行

傳送一個 **WebSocket 文字幀**，訊息體為 JSON。

### 請求

| 欄位        | 型別        | 必填 | 說明                                  |
| --------- | --------- | -- | ----------------------------------- |
| `event`   | string    | 是  | 固定為 `unsub`。                        |
| `topic`   | string    | 是  | `pct_rank_24h` 或 `volume_rank_24h`。 |
| `symbols` | string\[] | 否  | 只能省略、傳空陣列 `[]`，或傳 `["*"]`。          |
| `id`      | string    | 否  | 可選請求 ID。                            |

#### 範例

```json
{
  "event": "unsub",
  "topic": "pct_rank_24h",
  "symbols": ["*"]
}
```

### 回應

通常不會回傳專門的 JSON 確認幀。
