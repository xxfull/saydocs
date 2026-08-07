---
description: >-
  This page answers common questions about YesFi trading insurance (Revival /
  Double-up), not the same as bank-style “buy insurance for wealth management.”
hidden: true
metaLinks:
  alternates:
    - >-
      https://app.gitbook.com/s/2ydpQ0rXK8hfDMCn6VFp/readme/chang-jian-wen-ti/bao-xian-xiang-guan-wen-ti
---

# Insurance issues

### YesWhat is YesFi trading insurance?

YesFi offers two **optional** protections for positions:

| Name                        | What it does (high level)                                                                                                                                                                                                                                                                                     |
| --------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Revival insurance**       | If the insured position is **liquidated**, you receive a payout equal to the **full opening margin** for that position—the margin is “revived” via the payout rather than treated as gone by default.                                                                                                         |
| **Double-profit insurance** | When **floating profit** reaches the **agreed threshold**, you receive **additional profit equal to the current floating profit**—often described as **100% → 200%** profit. Premium moves with the market in **real time**; you can **cancel anytime** (refund based on **remaining time**, at a fair rate). |

**Premium, trigger rules, and expected payout** always follow the **quote and confirmation screens** for that purchase.

***

### What coverage durations are available?

There are **three fixed durations**:

* **24 hours**, **72 hours**, **168 hours (7 days)**

There is **no** arbitrary or custom length. Renewals and switches are **only** among these **three** options.

***

### When can I add insurance?

* Insurance is bound to **real perpetual orders/positions**.
* **At open**, only **market orders** support adding it (whether you can add/renew/switch/cancel later follows **in-app prompts**).

***

### Is this the same as “insurance wealth products”?

**No.** YesFi insurance only supports **in-platform contract trading and position risk management**. It is not the same as savings or wealth products sold by insurers to retail users. If someone means generic finance or offline insurance, clarify the context first, then point back to YesFi trading insurance.

***

### How is the premium priced?

The platform combines **real-time volatility**, **one of the three terms above**, **leverage**, and position context to produce a **live premium**; it changes with the market and your position. **Do not** treat assistant or third-party numbers as fixed rates—use the **live quote** in the app.

***

### Can I cancel, renew, or switch?

* **Cancel**: You can **stop** coverage anytime; refunds follow **remaining coverage time** at a fair rule—the **exact amount** is whatever the platform shows.
* **Renew / switch**: You can operate among **24h / 72h / 168h**; when switching, the old policy is refunded for **remaining time**, then the new tier is priced.
* **Close position**: When the position is closed, **unexpired** policies are refunded for **remaining time**.

***

### Quote failures, payout issues, or UI not matching expectations?

* **DEX model**: YesFi has **no** human support line, official phone, tickets, or one-to-one desk. Use **in-app copy**, this doc, and **public community channels**.
* **Scams**: Anyone claiming to be “YesFi official support” and asking for **transfers, private keys, seed phrases, or paid unfreezing** is fraudulent—**do not** comply.
* For **API error codes** (e.g. insurance domain `INS_*`), developers can refer to the Error responses doc; end users can retry shortly and check wallet and network status.

***
