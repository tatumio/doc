# Trace the history of a specific NFT

As the popularity of non-fungible tokens (NFTs) continues to surge, it becomes increasingly important for creators, collectors, and traders to monitor the transaction history of individual NFTs. This guide introduces you to the operation of obtaining all transactions for a specific NFT, providing a detailed overview of its transfer, trading, and ownership history. By leveraging this functionality, you can gain insights into the provenance and value of an NFT, assess its authenticity, and make informed decisions about buying, selling, or holding it. Ultimately, this operation enables you to navigate the dynamic NFT market with confidence and manage your digital assets more effectively.

### How to trace the history of a specific NFT on the Ethereum network

Use the TatumSDK (`@tatumio/tatum`) to get a transaction history of the NFT.

{% tabs %}
{% tab title="TypeScript" %}
{% code overflow="wrap" lineNumbers="true" %}
```typescript
// yarn add @tatumio/tatum
import {TatumSDK, Network, Ethereum, ResponseDto, NftTransaction} from '@tatumio/tatum'

const tatum = await TatumSDK.init<Ethereum>({network: Network.ETHEREUM})

const txs: ResponseDto<NftTransaction[]> = await tatum.nft.getAllNftTransactions({
  tokenId: '14721',
  tokenAddress: '0xccb9d89e0f77df3618eec9f6bf899be3b5561a89', // replace with your collection
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
    const txs = await tatum.nft.getAllNftTransactions({
      tokenId: '14721',
      tokenAddress: '0xccb9d89e0f77df3618eec9f6bf899be3b5561a89', // replace with your collection
    });
    console.log(txs.data);
  } catch (error) {
    console.error("Error fetching wallet balance:", error);
  }
})();
```
{% endcode %}
{% endtab %}

{% tab title="curl" %}
{% code overflow="wrap" lineNumbers="true" %}
```bash
curl --location --request GET 'https://api.tatum.io/v4/data/transactions?tokenAddress=0xccb9d89e0f77df3618eec9f6bf899be3b5561a89&tokenId=14721&chain=ethereum'
```
{% endcode %}
{% endtab %}
{% endtabs %}

{% embed url="https://codepen.io/tatum-devrel/pen/MWzZXxZ" %}

<details>

<summary>Expected Response</summary>

<pre class="language-json5"><code class="lang-json5"><strong>[
</strong>  {
    "chain": "ethereum-mainnet",
    "hash": "0xbbac7d1a2196c5148958bcf4ef05658f8220ca3f0ce1ff6ae9e87f67b9c940c5",
    "address": "0x727ea45b2eb6abb2badd3dc7106d146e0dc0450d",
    "blockNumber": 14568283,
    "transactionIndex": 34,
    "transactionType": "nft",
    "transactionSubtype": "incoming",
    "amount": "1",
    "timestamp": 1649733396000,
    "tokenId": "14721",
    "tokenAddress": "0xccb9d89e0f77df3618eec9f6bf899be3b5561a89",
    "counterAddress": "0x0000000000000000000000000000000000000000"
  },
  {
    "chain": "ethereum-mainnet",
    "hash": "0xbbac7d1a2196c5148958bcf4ef05658f8220ca3f0ce1ff6ae9e87f67b9c940c5",
    "address": "0x0000000000000000000000000000000000000000",
    "blockNumber": 14568283,
    "transactionIndex": 34,
    "transactionType": "nft",
    "transactionSubtype": "outgoing",
    "amount": "-1",
    "timestamp": 1649733396000,
    "tokenId": "14721",
    "tokenAddress": "0xccb9d89e0f77df3618eec9f6bf899be3b5561a89",
    "counterAddress": "0x727ea45b2eb6abb2badd3dc7106d146e0dc0450d"
  }
]
</code></pre>

</details>

### Request interface

{% code overflow="wrap" lineNumbers="true" %}
```typescript
interface GetAllNftTransactionsQuery {
  /**
   * Token ID
   */
  tokenId: string
  /**
   * Token contract address
   */
  tokenAddress: string
  /**
   * Optional transaction type. If not specified, both incoming and outgoing transactions are returned.
   */
  transactionType?: 'incoming' | 'outgoing'
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

interface NftTransaction {
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
  transactionIndex: number
  /**
   * Address of the token collection
   */
  tokenAddress: string
  /**
   * Token ID
   */
  tokenId: string
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
  counterAddress: string
}
```
{% endcode %}

### Supported blockchain networks

<table><thead><tr><th width="417">Network</th><th>Support</th></tr></thead><tbody><tr><td>Ethereum / Ethereum Sepolia / Ethereum Goerli<br>BNB Smart Chain / BNB Smart Chain Testnet<br>Celo / Celo Alfajores<br>Polygon / Polygon Mumbai</td><td>NFTs (BAYC,...)<br>ERC-1155 Tokens</td></tr></tbody></table>

