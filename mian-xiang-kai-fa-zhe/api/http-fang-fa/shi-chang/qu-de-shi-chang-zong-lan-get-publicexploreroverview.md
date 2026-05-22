# 取得市場總覽（GET /public/exchange/overview）

```
GET /v1/public/exchange/overview
```

無需查詢參數。

#### 回應

```json
{
  "success": true,
  "data": {
    "fundingRate": "...",
    "openInterest": "...",
    "price": "...",
    "symbol": "..."
  }
}
```

#### 回應欄位

| 欄位                  | 類型         | 說明                                               |
| ------------------- | ---------- | ------------------------------------------------ |
| `data`              | object \[] | 市場總覽列表。                                          |
| `data.fundingRate`  | string     | 目前資金費率，十進位字串。不可用時為 `null`。                       |
| `data.openInterest` | string     | 未平倉量，十進位字串，按該市場的 `szDecimals` 截斷。不可用時為 `null`。   |
| `data.price`        | string     | 最新市場價格，十進位字串，按該市場的 `pxDecimals` 截斷。不可用時為 `null`。 |
| `data.symbol`       | string     | 完整市場符號。                                          |
| `success`           | boolean    | 請求是否成功。                                          |
