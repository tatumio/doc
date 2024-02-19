---
description: This endpoint can help you get all the transactions of a wallet.
---

# Get all transactions on the wallet

{% embed url="https://codepen.io/tatum-devrel/pen/VwVqVwm" %}
Try this feature
{% endembed %}

As the world of digital assets expands, it becomes increasingly important for users to keep track of their transactions across various blockchain networks. The ability to retrieve all transactions associated with a particular address is an essential feature for managing and auditing your digital assets. This guide will introduce you to obtaining all transactions for a specific address, providing you with a comprehensive overview of your transaction history. By leveraging this functionality, you can effectively monitor your digital asset activities, verify past transactions, and maintain accurate records for tax or accounting purposes, ultimately gaining greater control over your financial assets in the digital landscape.

### How to get wallet transactions on the Ethereum network

Use the TatumSDK (`@tatumio/tatum`) to get a transaction history of the wallet.

{% hint style="info" %}
TatumSDK wraps multiple different calls to the Tatum API together in 1 function, so curl example is not shown here. You can check the [API documentation](https://apidoc.tatum.io/tag/Data-API#operation/GetBalances) for specific operations, which are internally used [inside the library](https://github.com/tatumio/tatum-js/blob/master/src/service/address/address.ts).
{% endhint %}

{% hint style="warning" %}
Note : Some filters are in alpha for UTXO chains, thus you may experience inconsistencies.
{% endhint %}

{% tabs %}
{% tab title="TypeScript" %}
{% code overflow="wrap" lineNumbers="true" %}
```typescript
// yarn add @tatumio/tatum
import {TatumSDK, Network, Ethereum, ResponseDto, AddressTransaction} from '@tatumio/tatum'

const tatum = await TatumSDK.init<Ethereum>({network: Network.ETHEREUM})

const txs: ResponseDto<AddressTransaction[]> = await tatum.address.getTransactions({
  address: '0x514d547c8ac8ccbec29b5144810454bd7d3625ca', // replace with your address
})

console.log(txs.data)

// Expected outcome

```
{% endcode %}
{% endtab %}

{% tab title="JavaScript" %}
{% code overflow="wrap" lineNumbers="true" %}
```javascript
// Install with: npm install @tatumio/tatum
const { TatumSDK, Network } = require("@tatumio/tatum");

(async () => {
  try {
    const tatum = await TatumSDK.init({ network: Network.ETHEREUM });
    const txs = await tatum.address.getTransactions({
      address: '0x514d547c8ac8ccbec29b5144810454bd7d3625ca', // replace with your address
    });
    console.log(txs.data);
  } catch (error) {
    console.error("Error fetching wallet balance:", error);
  }
})();

// Expected outcome
// [{
//    address: '0x514d547c8ac8ccbec29b5144810454bd7d3625ca',
//    amount: '1',
//    blockNumber: 3325299,
//    chain: 'ethereum-sepolia',
//    counterAddress: '0x39d2ba91296029afbe725436b4824ca803e27391',
//    hash: '0xf4ef4715f9ba61f1fb606a32775a7bf281ddf7858092aeb3e0e0484d01957058',
//    timestamp: 1681982316000,
//    transactionIndex: 1,
//    transactionSubtype: 'incoming',
//    transactionType: 'native',
//  }]
```
{% endcode %}
{% endtab %}
{% endtabs %}

<details>

<summary>Expected Response</summary>

```javascript
[
    {
        address: '0x514d547c8ac8ccbec29b5144810454bd7d3625ca',
        amount: '1',
        blockNumber: 3325299,
        chain: 'ethereum-sepolia',
        counterAddress: '0x39d2ba91296029afbe725436b4824ca803e27391',
        hash: '0xf4ef4715f9ba61f1fb606a32775a7bf281ddf7858092aeb3e0e0484d01957058',
        timestamp: 1681982316000,
        transactionIndex: 1,
        transactionSubtype: 'incoming',
        transactionType: 'native',
    }
]
```

</details>

### How to get wallet transactions on the Bitcoin network

In order to get a transaction history of a Bitcoin address, you can use the same approach and reuse the same code.

{% tabs %}
{% tab title="TypeScript" %}
{% code overflow="wrap" lineNumbers="true" %}
```typescript
// yarn add @tatumcom/js
import {TatumSDK, Network, Bitcoin, ResponseDto, AddressTransaction} from '@tatumio/tatum'

const tatum = await TatumSDK.init<Bitcoin>({network: Network.BITCOIN_TESTNET})

const balance: ResponseDto<AddressTransaction[]> = await tatum.address.getTransactions({
  address: 'tb1qrd9jz8ksy3qqm400vt296udlvk89z96p443mv0', // replace with your address
})

console.log(balance.data)

/// Expected outcome
// [{
//    address: 'tb1qrd9jz8ksy3qqm400vt296udlvk89z96p443mv0',
//    amount: '0.001',
//    blockNumber: 2427655,
//    chain: 'bitcoin-testnet',
//    hash: '954b246cdebf7338f561e2fdfb869fedd75302e2b233f339639b36d880e9c983',
//    timestamp: 1680779879,
//    transactionType: 'incoming',
//  }]
```
{% endcode %}
{% endtab %}

{% tab title="JavaScript" %}
{% code overflow="wrap" lineNumbers="true" %}
```javascript
// Install with: npm install @tatumcom/js
const { TatumSDK, Network } = require("@tatumio/tatum");

(async () => {
  try {
    const tatum = await TatumSDK.init({ network: Network.BITCOIN_TESTNET });
    const txs = await tatum.address.getTransactions({
      address: "tb1qrd9jz8ksy3qqm400vt296udlvk89z96p443mv0", // replace with your address
    });
    console.log(txs.data);
  } catch (error) {
    console.error("Error fetching wallet transactions:", error);
  }
})();

// Expected outcome
// [{
//    address: 'tb1qrd9jz8ksy3qqm400vt296udlvk89z96p443mv0',
//    amount: '0.001',
//    blockNumber: 2427655,
//    chain: 'bitcoin-testnet',
//    hash: '954b246cdebf7338f561e2fdfb869fedd75302e2b233f339639b36d880e9c983',
//    timestamp: 1680779879,
//    transactionType: 'incoming',
//  }]
```
{% endcode %}
{% endtab %}
{% endtabs %}

You can see, that the same request and response is used for different blockchain networks.

### Request interface

{% code overflow="wrap" lineNumbers="true" %}
```typescript
export interface GetAddressTransactionsQuery {
  /**
   * Blockchain address to get transactions for.
   */
  address: string
  /**
   * Optional transaction type. If not specified, all transactions are returned. For networks that support only native transactions, this parameter is ignored.
   */
  transactionTypes?: ['fungible' | 'nft' | 'multitoken' | 'native']
  /**
   * Optional transaction type. If not specified, both incoming and outgoing transactions are returned.
   */
  transactionDirection?: 'incoming' | 'outgoing'
  /**
   * Optional from block. If not specified, all transactions are returned from the beginning of the blockchain.
   */
  fromBlock?: number
  /**
   * Optional to block. If not specified, all transactions are returned up till now.
   */
  toBlock?: number
  /**
   * Optional page size. If not specified, the default page size is used, which is 10.
   */
  pageSize?: number
  /**
   * Optional page number. If not specified, the first page is returned.
   */
  page?: number
  /**
   * Optional token address. If specified, only transactions related to this token (smart contract) are returned.
   */
  tokenAddress?: string
}
```
{% endcode %}

### Response interface

{% code overflow="wrap" lineNumbers="true" %}
```typescript
interface ResponseDto<T> {
  /**
   * Actual payload of the response
   */
  data: T
  /**
   * Status of the response
   */
  status: Status
  /**
   * In case of ERROR status, this field contains the error message and detailed description
   */
  error?: ErrorWithMessage
}

interface AddressTransaction {
  /**
   * Blockchain network
   */
  chain: string
  /**
   * Block number
   */
  blockNumber: number
  /**
   * Transaction hash
   */
  hash: string
  /**
   * Transaction type
   */
  transactionType: 'incoming' | 'outgoing' | 'zero-transfer'
  /**
   * Index of the transaction in the block
   */
  transactionIndex?: number
  /**
   * Address of the token collection, if the transaction is related to a token (ERC-20, ERC-721, ERC-1155)
   */
  tokenAddress?: string
  /**
   * Token ID, if the transaction is related to a NFT (ERC-721) or MutiToken (ERC-1155)
   */
  tokenId?: string
  /**
   * Amount transferred. For outgoing transactions, it's a negative number. For zero-transfer transactions, it's always 0. For incoming transactions, it's a positive number.
   */
  amount: string
  /**
   * Transaction timestamp - UTC millis
   */
  timestamp: number
  /**
   * Address, on which transaction occurred. This is receiver address for incoming transactions and sender address for outgoing transactions.
   */
  address: string
  /**
   * Counter address of the transaction. This is sender address for incoming transactions on `address` and receiver address for outgoing transactions on `address`.
   * Not all blockchain networks can identify the counter address (UTXO chains like Bitcoin e.g., where there is multiple senders or recipients). In this case, the counter address is not returned.
   */
  counterAddress?: string
}
```
{% endcode %}

### Supported blockchain networks

<table><thead><tr><th width="417">Network</th><th>Support</th></tr></thead><tbody><tr><td>Ethereum / Ethereum Sepolia / Ethereum Goerli<br>BNB Smart Chain / BNB Smart Chain Testnet<br>Celo / Celo Alfajores<br>Polygon / Polygon Mumbai<br>Chilliz</td><td>Native Assets<br>ERC-20 Tokens (USDT, USDC,...)<br>NFTs (BAYC,...)<br>ERC-1155 Tokens</td></tr><tr><td>Bitcoin / Bitcoin Testnet<br>Litecoin / Litecoin Testnet<br>Dogecoin / Dogecoin Testnet</td><td>Native Assets only</td></tr></tbody></table>

