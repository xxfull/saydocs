---
metaLinks:
  alternates:
    - >-
      https://app.gitbook.com/s/KiKbOTrmqLWnXHD7ZyeJ/feng-xian-yu-zheng-ce/yong-hu-cao-zuo-an-quan/qian-ming-qing-qiu-he-yan-qing-dan-fang-diao-yu
---

# Signature Request Verification Checklist (Anti-Phishing)

Most sensitive wallet actions on YesFi rely on **EIP-712 or on-chain signatures**. Attackers often imitate sites or wallet popups to trick users into signing token approvals, malicious contract calls, or altered API requests. Check each item before you sign.

***

### Checklist before signing

1. **Domain and certificate**\
   Confirm that the browser address bar shows the official domain. Watch for look-alike characters. Do not enter trading pages through short links from chat messages.
2. **Contract or target shown in the wallet popup**\
   Be careful with `approve` or `permit` requests that show unusually large allowances, unlimited approval, or unknown contract addresses. If anything looks unclear, reject it and verify it through official channels.
3. **EIP-712 typed data for private API requests**\
   If you integrate or debug private Gateway endpoints, use the signature type required by the environment and docs, such as **`ApiRequest`** with `X-Signature-Type: eip712-api-request`. Check:
   * Whether **`method`** and **`path`** match the real HTTP request.
   * Whether **`path`** excludes the query string.
   * Whether **`bodyHash`** matches the canonical hash of the JSON body you will send.
   * Whether **`timestamp`** and **`deadline`** are reasonable and consistent with the headers.
   * Whether **`chainId`** and **`verifyingContract`** match the current environment values.\
     See [EIP-712 request signing](../../for-developers/api/http-methods/signing.md) for the full field list.
4. **Human-readable details**\
   If the popup only shows raw hex and you cannot understand the action, reject it first. Then retry with the official client or an updated wallet.
5. **Social engineering pressure**\
   There is no official YesFi flow that says "sign now or your account will be frozen" or "pay a deposit to unlock funds." Close the message immediately.
6. **Replay risk and time window**\
   The server can treat the same signature and timestamp pair as one-time use. Do not share screenshots or raw signatures with anyone while the request is still valid.

***

### Notes for integrators

* **`path` must match `URL.Path` exactly.** Do not include the `?` query string.
* **The body bytes and canonical JSON hash must match the signed payload.** Otherwise verification can fail, or the request body can be replaced.

***

### Related pages

* [EIP-712 request signing](../../for-developers/api/http-methods/signing.md)
* [Authentication](../../for-developers/api/http-methods/authentication.md)
* [Private Key and Mnemonic Phrase Management Tips](private-key-and-mnemonic-phrase-management-tips.md)
