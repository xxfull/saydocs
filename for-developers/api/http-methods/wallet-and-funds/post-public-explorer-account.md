---
metaLinks:
  alternates:
    - >-
      https://app.gitbook.com/s/KiKbOTrmqLWnXHD7ZyeJ/mian-xiang-kai-fa-zhe/api/http-fang-fa/qian-bao-yu-zi-jin/cha-xun-zhang-hu-zi-xun-post-publicexploreraccount
---

# POST account

```
POST /v1/public/exchange/account
```

#### Request Body

| Field     | Type   | Required | Description                                                                                    |
| --------- | ------ | -------- | ---------------------------------------------------------------------------------------------- |
| `address` | string | Yes      | Lowercase EVM address in the form of a `0x` prefix followed by a 40-bit hexadecimal character. |

#### Response

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

#### Response Fields

| Field                                            | Type       | Description                                                                                                        |
| ------------------------------------------------ | ---------- | ------------------------------------------------------------------------------------------------------------------ |
| `data`                                           | object     |                                                                                                                    |
| `data.account`                                   | object     | the simplified account summary structure returned by explorer.                                                     |
| `data.account.account_id`                        | string     | The address of the account owner.                                                                                  |
| `data.account.currency`                          | string     | The valuation/settlement assets used for the account summary.                                                      |
| `data.account.equity`                            | string     | Account benefits, expressed using a decimal string.                                                                |
| `data.account.insurance_summaries`               | object \[] | Summary of premiums and claims aggregated by insurance type; returns a zero value array when no data is available. |
| `data.account.insurance_summaries.insuranceType` | string     | Insurance type code.                                                                                               |
| `data.account.insurance_summaries.totalPayout`   | string     | The type has generated the cumulative amount of the indemnity obligation, expressed using a decimal string.        |
| `data.account.insurance_summaries.totalPremium`  | string     | This type of policy accumulates premiums, expressed as a decimal string.                                           |
| `data.account.updated_at`                        | integer    | Update timestamp in milliseconds. Current implementation fixed return `0`.                                         |
| `data.account.used_margin`                       | string     | Margin used, represented by decimal string.                                                                        |
| `data.address`                                   | string     | The account address being queried.                                                                                 |
| `data.margin_claimed`                            | boolean    | Whether the margin has been claimed or not. The current implementation fixedly returns`false`.                     |
| `success`                                        | boolean    |                                                                                                                    |
