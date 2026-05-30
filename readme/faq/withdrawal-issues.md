---
description: >-
  This page covers withdrawing from YesFi to your wallet, fees, and common
  failures. Withdrawals are on-chain; outcome depends on chain confirmation and
  correct recipient details.
metaLinks:
  alternates:
    - >-
      https://app.gitbook.com/s/2ydpQ0rXK8hfDMCn6VFp/readme/chang-jian-wen-ti/ti-xian-wen-ti
---

# Withdrawal issues

### Does YesFi charge a withdrawal fee?

**Yes.** Per product documentation, **each withdrawal** includes a **0.1 USDC** platform fee (you also pay on-chain **gas** and similar network fees).

Use the in-app **withdrawal preview** for what you receive after fees and network costs.

***

### Are there withdrawal limits or cooling-off periods?

Docs: **no** withdrawal **quota** cap and **no** forced account cool-down. After **on-chain confirmation**, funds should arrive in your wallet; **time varies with congestion**, often on the order of minutes to tens of minutes.

***

### Withdrawal stuck on Pending or very slow

1. **Chain status**: On a block explorer, is the withdrawal **Pending / Success / Failed**?
2. **Gas / congestion**: Congestion delays inclusion; if you speed up or replace from the wallet, follow that wallet’s rules.
3. **Address**: A wrong address sends funds to an **unintended** account; transfers are **irreversible**.

***

### Wrong address or wrong network

YesFi **cannot** undo a broadcast on-chain transfer. Wrong chain or address means you must work with the counterparty or compliant chain-side help—**never** expect an “official agent” to reverse it. Before confirming, verify **network, token, and address**.

***

### “Available to withdraw” vs total balance

Common reasons:

* **Positions**: Open positions and working orders **lock margin**; not all balance is withdrawable.
* **Unrealized PnL**: UI may separate **wallet-available** vs **margin in use**; reduce or close positions to free collateral.
* **In flight**: Recent trades, funding settlement, or internal transfers may still be processing.

***

### Someone offers to “manually speed up” my withdrawal?

YesFi is a **DEX protocol** with **no** human support desk; withdrawals run via **contracts and signed requests**. If they demand **extra fees, private keys, or seed phrases** to “release” funds, it is a **scam**.

***
