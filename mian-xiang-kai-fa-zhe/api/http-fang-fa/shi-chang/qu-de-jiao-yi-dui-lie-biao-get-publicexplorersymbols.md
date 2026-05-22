# 取得交易對列表（GET /public/exchange/symbols）

返回 Explorer 中可見的交易對列表。

支援按關鍵字做模糊過濾。

```
GET /v1/public/exchange/symbols
```

### 查詢參數

| 參數      | 必填 | 說明                                                                                  |
| ------- | -- | ----------------------------------------------------------------------------------- |
| `query` | 否  | 按基礎資產或完整交易對做模糊過濾。支援重複傳入多個 `query`，按 OR 關係匹配。最多 20 個非空值，每個最多 64 個字元。不傳或傳空時返回全部可見交易對。 |

### 回應

```json
{
  "success": true,
  "data": [
    {
      "name": "BTC-USD",
      "hlCoin": "BTC",
      "mark_price": "65000.5",
      "maxLeverage": 50,
      "openPositionMinMargin": "10",
      "pxDecimals": 1,
      "szDecimals": 4,
      "source": "hyperliquid",
      "tag": "major"
    }
  ]
}
```

#### 回應欄位（每個元素）

| 欄位                      | 類型      | 說明                                      |
| ----------------------- | ------- | --------------------------------------- |
| `name`                  | string  | 完整市場符號，例如 `BTC-USD`。                    |
| `hlCoin`                | string  | 上游基礎資產標識。                               |
| `mark_price`            | string  | 目前標記價格，十進位字串，按 `pxDecimals` 截斷。不可用時可缺失。 |
| `maxLeverage`           | integer | 該交易對允許的最大槓桿，且不小於 1。                     |
| `openPositionMinMargin` | string  | 開倉所需的最小保證金。                             |
| `pxDecimals`            | integer | 價格精度，即小數位數。                             |
| `szDecimals`            | integer | 數量精度，即小數位數。                             |
| `source`                | string  | 上游資料來源標記。                               |
| `tag`                   | string  | 資訊性分組標籤。                                |
