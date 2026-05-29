---
description: A fast introduction for first-time users, traders, and developers.
hidden: true
---

# Copy of QuickStart

> **One Yes, Trade All** — See [What is SayFi?](about-sayfi/what-is-sayfi.md).

| What you will encounter in YesFi | In one line                                                                                                                                                              |
| -------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| What the product is              | An **AI-native on-chain perpetuals exchange**. You express intent in **chat**. Your **AI Trader** helps turn it into orders and position actions.                        |
| Who makes the decision           | **You.** The agent provides analysis and options. Final execution still requires **your confirmation and on-chain signature**. It does **not** trade without permission. |
| Where funds sit                  | USDC assets are securely stored on-chain in contracts. You can create multiple independent **Traders / sub-accounts**. Funds stay separated. The limit is **10**.        |

***

### Recommended path

#### 1. Start with the product overview

Spend a few minutes on [**What is SayFi?**](about-sayfi/what-is-sayfi.md).

Use it to confirm the product model fits your expectations.

If you care about **Zero Loss Insurance** or **Double Profit Insurance**, rely on official product terms only.

#### 2. Prepare your wallet and sign in

* **Device**: [Web app](https://trade.sayfi.com/chat) and mobile browsers are supported where available.
* **Sign in**:
  * Connect an **EVM wallet** such as MetaMask, WalletConnect, or Rabby.
* **Deposit** _(optional)_:
  * Supported chains: `Ethereum`, `Base`, `BSC`, `Arbitrum`
  * Supported token: `USDC`

#### 3. Create your first AI Trader

In the app, complete the **recruit your AI Trader** flow.

Set the **name** and **avatar**.

Choose attribute tags such as **markets**, **trading frequency**, **entry style**, **risk preference**, and **stop-loss discipline**. Some fields support **+ Custom**.

See [**Agent profile**](ai-trader/agent-profile.md) for the full setup flow.

#### 4. Understand the account model

Each AI Trader typically maps to **one independent sub-account**.

Margin, positions, and risk stay isolated.

Switching Traders means switching to a different pool of funds and conversation context.

See [**Sub-account wallets**](ai-trader/sub-account-wallets.md) for details.

#### 5. Start with natural-language prompts

In chat, you can check markets, ask about rules, and place **market**, **limit**, **take-profit**, or **stop-loss** instructions.

You can copy or adapt the examples in [**Prompt reference**](ai-trader/prompt-reference.md).

* **Important**: Always confirm actions in the interface before execution.
* Never send your **private key** or **mnemonic phrase** to anyone.

#### 6. Open the deeper docs when you need them

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
| [What is SayFi?](about-sayfi/what-is-sayfi.md)    | Understanding the product model and its limits |
| [Agent profile](ai-trader/agent-profile.md)       | Setting names, avatars, and attribute tags     |
| [Prompt reference](ai-trader/prompt-reference.md) | Finding example prompts for chat-based trading |
| [API](for-developers/api/)                        | Integrating with the platform as a developer   |
