# 查詢帳戶資訊（POST /exchange/account）

```
POST /v1/public/exchange/account
```

#### 請求體

| 欄位        | 類型     | 必填 | 說明                                 |
| --------- | ------ | -- | ---------------------------------- |
| `address` | string | 是  | 小寫 EVM 地址，格式為 `0x` 前綴加 40 位十六進位字元。 |

#### 回應

```json
{
  "success": true,
  "data": {
    "account": {},
    "address": "...",
    "margin_claimed": true
  }
}
```

#### 回應欄位

| 欄位                                               | 類型         | 說明                          |
| ------------------------------------------------ | ---------- | --------------------------- |
| `data`                                           | object     | 查詢結果。                       |
| `data.account`                                   | object     | Explorer 返回的簡化帳戶摘要。         |
| `data.account.account_id`                        | string     | 帳戶所有者地址。                    |
| `data.account.currency`                          | string     | 帳戶摘要使用的估值或結算資產。             |
| `data.account.equity`                            | string     | 帳戶權益，十進位字串。                 |
| `data.account.insurance_summaries`               | object \[] | 按保險類型聚合的保費與賠付摘要。無資料時返回零值陣列。 |
| `data.account.insurance_summaries.insuranceType` | string     | 保險類型代碼。                     |
| `data.account.insurance_summaries.totalPayout`   | string     | 該類型累計產生的賠付金額，十進位字串。         |
| `data.account.insurance_summaries.totalPremium`  | string     | 該類型累計保費，十進位字串。              |
| `data.account.updated_at`                        | integer    | 毫秒級更新時間。目前實作固定返回 `0`。       |
| `data.account.used_margin`                       | string     | 已使用保證金，十進位字串。               |
| `data.address`                                   | string     | 目前查詢的帳戶地址。                  |
| `data.margin_claimed`                            | boolean    | 保證金是否已認領。目前實作固定返回 `false`。  |
| `success`                                        | boolean    | 請求是否成功。                     |
