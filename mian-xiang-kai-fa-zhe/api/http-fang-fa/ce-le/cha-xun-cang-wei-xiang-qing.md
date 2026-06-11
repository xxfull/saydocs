# 查詢倉位詳情

查詢單條**秒動合約 /** **連擊 /** **波動率 / 配對 / 區間 / 階梯 / 趨勢**倉位詳情。

```
GET /v1/public/beats/positions/detail?positionId=<uuid>
```

```
GET /v1/public/combo/positions/detail?positionId=<uuid>
```

```
GET /v1/public/moves/positions/detail?positionId=<uuid>
```

```
GET /v1/public/pair/positions/detail?positionId=<uuid>
```

```
GET /v1/public/range/positions/detail?positionId=<uuid>
```

```
GET /v1/public/steps/positions/detail?positionId=<uuid>
```

```
GET /v1/public/trend/positions/detail?positionId=<uuid>
```

#### Query Parameters

| 參數           | 類型     | 必填 | 說明       |
| ------------ | ------ | -- | -------- |
| `positionId` | string | 是  | 倉位 UUID。 |

#### Response Fields — `data.position`

| 欄位                        | 類型      | 說明          |
| ------------------------- | ------- | ----------- |
| `id`                      | string  | 倉位 UUID。    |
| `symbol`                  | string  | 交易對。        |
| `begin_time` / `end_time` | integer | 預測窗口。       |
| `price_min` / `price_max` | string  | 價帶。         |
| `margin`                  | string  | 保證金。        |
| `odds`                    | string  | 賠率。         |
| `status`                  | string  | 倉位狀態。       |
| `tx_hash`                 | string  | 開倉帳本 tx 哈希。 |
| `client_order_id`         | string  | 批次冪等鍵。      |
| `created_at`              | integer | 建立時間。       |

**連擊**產品特有欄位：

* `symbol1`
* `symbol2`
* `symbol3`
* `direction1`
* `direction2`
* `direction3`
* `targetPrice1`
* `targetPrice2`
* `targetPrice3`

**配對**產品特有欄位

* `asset1`
* `asset2`
* `direction`
* `handicap`
* `handicapTier`
* `openedPrice1`
* `openedPrice2`
* `targetDiffPct`

**區間**產品特有欄位

* `ring`
* `ringPct`
* `targetRingPct`
* `durationSec`
* `lowerPrice`
* `upperPrice`

**階梯**產品特有欄位

* `betTier`
* `tier1Pct`
* `tier2Pct`
* `tier3Pct`
* `tier4Pct`
* `tier1Price`
* `tier2Price`
* `tier3Price`
* `tier4Price`

**趨勢**產品特有欄位

* `direction`
* `tier`
* `amplitudePct`
* `targetAmplitudePct`
* `durationSec`
* `targetPrice`

**波動率**產品特有欄位

* `selectedTier`
* `tierLowerPct`
* `tierUpperPct`
* `durationSec`



#### Errors

| HTTP | Code                | 說明                  |
| ---- | ------------------- | ------------------- |
| 400  | `BEATS_BAD_REQUEST` | 缺少或非法 `positionId`。 |
| 404  | `BEATS_NOT_FOUND`   | 倉位不存在。              |
| 500  | `BEATS_INTERNAL`    | 服務端錯誤。              |
