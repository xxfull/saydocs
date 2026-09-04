---
metaLinks:
  alternates:
    - >-
      https://app.gitbook.com/s/KiKbOTrmqLWnXHD7ZyeJ/ai-jiao-yi-yuan/zi-zhang-hu-yu-qian-bao
---

# Sub-account wallets

### What a sub-account is

* **One user : many sub-accounts**\
  Each sub-account has its own margin pool and **isolated** positions. Losses or liquidation in one sub-account do **not** automatically affect others.

Current product limits:

* Each user can create up to **10** sub-accounts.

***

### Relationship to your wallet

* **You still control the funds**
* **Login and signing**\
  Whether you use **MetaMask**, **WalletConnect**, **Rabby**, or a social-login flow supported by the product, real trades and fund actions still rely on on-chain authorization and signatures. Natural language is the interface layer. It does not bypass your signing authority.
* **Convenience and delegated signing scenarios**\
  For smoother interaction, the product can apply practices such as encrypted key storage, permission isolation, and minimal exposure. Final implementation details follow official security disclosures and the live interface.

***

### Common use cases

| Scenario                                    | Suggested setup                                             |
| ------------------------------------------- | ----------------------------------------------------------- |
| Testing a new strategy                      | Create and start with small size in a separate sub-account. |
| Separating long-term and short-term trading | Use two Traders with separate funds and positions.          |
| Separating Commodities and Cryptos          | Use two Traders with separate funds and positions.          |

***

### Security reminders

* YesFi does **not** use a traditional private customer-service flow that asks for your private key, mnemonic, transfers, or paid account recovery.
* If you have questions about positions or funds, verify them through the app and on-chain records.
