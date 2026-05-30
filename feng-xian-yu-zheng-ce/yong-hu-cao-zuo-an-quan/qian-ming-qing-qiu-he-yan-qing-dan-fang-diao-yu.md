# 簽名請求核驗清單（防釣魚）

在 YesFi 上使用錢包時，大部分敏感操作依賴 **EIP-712 / 鏈上簽名**。攻擊者常偽造站點或彈窗，誘導你簽署**轉帳授權、惡意合約呼叫或遭竄改的 API 請求**。簽字前請逐項核對。

***

### 簽字前檢查清單

1. **網域與憑證**\
   確認瀏覽器網址列為**官方網域**（注意同形異義字元）；避免透過聊天中的短連結直接進入交易頁。
2. **錢包彈窗中的「合約 / 互動對象」**\
   對**授權額度異常大、無限授權、不明合約地址**的 `approve` 或 `permit` 保持警覺；若不確定，請拒絕並到官方社群或文件核實。
3. **EIP-712 結構化資料（Private API）**\
   若你整合或除錯 **Gateway 私域介面**，簽名類型應與環境及文件約定一致（如 **`ApiRequest`** + `X-Signature-Type: eip712-api-request`）。請核對：
   * **`method`、`path`（不含 query）** 是否與實際 HTTP 請求一致；
   * **`bodyHash`** 是否與待送出的 JSON body 規範雜湊一致；
   * **`timestamp` / `deadline`** 是否合理，且是否與請求標頭一致；
   * **`chainId`、`verifyingContract`** 是否為**目前環境**公布的值。\
     完整欄位說明見：[EIP-712 請求簽名](../../mian-xiang-kai-fa-zhe/api/http-fang-fa/qian-ming.md)。
4. **人類可讀資訊**\
   若彈窗只顯示十六進位資料、無法解析含義，**優先拒絕**，改用官方客戶端或更新錢包後再試。
5. **社交工程**\
   不存在「必須立刻簽名否則封號」「繳納保證金解鎖」等 YesFi **官方**流程；遇到此類話術請直接關閉。
6. **重放與時間窗**\
   同一組簽名 / 時間戳在服務端可能被**一次性消耗**；不要將截圖或簽名原文發給他人，以免被濫用（在允許的時間窗內）。

***

### 整合方提示

* **`path` 必須與 `URL.Path` 一致**（不含 `?` 查詢字串）。
* **Body 位元組與 canonical JSON 雜湊**須與簽名計算一致，否則會驗簽失敗，或存在 body 被替換的風險。

***

### 相關頁面

* [EIP-712 請求簽名](../../mian-xiang-kai-fa-zhe/api/http-fang-fa/qian-ming.md)
* [認證](../../mian-xiang-kai-fa-zhe/api/http-fang-fa/yan-zheng.md)
* [私鑰與助記詞管理提示](si-yue-yu-zhu-ji-ci-guan-li-ti-shi.md)
