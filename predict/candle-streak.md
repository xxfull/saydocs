# Candle Streak

### Overview

Each Candle Streak round lasts 60 seconds and is made up of six 10-second candles. Before the round starts, you predict how these six candles will move. If your card hits, you receive a payout at the payout multiple locked when you placed the order; if it misses, you lose the order amount.

| Item          | Details                                                                                                                           |
| ------------- | --------------------------------------------------------------------------------------------------------------------------------- |
| Underlying    | BTC-USD                                                                                                                           |
| Round length  | 60 seconds, six 10-second candles                                                                                                 |
| Modes         | Count only: predict how many of the 6 candles close up, down or flat. Exact order: predict the direction of each candle, in order |
| Order amount  | 1–500 USDC, with a Custom amount option                                                                                           |
| Order cut-off | Orders are accepted until the next round starts                                                                                   |
| Maximum loss  | The order amount                                                                                                                  |

### How each candle is classified: up, flat or down

Each candle's result is determined by comparing its close price with its open price. Both prices are taken from the price source and compared at two decimal places:

| Result | Condition    |
| ------ | ------------ |
| Up     | Close > Open |
| Flat   | Close = Open |
| Down   | Close < Open |

For example, with an open price of 75,981.00: a close of 75,981.00 is flat; 75,981.01 is up; 75,980.99 is down. The three results never overlap, and every mode uses the same rule.

When a card hits:

* Count only: exactly N of the 6 candles move in the direction you chose.
* Exact order: all 6 candles in the round must match the card from left to right. The same number of ups and downs in a different order is still a miss. Exact order cards contain only up and down, so any flat candle means the card misses.

### How We Price Candle Streak with Options

One minute, six 10-second candles: together they make one Candle Streak card, and the card hits only if all six candles move as you predicted. So what is that card worth?

This is the same question the options market answers every day.

The basic approach to option pricing is to weight the payout of every possible outcome at expiry by its probability and add them up. Every option in Candle Streak is all-or-nothing: the payout is fixed, paid at the payout multiple if the card hits and zero if it misses. So the question comes down to one thing: how likely is it to pay out?

We answer it in four steps. First, we **break down** the card into a set of options that each expire in 10 seconds. Next, we **price** each one based on current market conditions. Then we **combine** them according to the card's rules. Finally, we add a disclosed spread to form the **quote**. As a result, the payout multiple reflects market conditions right now, not how often a pattern has appeared in the past.

That is the idea behind Candle Streak: **carry option pricing logic in the most intuitive form possible**. You don't need to understand strikes, expiries or Greeks; you only need to judge where the candles will go over the next minute. Behind every payout multiple is a set of options priced on current market conditions. Built on the candlestick chart traders know best, it is a lightweight product you can complete in 60 seconds, and also an entry point to options: every call you make is a hands-on lesson in probability and price.

#### Break down: one candle, three all-or-nothing options

An option has three elements: an underlying, a strike and an expiry. In Candle Streak, the underlying is BTC, the expiry is the moment the candle closes, and the strike is the candle's open price. Unlike a standard option, this strike is not fixed when you place the order; it is set automatically at the price when the candle opens. In the industry this is called a **Forward-Start Option**.

Each direction you choose is equivalent to buying an **All-or-Nothing Option (also known as a Digital Option)**. What sets it apart from a standard option is how it pays out. A standard option pays more the further the price moves in your favor; an all-or-nothing option only asks whether a condition is met. If it is, you receive a fixed payout at the payout multiple; if not, you lose the order amount. There is no partial payout.

| Your direction | What it is in the options market                       | When it pays |
| -------------- | ------------------------------------------------------ | ------------ |
| Up             | Digital call, strike = open price                      | Close > Open |
| Down           | Digital put, strike = open price                       | Close < Open |
| Flat           | The case where neither the up nor the down option pays | Close = Open |

In other words, **the moment a candle opens, three all-or-nothing options go live at once**, all expiring when the candle closes: Up covers everything above the open price, Down covers everything below it, and Flat covers only the open price itself. The three never overlap and every possible close falls into exactly one of them, so their probabilities always add up to 100%, and one rises only as the others fall. When the market quiets down and a flat close becomes more likely, the chances of up and down fall together. It also means the three options cannot be priced in isolation; they must be priced together within a single probability framework.

<figure><img src="../.gitbook/assets/image (4).png" alt=""><figcaption></figcaption></figure>

#### Price: what each option is worth depends on current market conditions

The next question is: how likely is the candle to close up, flat or down? This is where option pricing comes in, and it can be broken into two steps.

**Step 1: Did the price move in these 10 seconds?** A close that matches the open to the cent almost only happens when the market is quiet and the price hasn't changed within the 10 seconds. So the chance of a flat close reflects how active the market is: the more active, the fewer flat closes. Taking Binance BTCUSDT data from November 1–15, 2026 as an example, about 15% of all 10-second candles closed flat; by hour, about 1% in active hours and about 39% in quiet hours (such as weekends and late nights).

<figure><img src="../.gitbook/assets/image (5).png" alt=""><figcaption></figcaption></figure>

**Step 2: If it moved, which way?** In standard option pricing models, a digital option struck at the current price (an at-the-money digital option) is worth close to half its payout when the time to expiry is very short: the price is about as likely to go up as down. Ten seconds is too short for any meaningful directional drift, so once the price moves, up and down are roughly equally likely, and the probability taken up by a flat close is shared evenly between them. The flat-close probability is estimated from recent trading data and keeps updating with market activity. That is also why the payout multiple changes when market activity changes (see Section 4).

#### Combine: six options make one card

