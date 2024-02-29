# Supported types and blockchain networks

### Types of notifications you can monitor

Tatum supports various types of notifications on a chain, which are designed to cover a wide range of blockchain events. These are the notifications types we offer :

<details>

<summary>Incoming Transaction Notifications 📭 : </summary>

1. [**Incoming Native Transactions**](notification-types/incoming-native-transactions.md)**:** This notification is triggered when an address you are subscribed to, receives some [Native Token](../../learn-blockchain/basics/what-is-a-token-on-blockchain/what-are-native-tokens.md) from any address.
2. [**Incoming Internal Transactions**](notification-types/incoming-internal-transactions.md)**:** This notification is triggered when an address you are subscribed to, receives an [Internal transaction](../../learn-blockchain/basics/what-are-transactions/what-are-internal-transactions.md) (such as transfer an asset by a smart contract).
3. [**Incoming Fungible Transactions**](notification-types/incoming-tokens.md)**:** This notification is triggered when an address you are subscribed to, receives a [Fungible token](../../learn-blockchain/basics/what-is-a-token-on-blockchain/what-are-fungible-tokens.md) from any address.
4. [**Incoming NFT Transactions**](notification-types/incoming-nfts.md): This notification is triggered when an address you are subscribed to, receives a [Non Fungible Token](../../learn-blockchain/basics/what-is-a-token-on-blockchain/what-are-non-fungible-tokens.md) (NFT's) from any address.
5. [**Incoming MultiToken Transactions**](notification-types/incoming-multitokens.md): This notification is triggered when an address you are subscribed to, receives [MultiToken](../../learn-blockchain/basics/what-is-a-token-on-blockchain/what-are-multitokens.md) from any address.

</details>

<details>

<summary>Outgoing Transaction Notifications ✈️ : </summary>

1. [**Outgoing Native Transactions**](notification-types/outgoing-native-transactions.md): This notification is triggered when an address you are subscribed to, sends some [Native Token](../../learn-blockchain/basics/what-is-a-token-on-blockchain/what-are-native-tokens.md) to any address.
2. [**Outgoing Internal Transactions**](notification-types/outgoing-internal-transactions.md): This notification is triggered when an smart contract address you are subscribed to, sends assets to another address ([Internal transaction](../../learn-blockchain/basics/what-are-transactions/what-are-internal-transactions.md)).
3. [**Outgoing Fungible Transactions**](notification-types/outgoing-nfts.md): This notification is triggered when an address you are subscribed to, send's [Fungible tokens](../../learn-blockchain/basics/what-is-a-token-on-blockchain/what-are-fungible-tokens.md) to any address.
4. [**Outgoing NFT Transactions**](notification-types/outgoing-nfts.md): This notification is triggered when an address you are subscribed to, sends a [Non Fungible Token](../../learn-blockchain/basics/what-is-a-token-on-blockchain/what-are-non-fungible-tokens.md) (NFT's) to any address.
5. [**Outgoing MultiToken Transaction**](notification-types/outgoing-multitokens.md): This notification is triggered when an address you are subscribed to, sends a [MultiToken](../../learn-blockchain/basics/what-is-a-token-on-blockchain/what-are-multitokens.md) to any address.
6. [**Outgoing Failed Transactions**](notification-types/outgoing-failed-transactions.md): This notification is triggered when an address you are subscribed to, initiates any transaction but it failed due to any [reason](../../learn-blockchain/basics/what-are-transactions/what-are-the-reasons-a-transaction-fails.md).

</details>

<details>

<summary>Special Abstraction Notifications 🔔 :</summary>

1. [**Address Events**](notification-types/address-event.md): This notification is triggered when a user either receives or sends any token to any address on blockchain.
2. [**Paid Fee**](notification-types/paid-fee.md): This notification is triggered when a fee is paid as part of a transaction involving a specific address.
3. [**Failed Transactions in a Block** ](notification-types/failed-transactions-in-a-block.md): This notification is triggered when a block containing failed transactions is detected. This notification can be useful for monitoring and analysing failed transactions within specific blocks.
4. [**Contract Address Log Event :**](notification-types/contract-address-log-event.md) This notification allows you to monitor specific custom log events of a smart contract.

</details>

These notification types allow users to monitor a wide range of events on the blockchain, enabling them to build responsive and efficient applications.

### Blockchain protocols you can work with

{% hint style="info" %}
Every type of notification has its [own guide](notification-types/), where all the supported blockchain for that type is mentioned.
{% endhint %}

Each of the notification types provided by Tatum can be used across various blockchains, depending on the blockchain family. These families include&#x20;

1. UTXO (Unspent Transaction Output) chains :&#x20;
   1. Bitcoin
   2. Litecoin
   3. Dogecoin
   4. Bitcoin Cash
2. EVM (Ethereum Virtual Machine) chains :&#x20;
   1. Ethereum
   2. Binance Smart Chain
   3. Polygon
   4. Chilliz
   5. Celo
   6. Klaytn
   7. Flare
3. Other Blockchains
   1. Solana
   2. XRP
   3. Tron

By offering compatibility with different blockchain families, Tatum ensures that users can effectively monitor and respond to a diverse range of events, irrespective of the underlying blockchain technology
