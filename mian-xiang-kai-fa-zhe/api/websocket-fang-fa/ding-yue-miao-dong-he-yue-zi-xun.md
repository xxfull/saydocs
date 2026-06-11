# 訂閱秒動合約資訊

## 訂閱 beats\_symbols

`topic=beats_symbols` **不使用** `symbols` 或 `addresses`。訂閱整個 topic，約每秒推送（內容 hash 未變時可能跳過）。

單連線上整個 topic 計 **1** 個訂閱槽位。

### 訂閱請求

| 欄位            | 類型      | 必填 | 說明               |
| ------------- | ------- | -- | ---------------- |
| `event`       | string  | 是  | `sub`。           |
| `topic`       | string  | 是  | `beats_symbols`。 |
| `compression` | integer | 否  | 出站推送編碼。          |
| `id`          | string  | 否  | 下行回顯。            |

#### 示例

```json
{
  "event": "sub",
  "topic": "beats_symbols",
  "compression": 0,
  "id": "beats-symbols-1"
}
```

### 下行推送

| 欄位                 | 類型      | 說明                                 |
| ------------------ | ------- | ---------------------------------- |
| `data.ts_ms`       | integer | 組裝時刻（Unix ms）。                     |
| `data.crypto`      | array   | crypto 類 symbol 列表。                |
| `data.traditional` | array   | 傳統類 symbol 列表。                     |
| `data.unknown`     | array   | 目錄有但 PG 無 instrument 類型時。          |
| `*[].symbol`       | string  | 交易對。                               |
| `*[].price`        | string  | 來自 `oracle:ticker24h` 字段 `c`；無則省略。 |
| `*[].pct_24h`      | string  | 來自 `P` 或 `pct`；無則省略。               |

### 退訂 beats\_symbols

| 欄位      | 類型     | 必填 | 說明               |
| ------- | ------ | -- | ---------------- |
| `event` | string | 是  | `unsub`。         |
| `topic` | string | 是  | `beats_symbols`。 |

#### 示例

```json
{
  "event": "unsub",
  "topic": "beats_symbols"
}
```
