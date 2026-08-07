---
description: >-
  This page covers depositing USDC (and supported assets) into YesFi, transfers
  between sub-accounts, and balance not updating.
hidden: true
metaLinks:
  alternates:
    - >-
      https://app.gitbook.com/s/2ydpQ0rXK8hfDMCn6VFp/readme/chang-jian-wen-ti/chong-zhi-huo-zhuan-zhang-wen-ti
---

# Deposit or transfer issues

### How does custody work?

* **Non-custodial**: Assets live in on-chain contracts; moves require your signed authorization. YesFi does **not** freely move your principal via a centralized treasury model.
* **Verifiable**: Deposits and on-chain flows can be checked on a **block explorer**.

***

### Is there a deposit fee?

Per product docs: **no deposit fee**. You still pay on-chain **gas** (and similar network fees).

***

### Minimum amounts

* Docs: **no** mandatory minimum deposit.

***

### Deposit not showing or delayed

Check in order:

1. **On-chain success**: Explorer shows **Success** and the right recipient/contract for your environment.
2. **Network**: Use the **chain/network** YesFi expects; wrong chain often means **no** matching balance in the app.
3. **Token**: Perps are **USDC-margined**; use the **correct USDC** contract on that chain.
4. **Confirmations / time**: Congestion causes delays; after enough confirmations, **refresh** the app.

YesFi does **not** offer “manual balance fixes” or private support to change balances—resolution is **correct chain, correct asset, successful on-chain settlement**.

***

### Transfers between sub-accounts (multiple Traders)

YesFi supports multiple **AI Traders**, each with an **isolated sub-account**:

* **Isolated margin**: Pools are separate; Trader A’s loss does **not** auto-back Trader B.
* **Moving risk capital** between Traders usually needs an **in-app internal transfer** or closing and reallocating—follow the **live product flow**.

If a transfer looks stuck: confirm **you signed**, the **API/chain** succeeded, and you are on the **target Trader** view.

***

### Wrong chain or wrong token

If funds went to the **wrong network** or an unexpected token standard, **YesFi cannot reverse** the on-chain transaction.

***

### Login and trading authorization

* **EVM wallets** (e.g. MetaMask, WalletConnect, Rabby) and **Particle social login** (Google, X, GitHub, Apple).
* **Fills and transfers still need on-chain authorization.** If you can log in but not trade, check **wallet connection, network, and allowances**.

***

### Security

* **No** official phone or ticket-based human support—use **docs, in-app copy, and public communities**.
* Anyone asking for **private keys, seed phrases, or “verification” transfers** is not official.

***