Six candles in a round are six options expiring one after another, and a card is a combination of them. This is how structured products are priced: price each component first, then assemble the whole according to the rules.

| Mode        | Equivalent structure | When it pays                                                      |
| ----------- | -------------------- | ----------------------------------------------------------------- |
| Exact order | Digital Strip        | All 6 options pay out, in order                                   |
| Count only  | Digital Basket       | Exactly N options in the basket pay out, regardless of which ones |

One market feature also matters when combining them: short-term price movements have momentum. If one candle closes up, the next is slightly more likely to close up again than to reverse, and vice versa. In Binance BTCUSDT 10-second candles from November 1–15, 2026, about 42% of all candles closed up, while after an up candle about 48% of the next candles also closed up; the same holds for down moves. So in Exact order, patterns with a consistent direction (such as all up or all down) are more likely, which means a higher price and a lower payout multiple; patterns that keep switching (such as alternating up and down) are less likely, which means a lower price and a higher payout multiple.

#### Quote: fair price plus a platform spread

Imagine every Candle Streak card is designed to pay 1 USDC if it hits and 0 if it misses. Its fair price is then roughly equal to its probability of hitting, which gives the price an intuitive meaning: a card quoted at 0.20 USDC means that, based on current market conditions, there is roughly a 20% chance that the six candles move as you predicted. The higher the price, the higher that chance.

When options market makers quote prices, they add a spread on top of the fair price as compensation for the risk they take. Candle Streak works the same way: quote = fair price + platform spread, and the spread is already included in the payout multiple shown on the page.

To keep things intuitive, the page does not show the contract price directly. Instead, it converts it into a payout multiple: the payout you receive for every 1 USDC of order amount if the card hits (including the order amount). The lower the contract price, the higher the payout multiple; the harder a card is to hit, the higher its payout multiple. For example, a quote of 0.20 USDC corresponds to 5.00x: an order of 10 USDC pays 50 USDC if it hits. Payout multiples are shown to two decimal places.

### When the payout multiple changes and when it is locked

The payout multiple changes because the pricing inputs change, not because the model changes.

In the options market, the same option has no fixed price: the pricing model stays the same, inputs such as volatility update in real time, and market makers recalculate their quotes accordingly. Candle Streak works the same way. The pricing model is fixed, and the core input that keeps updating with the market is the probability of a flat close. When the market is active, the price changes in almost every 10-second candle, flat closes are rare, the payout multiple for Flat goes up and the payout multiples for Up and Down go down. When the market is quiet (for example on weekends or late at night), the price often stays put, flat closes become more common, the payout multiple for Flat goes down and the payout multiples for Up and Down go up.

Pricing inputs such as the flat-close probability are updated every 60 seconds (once per round), and payout multiples are refreshed accordingly. Payout multiples are not based on how often a pattern has appeared recently, so a pattern that has been rare in the past does not get a higher payout multiple for that reason.

Your payout multiple is locked when you tap to confirm your order, and your order settles at that locked multiple.

### Settlement

Candle prices come from the YesFi composite index price: the system pulls quotes from multiple external exchanges in real time, filters out anomalies and calculates a weighted price. For details on price sources and methodology, see [Pricing](https://docs.yesfi.com/perps/market-and-limit/pricing).

* Open price: equal to the close price of the previous candle
* Close price: the weighted price calculated from multiple external exchange quotes when the candle ends
* Price precision: open and close prices are compared at two decimal places
* Feed interruption: if third-party quotes are temporarily unavailable, the platform fills in quotes at the current price every second, so every candle always has a complete open and close price

Each round settles automatically when it ends, and payouts are credited directly to your account. The top of the candlestick chart shows all six candles for every round, so you can check the result candle by candle. Each order's opening and settlement transaction hashes are available in your order history and can be verified in the block explorer.

### Limits and maximum payout

| Limit                            | Value                                |
| -------------------------------- | ------------------------------------ |
| Order amount                     | 1–500 USDC, up to two decimal places |
| Maximum payout multiple per card | 600x                                 |

The maximum payout for a single order is 600 times the order amount. Orders that would exceed this limit are rejected.

### FAQ

**Why isn't the chance of a single candle closing up 50%?** Each candle can also close flat. A flat close takes up part of the probability, and up and down split the rest equally, so the chance of a single candle closing up is below 50%.

**When does a candle close flat?** A candle is flat when its close and open prices are exactly equal at two decimal places, for example an open of 75,981.00 and a close of 75,981.00. This usually happens when the market is quiet and the price hasn't changed within the 10 seconds, so flat closes are more common on weekends and late at night, and the payout multiple for Flat falls accordingly. When the market is active, flat closes are rare and the payout multiple for Flat rises.

**Does a 0.01 difference really count as up?** Yes. The result only depends on whether the close is higher or lower than the open, compared at two decimal places, so a 0.01 difference counts as up or down. Flat only means the price did not move at all during those 10 seconds.

**Can I choose multiple directions in the same round?** Yes. Each card settles separately at its own payout multiple, and the platform spread is included in each card individually.

**Why is the payout multiple different from what I saw when I picked the card?** Payout multiples refresh every 60 seconds and are locked when you tap to confirm your order; your order settles at the locked multiple. The multiple at the time of your order can be found in your order history.

**How can I verify the settlement result?** The top of the candlestick chart shows all six candles for every round, so you can check up, down and flat candle by candle against your card. The settlement price and result of each order are available in your order history.

### Risk disclosure

Each Candle Streak round lasts only 60 seconds. If your card misses, you lose the entire order amount. Payout multiples already include the platform spread. This page does not constitute investment advice. Only use funds you can afford to lose.
