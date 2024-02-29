# Show fungible token history of a wallet

### Overview

Fungible token transfers are critical in blockchain networks. They are used as a means of value exchange in cryptocurrency systems like Bitcoin and Ethereum. Beyond just transactions, they're also transferred into smart contracts in DeFi spaces for participation in liquidity pools or lending protocols. In Decentralised Autonomous Organisations (DAOs), governance tokens, a type of fungible token, are transferred to represent voting rights, enabling holders to have a say in network decisions. The versatility of fungible tokens and their transferability underscores the profound utility they bring to the blockchain ecosystem.

{% embed url="https://codepen.io/tatum-devrel/pen/oNQJMPG" %}

### How to show the fungible token history of a specific wallet on the Ethereum network

Use the TatumSDK (`@tatumio/tatum`) to get a transaction history of the wallet.

{% tabs %}
{% tab title="TypeScript" %}
{% code overflow="wrap" lineNumbers="true" %}
```typescript
// yarn add @tatumio/tatum
import { TatumSDK, Network, Ethereum, ResponseDto, Transaction } from '@tatumio/tatum'

const tatum = await TatumSDK.init<Ethereum>({network: Network.ETHEREUM})

const txs: ResponseDto<Transaction[]> = await tatum.token.getAllFungibleTransactions({
        addresses: ['0x78E851C35326c9296485E9720D85CB3Bd153b428'], // replace with your address
      })

console.log(txs.data)
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
    const txs = await tatum.token.getAllFungibleTransactions({
        addresses: ['0x78E851C35326c9296485E9720D85CB3Bd153b428'], // replace with your address
      })
    console.log(txs.data);
  } catch (error) {
    console.error("Error fetching wallet history:", error);
  }
})();
```
{% endcode %}
{% endtab %}

{% tab title="curl" %}
{% code overflow="wrap" lineNumbers="true" %}
```bash
curl --location --request GET 'https://api.tatum.io/v4/data/transactions?addresses=0x78E851C35326c9296485E9720D85CB3Bd153b428&chain=ethereum&transactionTypes=fungible'
```
{% endcode %}
{% endtab %}
{% endtabs %}

<details>

<summary>Expected Response</summary>

```json5
[
  {
    "chain":"ethereum-mainnet",
    "blockNumber":17463011,
    "hash":"0x3509d471bf8362f4bffcfec8d27b0d1d6af3d3520dbd72f2aad61cfb8e22417f",
    "transactionType":"fungible",
    "transactionIndex":60,
    "tokenAddress":"0xdac17f958d2ee523a2206206994597c13d831ec7",
    "amount":"3900",
    "timestamp":1686561155000,
    "address":"0x78e851c35326c9296485e9720d85cb3bd153b428",
    "counterAddress":"0x54157126f10ed5019ab2785cd8f1ced207d10346",
    "transactionSubtype":"incoming"
  }
]
```

</details>

### Request interface

{% code overflow="wrap" lineNumbers="true" %}
```typescript
interface GetAllFungibleTransactionsQuery {
  /**
   * Token contract address
   */
  tokenAddress?: string
  /**
   * Addresses to fetch. Up to 10 addresses as a comma separated string.
   */
  addresses: string[]
  /**
   * Optional transaction type. If not specified, both incoming and outgoing transactions are returned.
   */
  transactionTypes?: TransactionType[]
  /**
   * Optional from block. If not specified, all transactions are returned from the beginning of the blockchain.
   */
  blockFrom?: number
  /**
   * Optional to block. If not specified, all transactions are returned up till now.
   */
  blockTo?: number
  /**
   * Optional page size. If not specified, the default page size is used, which is 10.
   */
  pageSize?: number
  /**
   * Optional page number. If not specified, the first page is returned.
   */
  page?: number
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

interface Transaction {
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
  transactionType: 'fungible' | 'nft' | 'multitoken' | 'native' | 'internal'
  /**
   * Transaction sub type
   */
  transactionSubtype: 'incoming' | 'outgoing' | 'zero-transfer'
  /**
   * Index of the transaction in the block
   */
  transactionIndex: number
  /**
   * Address of the token collection
   */
  tokenAddress?: string
  /**
   * The ID of the token involved in the transaction (optional).
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
   */
  counterAddress?: string
}
```
{% endcode %}

### Supported blockchain networks

| Network                                                                                                                              | Support                             |
| ------------------------------------------------------------------------------------------------------------------------------------ | ----------------------------------- |
| <p>Ethereum / Ethereum Sepolia<br>BNB Smart Chain / BNB Smart Chain Testnet<br>Celo / Celo Alfajores<br>Polygon / Polygon Mumbai</p> | Multiple addresses per 1 invocation |
