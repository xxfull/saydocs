---
description: >-
  This page explains how the YesFi API Gateway identifies users and enforces
  address-based access control without usernames or passwords.
metaLinks:
  alternates:
    - >-
      https://app.gitbook.com/s/KiKbOTrmqLWnXHD7ZyeJ/mian-xiang-kai-fa-zhe/api/http-fang-fa/yan-zheng
---

# Authentication

### Who should read this

* Frontend or backend developers calling **private** APIs from apps or scripts
* Integrators who need the full request-auth flow together with the signing page

If you have not signed EIP-712 requests with a wallet before, read [**Signing**](signing.md) first.

***

### Core concepts

#### No traditional account system

YesFi does **not** use usernames or passwords. The user identity is an **EVM-compatible address**. Sensitive actions are authorized with an **EIP-712 structured signature**. After verification, the gateway treats the request as coming from that address.

#### Private and public routes

| Path shape                                               | Requires EIP-712                                                           |
| -------------------------------------------------------- | -------------------------------------------------------------------------- |
| `/v1/private/...` and other versioned `private` prefixes | **Yes**. Send the signature headers described on the signing page.         |
| `/v1/public/...`                                         | **No**. These routes do not pass through the gateway's EIP-712 middleware. |

> Requests that do not match a deployed versioned public or private route can return `404`. Actual behavior depends on the current route set and deployment.

Verification only succeeds when the address **recovered from the signature** matches the address declared in `X-Address`.

***

### Gateway auth order

For a **private** request that requires signature verification, the gateway can run these checks in order. Exact behavior depends on deployment settings.

1. **Blacklist** — block by address, or by address and client IP
2. **Rate limit** — limit throughput per address
3. **EIP-712 verification and replay protection** — validate time window, `deadline`, signature recovery, and one-time use of `(address, timestamp)`

***

### Error responses

Auth and signature failures use HTTP status codes such as **4xx** and **429**. The response body follows the same JSON envelope, including `success: false`. For security, responses do **not** expose detailed failure reasons that help an attacker. See [**Error responses**](error-responses.md) for the full code list.

Common auth-related `code` values include:

| `code`              | Summary                                                                                                               | Typical HTTP status |
| ------------------- | --------------------------------------------------------------------------------------------------------------------- | ------------------- |
| `INVALID_SIGNATURE` | Missing or invalid headers, unsupported chain ID, signature type and path mismatch, or signature verification failure | `401` or `400`      |
| `EXPIRED_REQUEST`   | Request falls outside the allowed time window, or `deadline` has passed                                               | `401`               |
| `TIMESTAMP_REUSED`  | The same address reuses a consumed timestamp                                                                          | `401`               |
| `AUTH_RATE_LIMITED` | Per-address rate limit is hit                                                                                         | `429`               |
| `AUTH_BLACKLISTED`  | The request hits a blacklist rule                                                                                     | `403`               |

***

### Related pages

* [**Signing**](signing.md) — headers, domain, primary type, and path rules
* [**Error responses**](error-responses.md) — response schema and the full code list
* If your browser sends a CORS preflight, allow custom headers such as `X-Signature`, `X-Signature-Type`, `X-Address`, `X-Timestamp`, and `X-EIP712-Chain-Id`
