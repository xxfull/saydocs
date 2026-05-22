# 取得資金費率（GET /public/exchange/funding-rate）

```
GET /v1/public/exchange/funding-rate
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
    "fundingRate": "...",
    "symbol": "..."
  }
}
```

#### 回應欄位

| 欄位                 | 類型      | 說明             |
| ------------------ | ------- | -------------- |
| `data`             | object  | 查詢結果。          |
| `data.fundingRate` | string  | 資金費率，以十進位字串表示。 |
| `data.symbol`      | string  | 完整市場符號。        |
| `success`          | boolean | 請求是否成功。        |
