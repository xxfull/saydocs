# 取得最新價格（GET /public/exchange/prices）

```
GET /v1/public/exchange/prices
```

無需查詢參數。

#### 回應

```json
{
  "success": true,
  "data": {}
}
```

#### 回應欄位

| 欄位        | 類型      | 說明                                                |
| --------- | ------- | ------------------------------------------------- |
| `data`    | object  | 從完整交易對到最新價格十進位字串的映射。價格按市場 `pxDecimals` 截斷，不做四捨五入。 |
| `success` | boolean | 請求是否成功。                                           |
