# 取得帳戶餘額（GET /exchange/account/balances）

```
GET /v1/private/exchange/account/balances
```

無需查詢參數。

#### 回應

```json
{
  "success": true,
  "data": {
    "address": "...",
    "asset": "...",
    "by_kind": {}
  }
}
```

#### 回應欄位

| 欄位             | 類型      | 說明                   |
| -------------- | ------- | -------------------- |
| `data`         | object  | 查詢結果。                |
| `data.address` | string  | 目前驗權呼叫方地址。           |
| `data.asset`   | string  | 本次餘額視圖使用的報價資產。       |
| `data.by_kind` | object  | 內部帳本帳戶類型到餘額十進位字串的映射。 |
| `success`      | boolean | 請求是否成功。              |
