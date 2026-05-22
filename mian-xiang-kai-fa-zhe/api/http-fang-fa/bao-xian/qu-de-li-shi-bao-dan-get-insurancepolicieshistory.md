# 取得歷史保單（GET /insurance/policies/history）

列出目前使用者所有非 `active` 的歷史保單。

```
GET /v1/public/insurance/policies/history
```

#### 查詢參數

| 參數             | 必填 | 預設 | 說明                   |
| -------------- | -- | -- | -------------------- |
| `symbol`       | 否  | —  | 依交易對過濾               |
| `limit`        | 否  | 20 | 最大 200               |
| `offset`       | 否  | 0  | 分頁偏移                 |
| `expireAtFrom` | 否  | —  | `expire_at` 下界，毫秒，包含 |
| `expireAtTo`   | 否  | —  | `expire_at` 上界，毫秒，包含 |

***
