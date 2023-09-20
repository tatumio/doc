# Show the NFT history of a wallet

As non-fungible tokens (NFTs) gain traction in the world of digital assets, it becomes increasingly essential for users to manage and monitor their NFT-related transactions across various blockchain networks. This guide introduces you to obtaining all NFT transactions for a specific wallet, offering a comprehensive view of your NFT wallet history. By leveraging this functionality, you can effectively track the acquisition, transfer, and sale of NFTs associated with your wallet, analyze your trading patterns, and maintain accurate records for tax or accounting purposes. Ultimately, this operation empowers you to take full control of your unique digital assets and navigate the ever-evolving NFT landscape with greater ease and efficiency.

### How to show the NFT history of a specific wallet on the Ethereum network

Use the TatumSDK (`@tatumio/tatum`) to get a transaction history of the wallet.

{% tabs %}
{% tab title="TypeScript" %}
{% code overflow="wrap" lineNumbers="true" %}
```typescript
// yarn add @tatumio/tatum
import {TatumSDK, Network, Ethereum, ResponseDto, NftTransaction} from '@tatumio/tatum'

const tatum = await TatumSDK.init<Ethereum>({network: Network.ETHEREUM})

const txs: ResponseDto<NftTransaction[]> = await tatum.nft.getAllNftTransactionsByAddress({
  addresses: ['0x727ea45b2eb6abb2badd3dc7106d146e0dc0450d'], // replace with your address
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
    const txs = await tatum.nft.getAllNftTransactionsByAddress({
      addresses: ['0x727ea45b2eb6abb2badd3dc7106d146e0dc0450d'], // replace with your address
    });
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
curl --location --request GET 'https://api.tatum.io/v4/data/transactions?addresses=0x727ea45b2eb6abb2badd3dc7106d146e0dc0450d&chain=ethereum'
```
{% endcode %}
{% endtab %}
{% endtabs %}

{% embed url="https://codepen.io/tatum-devrel/pen/qBQLKGO?editors=1111" %}

###

<details>

<summary>Expected Response</summary>

```javascript
[
  {
    "chain": "ethereum-mainnet",
    "hash": "0x3d5dafbb461ae5b1a485756c345779ed7e0a21ca4d8e2d59fb3453a7c38131b9",
    "address": "0x727ea45b2eb6abb2badd3dc7106d146e0dc0450d",
    "blockNumber": 17029923,
    "transactionIndex": 79,
    "transactionType": "nft",
    "transactionSubtype": "outgoing",
    "amount": "-0.2",
    "timestamp": 1681278035000,
    "counterAddress": "0x64ceaaf5df1be80f29f35589f096f0714f458b40"
  }
]
```

</details>

### Request interface

{% code overflow="wrap" lineNumbers="true" %}
```typescript
interface GetAllNftTransactionsByAddress {
  /**
   * Addresses to get NFT transactions from.
   */
  addresses: string[]
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

