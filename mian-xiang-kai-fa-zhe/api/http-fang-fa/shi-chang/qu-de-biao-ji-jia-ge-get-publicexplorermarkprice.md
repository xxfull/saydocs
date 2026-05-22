# 取得標記價格（GET /public/exchange/mark-price）

```
GET /v1/public/exchange/mark-price
```

#### 查詢參數

| 參數       | 必填 | 說明    |
| -------- | -- | ----- |
| `market` | 是  | 市場標識。 |

#### 回應

```json
{
  "success": true,
  "data": {
    "price": "...",
    "symbol": "..."
  }
}
```

#### 回應欄位

| 欄位            | 類型      | 說明                                        |
| ------------- | ------- | ----------------------------------------- |
| `data`        | object  | 查詢結果。                                     |
| `data.price`  | string  | 標記價格，以十進位字串表示，按市場 `pxDecimals` 截斷，不做四捨五入。 |
| `data.symbol` | string  | 完整市場符號。                                   |
| `success`     | boolean | 請求是否成功。                                   |
