---
description: A fast introduction for first-time users, traders, and developers.
---

# QuickStart

> **One Yes, Trade All** — See [What is YesFi](readme/what-is-yesfi.md)?.

| What you will encounter in YesFi | In one line                                                                                                                                                              |
| -------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| What the product is              | An **AI-native on-chain perpetuals exchange**. You express intent in **chat**. Your **AI Trader** helps turn it into orders and position actions.                        |
| Who makes the decision           | **You.** The agent provides analysis and options. Final execution still requires **your confirmation and on-chain signature**. It does **not** trade without permission. |
| Where funds sit                  | USDC assets are securely stored on-chain in contracts. You can create multiple independent **Traders / sub-accounts**. Funds stay separated. The limit is **10**.        |

***

### Recommended path

#### 1. Start with the product overview

Spend a few minutes on [What is YesFi](readme/what-is-yesfi.md).

Use it to confirm the product model fits your expectations.

If you care about **Zero Loss Insurance** or **Double Profit Insurance**, rely on official product terms only.

#### 2. Prepare your wallet and sign in

* **Device**: [Web app](https://trade.yesfi.com/) and mobile browsers are supported where available.
* **Sign in**:
  * Connect an **EVM wallet** such as MetaMask, WalletConnect, or Rabby.
* **Deposit** _(optional)_:
  * Supported chains: `Ethereum`, `Base`, `BSC`, `Arbitrum`
  * Supported token: `USDC`
* **Transfer**_(optional)_: A user can have multiple sub-accounts, with funds segregated between sub-accounts and transfers allowed between them.See [**Sub-account wallets**](trading/market-and-limit/sub-account-wallets.md) for details.

#### 3. Start with natural-language prompts

In AI chat, you can talk about markets, ask rules, and place **market**, **limit**, **take-profit**, or **stop-loss** instructions.

You can copy or adapt the examples in [**Prompt reference**](ai-trader/prompt-reference.md).

* **Important**: Always confirm actions in the interface before execution.
* Never send your **private key** or **mnemonic phrase** to anyone.

#### 4. Start with strategy or trading signals

* **Flash options**: Select a strategy card, confirm your direction and amount, and place the order — the outcome settles automatically at a pre-locked multiplier when the window closes. No stop-loss setup or liquidation risk; your maximum loss is limited to the principal you put in.
* **Trading signals**:Browse signals rated by the YesFi AI system, pick one that fits your risk tolerance, and apply the full parameter set — direction, leverage, TP, and stop-loss — with a single click or adjust manually before placing the order.&#x20;

#### 5. Open the deeper docs when you need them

These topics go beyond a quick intro, but every real trader should review them:

* [**Trading**](trading/) — order types, position handling, pricing, and funding
* [**Insurance**](insurance/) — Zero Loss Insurance and Double Profit Insurance
* [**FAQ**](rewards-and-campaigns/faq.md)

***

### Security and expectation setting

* **YesFi does not operate through unofficial private support requests**. Treat any request for transfers, private keys, mnemonic phrases, or paid account recovery as fraud.
* Use **official documentation**, in-app guidance, and public community channels as your primary sources.
* If you see claims such as **zero threshold**, **zero fees**, **guaranteed principal**, or **guaranteed profit**, verify the exact rules in the product and official docs.

***

### Section map

| Page                                              | Best for                                       |
| ------------------------------------------------- | ---------------------------------------------- |
| [What is YesFi?](readme/what-is-yesfi.md)         | Understanding the product model and its limits |
| [Agent profile](ai-trader/agent-profile.md)       | Setting names, avatars, and attribute tags     |
| [Prompt reference](ai-trader/prompt-reference.md) | Finding example prompts for chat-based trading |
| [API](for-developers/api/)                        | Integrating with the platform as a developer   |
