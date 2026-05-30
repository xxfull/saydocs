---
icon: window
cover: .gitbook/assets/yesfichain.png
coverY: 0
metaLinks: {}
---

# YesFi Chain Explorer

YesFi Chain Explorer is the **official block explorer** for YesFi Chain. It is aimed at developers and end users who need **live on-chain lookup and visualization**—transactions, addresses, and blocks—without calling node RPC directly.

**Explorer URL:** [https://explorer.sayfi.com/](https://explorer.sayfi.com/)

***

### Feature overview

| Module              | Description                                             |
| ------------------- | ------------------------------------------------------- |
| Global search       | Query by address / transaction hash / block height      |
| Latest transactions | Live feed of recent on-chain transactions, auto-refresh |
| Transaction detail  | Full information and payload for a single transaction   |
| Address detail      | Wallet balance and historical transactions              |

***

### Core features

#### 1. Global search

The home page provides a single search box. Supported query types:

```
Search by Address / Txn Hash / Block
```

| Query type       | Example format                                  | Notes               |
| ---------------- | ----------------------------------------------- | ------------------- |
| Wallet address   | `0x50947b54c6240f5f6c6c832468a4fc9ae09e5d09`    | Balance and history |
| Transaction hash | `0x3ea36306c8b01fb1831c578c65afa57f631f0a19...` | Single transaction  |
| Block height     | `9035608`                                       | Block details       |

***

#### 2. Latest transactions

The home page lists the newest on-chain transactions. By default the list **refreshes every 2 seconds**; you can also click **Refresh** manually.

Column reference:

| Field          | Description                                                           |
| -------------- | --------------------------------------------------------------------- |
| **HASH**       | Transaction hash (truncated; click through to detail)                 |
| **ACTION**     | Type; currently `OPEN POSITION` / `CLOSE POSITION`                    |
| **BLOCK**      | Block height                                                          |
| **TIME (UTC)** | Time in UTC                                                           |
| **ADDRESS**    | Sending wallet address                                                |
| **AMOUNT**     | Asset amount (**positive** = inflow, **negative** = outflow), in USDC |

**Sample rows:**

```
HASH                          ACTION          BLOCK     TIME(UTC)   ADDRESS                    AMOUNT
0xae402346...550f7491         OPEN POSITION   9035809   10:59:40    0x50947b54...e09e5d09      -10 USDC
0x3ea36306...ca7e4d56         CLOSE POSITION  9035608   10:59:20    0x50947b54...e09e5d09      9.8205789013 USDC
```

***

#### 3. Transaction detail (Transaction Information)

Click any transaction hash to open its detail page.

**Fields:**

| Field                | Description                                  |
| -------------------- | -------------------------------------------- |
| **Transaction Hash** | Full hash (hex), copy supported              |
| **Status**           | e.g. `Completed` / pending / failed          |
| **Timestamp**        | On-chain time in UTC (`YYYY-MM-DD HH:mm:ss`) |
| **Block**            | Height; link to block view                   |
| **Address**          | Sender; link to address view                 |
| **Action**           | Type (e.g. `CLOSE POSITION`)                 |
| **Amount**           | Amount and asset (e.g. `9.8205789013 USDC`)  |
| **Payload**          | Raw business data (JSON)                     |

**Payload example:**

```json
{
  "asset": "USDC",
  "amount": "9.8205789013"
}
```

**Full transaction example:**

```
Transaction Hash: 0x3ea36306c8b01fb1831c578c65afa57f631f0a19893e14b85abb815bca7e4d56
Status:           Completed
Timestamp:        2026-04-27 10:59:20
Block:            9035608
Address:          0x50947b54c6240f5f6c6c832468a4fc9ae09e5d09
Action:           CLOSE POSITION
Amount:           9.8205789013 USDC
```

***

#### 4. Address detail (Address Details)

Search for an address or follow an address link to open the address page.

**Summary at top:**

| Field                  | Description                      |
| ---------------------- | -------------------------------- |
| **Address**            | Full address, copy supported     |
| **Balance**            | Current balance (USDC)           |
| **Total Transactions** | Count of historical transactions |

**Address example:**

```
Address:             0x50947b54c6240f5f6c6c832468a4fc9ae09e5d09
Balance:             6.52466711 USDC
Total Transactions:  17
```

**History table columns:**

| Field              | Description                                |
| ------------------ | ------------------------------------------ |
| **Tx Hash**        | Hash (click for detail, copy supported)    |
| **Action**         | `OPEN POSITION` / `CLOSE POSITION`         |
| **Block**          | Height (click through)                     |
| **DateTime (UTC)** | `YYYY-MM-DD HH:mm:ss`                      |
| **Amount**         | Change (**positive** in, **negative** out) |

***

### Typical workflows

#### 1. Confirm a transaction landed on-chain

1. Copy the transaction hash from your wallet or app.
2. Paste it into the Explorer search box and run **Search**.
3. Check **Status**—`Completed` means the transaction is confirmed on-chain.

#### 2. Review address / position history

1. Search for the wallet address.
2. On the address page, check **Total Transactions** and the history list.
3. Review `OPEN POSITION` and `CLOSE POSITION` rows to reason about flows and PnL.

#### 3. Development and debugging

When integrating with YesFi, use Explorer to verify:

* Contract interactions produced the expected on-chain records
* **Payload** shape matches expectations
* Block time and ordering

***

### Data reference

#### Amount rules

| Display             | Meaning                                                     |
| ------------------- | ----------------------------------------------------------- |
| `-10 USDC`          | User pays 10 USDC (open)                                    |
| `9.8205789013 USDC` | User receives this amount (close, including PnL settlement) |

> Up to **10** decimal places may be shown; final values follow on-chain settlement.

#### Time format

All times are **UTC**:

```
List view:     HH:mm:ss
Detail view:   YYYY-MM-DD HH:mm:ss
```

#### Address format

Standard EVM address:

```
0x + 40 hexadecimal characters
Example: 0x50947b54c6240f5f6c6c832468a4fc9ae09e5d09
```

***

### FAQ

**Q: Transaction status does not update?**

The latest-transactions list auto-refreshes about every **2 seconds**. For a specific transaction, reload the page or use **Refresh**. If a tx never appears, check connectivity and whether it was **broadcast** to the chain.

**Q: Address search returns nothing?**

The address may have **no on-chain activity yet**. The explorer only shows addresses that already have records.

**Q: What is the Payload field?**

**Payload** is structured business data (JSON) attached to the transaction and written by the upper-layer protocol (e.g. YesFi)—asset type, amount, and related fields.
