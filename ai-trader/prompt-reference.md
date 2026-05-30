---
hidden: true
icon: scroll
metaLinks:
  alternates:
    - >-
      https://app.gitbook.com/s/KiKbOTrmqLWnXHD7ZyeJ/ai-jiao-yi-yuan/dui-hua-zhi-ling-can-kao
---

# Prompt reference

SayFi is built around **natural-language interaction**. You do not need to memorize every trading term first. You can express intent the way you would speak to a trading assistant. The AI then turns that intent into executable actions or clear options. Before any sensitive action, it still asks for your confirmation.

This page gives **reference phrasing and keywords**. It is **not** a strict command language.

***

### Usage principles

1. **State the objective clearly**\
   Name the market, such as BTC or gold. Add your preferred margin size or notional range if that matters.
2. **State the risk boundary clearly**\
   Include your leverage preference and your TP or SL idea. You can describe them as prices, percentages, or simple natural-language rules.
3. **Confirm before execution**\
   Opening, closing, resizing, and leverage changes still depend on your explicit confirmation in the interface.
4. **Ask first when unsure**\
   If you only want analysis, say things like **"analyze only"** or **"do not place an order yet."**

***

### Reference: opening and managing positions

| Intent                         | Example phrasing                                                        |
| ------------------------------ | ----------------------------------------------------------------------- |
| Open a long or short at market | `Open a BTC long with XX USDC margin at 5x leverage.`                   |
| Place a limit entry            | `If BTC drops to 9xxxx, open a long with XX margin at x leverage.`      |
| Add or reduce size             | `Add XX USDC to my current BTC long.` or `Close half of this position.` |
| Fully close a position         | `Close the entire position.` or `Close my position on this market.`     |
| Adjust margin                  | `Add XX USDC margin to this position.`                                  |
| Set TP or SL                   | `Take profit at X%.` or `Stop loss at Y.`                               |

You can use common English tickers or plain asset names. Supported markets always depend on the live platform listing. You can also ask which markets are currently available.

***

### Reference: account and information requests

| Intent                          | Example phrasing                                                    |
| ------------------------------- | ------------------------------------------------------------------- |
| Check current positions and PnL | `What positions do I have right now?` or `What is my floating PnL?` |
| Check account and fees          | `Show my account.` or `Show my recent fees and funding.`            |
| Check trading rules             | `What is the minimum margin?` or `How often is funding charged?`    |

***

### Reference: insurance questions

If the product currently shows insurance entry points for your account, you can ask about the mechanism in natural language. Premiums, availability, and duration always follow the confirmation screen.

Example questions:

* `What is the difference between Zero Loss Insurance and Double Profit Insurance?`
* `Can I add Zero Loss Insurance to this BTC position?`
* `How long can this position be insured?`

***

### What not to ask for

* Do not expect fully unattended profit generation. The assistant supports analysis and execution flow. Decision-making and signing authority still stay with you.
* Do not send your private key, mnemonic, or complete seed phrase in chat. No legitimate workflow should require that.

***

### Voice and multilingual input

* **Voice**\
  If voice input is enabled in the client, spoken input follows the same confirmation flow as typed input.
* **Mixed-language input**\
  Simple mixed-language prompts can still work. If the meaning is unclear, the assistant asks you to confirm.
