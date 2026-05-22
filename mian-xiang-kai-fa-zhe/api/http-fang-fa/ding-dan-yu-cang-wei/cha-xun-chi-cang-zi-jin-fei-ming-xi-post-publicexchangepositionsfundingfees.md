# 查詢持倉資金費明細（POST /public/exchange/positions/funding-fees）

按 `position_uids` 批量查詢持倉的資金費事件。

```
POST /v1/public/exchange/positions/funding-fees
```

### 請求體

| 欄位              | 類型         | 必填 | 說明            |
| --------------- | ---------- | -- | ------------- |
| `position_uids` | string \[] | 是  | 要查詢的倉位 ID 列表。 |

若需使用其他查詢欄位，請以核心契約為準。

### 回應

成功時，`data.items` 會按 `position_uid` 聚合資金費事件。

```json
{
  "success": true,
  "data": {
    "items": [
      {
        "position_uid": "uuid",
        "total": "0.12",
        "events": [
          {
            "amount": "0.06",
            "created_at": "2026-05-22T12:00:00Z"
          }
        ]
      }
    ]
  }
}
```

#### 回應欄位

| 欄位                             | 類型         | 說明                           |
| ------------------------------ | ---------- | ---------------------------- |
| `data`                         | object     | 查詢結果。                        |
| `data.items`                   | object \[] | 按 `position_uid` 聚合的資金費事件列表。 |
| `data.items.position_uid`      | string     | 倉位唯一識別碼。                     |
| `data.items.total`             | string     | 該倉位在目前回應範圍內的資金費合計。           |
| `data.items.events`            | object \[] | 該倉位對應的資金費事件列表。               |
| `data.items.events.amount`     | string     | 單筆資金費金額。使用十進位字串表示。           |
| `data.items.events.created_at` | string     | 單筆資金費事件建立時間，ISO 8601 UTC。    |
| `success`                      | boolean    | 請求是否成功。                      |

#### 狀態碼

| 狀態碼   | 說明                  |
| ----- | ------------------- |
| `200` | 查詢成功。               |
| `400` | 參數錯誤。回傳 core 錯誤封裝。  |
| `503` | 服務不可用。回傳 core 錯誤封裝。 |

### 相關頁面

* [取得資金費率（GET /public/exchange/funding-rate）](../shi-chang/qu-de-zi-jin-feilget-publicexplorerfundingrate.md)
