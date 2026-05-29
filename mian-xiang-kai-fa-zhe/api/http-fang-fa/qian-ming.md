---
description: >-
  本頁說明如何為需要驗權的私有 API 請求建立 EIP-712 簽名，包括域、請求標頭、請求簽名類型，以及該類型與 path
  的匹配要求。開始前請先讀完驗證頁中的路由與身分模型。
---

# 簽名

### 域（EIP712Domain）

簽名使用的 `EIP712Domain` 在實作上至少包含：

| 欄位                  | 說明                                                         |
| ------------------- | ---------------------------------------------------------- |
| `name`              | 產品域名字串，需與鏈上 / 前端實作保持一致，例如 `YesFiExchange`                  |
| `version`           | 域版本號，例如 `1`                                                |
| `chainId`           | 必須在 Gateway **目前環境允許的鏈 ID 清單** 內；若未在標頭明確宣告，則使用 Gateway 預設鏈 |
| `verifyingContract` | 由部署設定指定；可能是零地址佔位，也可能是實際合約地址                                |

> **給整合方**\
> 請以 **你所面向的環境**（測試網 / 主網）公布的 `chainId` 與 `verifyingContract` 為準；不要硬編碼其他環境的值。

如果請求攜帶 **`X-EIP712-Chain-Id`**（十進位字串），系統會用它從允許清單中選定鏈；若值非法或不在清單中，驗簽會失敗。

***

### HTTP 請求標頭（私有請求）

在送出 **與簽名內容完全一致** 的 `method`、**只含路徑且不含 query 的** `path`，以及參與 bodyHash 計算的 body 時，標準呼叫需要帶上以下標頭：

| 請求標頭                | 說明                                    |
| ------------------- | ------------------------------------- |
| `X-Signature`       | `0x` 开头的 65 字节 ECDSA 签名的十六进制          |
| `X-Signature-Type`  | 固定為 **`eip712-api-request`**          |
| `X-Address`         | 使用者宣告的簽名者地址（`0x` + 20 位元組）            |
| `X-Timestamp`       | **毫秒** Unix 時間戳；需與訊息中的 `timestamp` 一致 |
| `X-EIP712-Chain-Id` | 可選，鏈 ID 的十進位字串                        |

> **重要**\
> 驗簽使用的 `path` 是 **`URL.Path`**。如果 URL 帶有 `?query=...`，**簽名裡仍只包含 path 部分**，不包含 `?` 與查詢字串。

當 `Content-Type: application/json` 時，請確保實際送出的 body 位元組與計算 **bodyHash** 時完全一致。

***

### 時間窗、deadline 與防重放

* **時間窗**：`X-Timestamp` 與伺服器時間的差值不得超過 Gateway 設定的 **5 分鐘** 視窗。
* **deadline**：如果 JSON body 提供 `deadline`，單位為毫秒，可為數字或十進位字串，系統會以它作為截止時間；若未提供，實作通常會套用 **預設相對偏移**，例如自 `timestamp` 起若干分鐘。
* **防重放**：驗簽成功且地址匹配後，系統會**消耗**該 **(地址, timestamp)** 組合；**同一組不得重複使用**，否則會返回與重放相關的錯誤碼，詳見 [驗證](yan-zheng.md) 與 [錯誤回應](cuo-wu-hui-ying.md)。

***

### 請求簽名類型

本整合只使用 **`X-Signature-Type: eip712-api-request`**，對應的 EIP-712 主類型是 **`ApiRequest`**。Typed message 包含以下欄位：`from`（需與 `X-Address` 一致）、HTTP **`method`**、**`path`（不含 query）**、**`bodyHash`**、**`timestamp`** 與 **`deadline`**。

* **bodyHash**：先對解析後的 JSON body 物件做**遞迴鍵排序的 canonical 表示**，再取 **Keccak-256**；**沒有 body** 時，需與**空物件** `{}` 的規範編碼一致。實作必須與參考實作一致，否則驗簽會失敗。
* 參考實作：

```go
bh := eip712.CanonicalBodyHash(body) // body: map[string]interface{}，与网关中间件解析 JSON 一致
bodyHashHex := "0x" + hex.EncodeToString(bh[:])

td := apitypes.TypedData{
	Types: apitypes.Types{
		"EIP712Domain": eip712.TypeSchemas["EIP712Domain"],
		"ApiRequest":   eip712.TypeSchemas["ApiRequest"],
	},
	PrimaryType: "ApiRequest",
	Domain:      eip712.BuildDomainWithContract(chainID, verifyingContract),
	Message: apitypes.TypedDataMessage{
		"from":      addr.Hex(),
		"method":    method,
		"path":      path, // 无 query，与 URL.Path 一致
		"bodyHash":  bodyHashHex,
		"timestamp": strconv.FormatInt(tsMs, 10),
		"deadline":  strconv.FormatInt(deadlineMs, 10),
	},
}
rawHash, _, err := apitypes.TypedDataAndHash(td)
if err != nil {
	return "", err
}
sig, err := crypto.Sign(rawHash, priv)
if err != nil {
	return "", err
}
sig[64] += 27
return "0x" + hex.EncodeToString(sig), nil
```

***

### 瀏覽器與 CORS

從瀏覽器直接呼叫時，請確認預檢請求允許上述 `X-Signature*`、`X-Address`、`X-Timestamp`、`X-EIP712-Chain-Id` 等標頭；實際以該環境的 CORS 策略為準。

***

### 相關頁面

* [驗證](yan-zheng.md)
* [錯誤回應](cuo-wu-hui-ying.md)
