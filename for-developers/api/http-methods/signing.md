---
description: >-
  This page explains how to build EIP-712 signatures for authenticated private
  API requests, including the domain, headers, signature type, and path-matching
  rules.
metaLinks:
  alternates:
    - >-
      https://app.gitbook.com/s/KiKbOTrmqLWnXHD7ZyeJ/mian-xiang-kai-fa-zhe/api/http-fang-fa/qian-ming
---

# Signing

### EIP712Domain

In practice, the signature `EIP712Domain` includes at least these fields:

| Field               | Description                                                                                                                                 |
| ------------------- | ------------------------------------------------------------------------------------------------------------------------------------------- |
| `name`              | Product domain string. It must match the on-chain and frontend implementation, such as `YesFiExchange`.                                     |
| `version`           | Domain version, such as `1`                                                                                                                 |
| `chainId`           | Must be in the gateway's **allowed chain ID list** for the current environment. If not sent explicitly, the gateway uses its default chain. |
| `verifyingContract` | Set by deployment config. It can be a zero address placeholder or a real contract address.                                                  |

> Use the `chainId` and `verifyingContract` published for **your target environment**, such as testnet or mainnet. Do not hard-code values from another environment.

If the request includes **`X-EIP712-Chain-Id`** as a decimal string, the gateway uses it to select a chain from the allowed list. Invalid or disallowed values fail verification.

***

### HTTP headers for private requests

When you send the exact same `method`, `path`, and body that were signed, include these headers on standard public requests. The signed `path` contains **only the path**, not the query string.

| Header              | Description                                                                                  |
| ------------------- | -------------------------------------------------------------------------------------------- |
| `X-Signature`       | Hex-encoded 65-byte ECDSA signature with `0x` prefix                                         |
| `X-Signature-Type`  | Fixed value **`eip712-api-request`**                                                         |
| `X-Address`         | Claimed signer address, as `0x` plus 20 bytes                                                |
| `X-Timestamp`       | Unix timestamp in **milliseconds**. It must match the `timestamp` inside the signed message. |
| `X-EIP712-Chain-Id` | Optional chain ID as a decimal string                                                        |

> Verification uses **`URL.Path`**. If the URL contains `?query=...`, the signature still includes **only the path**. Do not include `?` or the query string.

When `Content-Type: application/json` is used, make sure the body you send matches the body used to compute **`bodyHash`**.

***

### Time window, deadline, and replay protection

* **Time window**: The difference between `X-Timestamp` and server time must stay within the configured window, typically **5 minutes**.
* **`deadline`**: If the JSON body includes `deadline`, in milliseconds as a number or decimal string, the gateway uses it as the cutoff. If it is missing, the implementation usually applies a default offset from `timestamp`.
* **Replay protection**: After signature verification and address matching succeed, the gateway consumes the **`(address, timestamp)`** pair. The same pair cannot be reused. See [**Authentication**](authentication.md) and [**Error responses**](error-responses.md).

***

### Request signature type

This integration uses only **`X-Signature-Type: eip712-api-request`**. It maps to the EIP-712 primary type **`ApiRequest`**. The typed message includes `from`, HTTP `method`, `path` without query, `bodyHash`, `timestamp`, and `deadline`.

* **`bodyHash`** uses the parsed JSON body in a canonical form with recursively sorted keys, then applies **Keccak-256**.
* If there is **no body**, the result matches the canonical encoding of an empty object, `{}`.
* Your implementation must match the reference behavior. Otherwise, signature verification fails.

Reference implementation:

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
		"path":      path, // no query; must match URL.Path
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

### Browser and CORS

For direct browser calls, make sure the preflight request allows headers such as `X-Signature`, `X-Signature-Type`, `X-Address`, `X-Timestamp`, and `X-EIP712-Chain-Id`. Exact behavior depends on the environment's CORS policy.

***

### Related pages

* [**Authentication**](authentication.md)
* [**Error responses**](error-responses.md)
