---
hidden: true
icon: head-side-gear
metaLinks:
  alternates:
    - >-
      https://app.gitbook.com/s/KiKbOTrmqLWnXHD7ZyeJ/ai-jiao-yi-yuan/zhi-hui-dai-li-she-ding-dang
---

# Agent profile

In SayFi, each **AI Trader** is more than a single chat session. It is a reusable trading profile with a name, an avatar, attribute tags, and its own conversation boundary. Think of it as your dedicated trading assistant. You define the markets, style, risk preference, and stop-loss discipline first. Then you issue instructions in natural language.

***

### In the app: recruit your AI Trader

The creation flow usually appears as a step-by-step setup for your next dedicated AI Trader.

It typically includes:

1. **Name and avatar**\
   Give the Trader a recognizable identity.
2. **Attribute tags**\
   Select or customize the tags that shape this Trader's focus and style.
3. **Start**\
   Save the profile and enter the linked chat and sub-account.

The exact wording and UI steps depend on the current app version.

#### Name and avatar

| Item               | Description                                                                                                              |
| ------------------ | ------------------------------------------------------------------------------------------------------------------------ |
| **AI Trader name** | A custom name that helps you switch between Traders. The interface can enforce a character limit.                        |
| **Avatar**         | A visual identity such as a pixel-style character. It affects recognition only. It does not change on-chain permissions. |

***

### Attribute tags

Attribute tags shape the assistant's emphasis during analysis, reminders, and option suggestions. Exact labels, multi-select behavior, and `+ Custom` support depend on the live UI. Actual orders and adjustments still require your instruction or confirmation.

#### Preferred instruments

The assistant gives more attention to the markets you select.

Common categories include:

* **Cryptocurrency**
* **Commodities**
* **Energy**
* **Stocks**
* **Forex**

Multi-select means those categories stay inside this Trader's discussion scope. It does not mean automatic multi-market trading.

#### Trading frequency

| Option   | Practical meaning                                                                     |
| -------- | ------------------------------------------------------------------------------------- |
| **Low**  | Lower-frequency discussion. More patience. More focus on larger structures or events. |
| **Mid**  | A balanced rhythm between signal density and trade frequency.                         |
| **High** | More focus on short-term timing and denser opportunity discussion.                    |

This setting shapes **analysis rhythm**, not unattended auto-trading. Execution still depends on your confirmation and signature.

#### Entry style

Common examples:

* **Trend Follow**
* **Range**
* **Breakout**
* **Pullback Buy**

Some versions of the UI support **`+ Custom`** for entry style. Use it to add short keywords or phrases that match your own setup logic.

#### Risk preference

| Option           | Practical meaning                                                                                                                                |
| ---------------- | ------------------------------------------------------------------------------------------------------------------------------------------------ |
| **Conservative** | More focus on capital preservation and tighter risk exposure.                                                                                    |
| **Balanced**     | A middle ground between risk and return.                                                                                                         |
| **Aggressive**   | More willingness to discuss higher-volatility setups and leverage ideas. Actual leverage limits still follow market controls and platform rules. |

If `+ Custom` is available, use it to describe your risk preference more precisely.

#### Stop-loss discipline

| Option       | Practical meaning                                                            |
| ------------ | ---------------------------------------------------------------------------- |
| **Strict**   | More emphasis on hard stop-losses and disciplined exits.                     |
| **Flexible** | More room for trailing stops, staged profit taking, or drawdown-based exits. |

If `+ Custom` is available, you can define how strict "strict" should be in your own words. Final execution still follows the TP and SL values you set in the interface.

***

### Why this matters

* **More consistent behavior**\
  The assistant keeps your selected instruments, pace, entry logic, risk preference, and stop-loss discipline in view.
* **Clearer multi-strategy separation**\
  You can maintain multiple Traders, each with its own sub-account and conversation context.
* **You still stay in control**\
  Tags guide suggestions. They do not grant the assistant permission to trade on its own.

***

### Relationship to sub-accounts

Each **AI Trader** maps to **one** on-chain sub-account. Funds, isolated positions, and margin pools stay separate. Switching Traders is effectively switching to a different set of funds, risk boundaries, and chat context.

For details, see [**Sub-account wallets**](../contracts/market-and-limit/sub-account-wallets.md).

***

### Tips

* Start with **one** Trader first. Add more only when you need strategy separation.
* Keep tag selection focused. Fewer strong signals often work better than selecting everything.
* If you make a large change to risk or stop-loss tags, test with small size first.
