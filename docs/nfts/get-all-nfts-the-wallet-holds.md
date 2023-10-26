---
description: >-
  This function helps you to fetch all the NFT's a wallet holds, all you have to
  do is pass the address to the function parameter and chain while initialising
  the sdk.
---

# Get all NFTs the wallet holds

The world of non-fungible tokens (NFTs) has witnessed exponential growth, attracting artists, collectors, and investors alike. As users accumulate various NFTs across multiple blockchain networks, it becomes crucial to manage and track their digital collections. This guide introduces you to the operation of obtaining all NFTs associated with a particular address, offering you a comprehensive snapshot of your NFT holdings. By leveraging this functionality, you can effectively monitor your NFT collection, verify ownership, and assess the value of your digital assets. Ultimately, this operation empowers you to take full control of your unique digital assets and manage them with greater ease and efficiency.

### How to get NFTs on a wallet in the Ethereum network

Use the TatumSDK (`@tatumio/tatum`) to get a balance of the wallet.

{% tabs %}
{% tab title="TypeScript" %}
{% code overflow="wrap" lineNumbers="true" %}
```typescript
// yarn add @tatumio/tatum
import {TatumSDK, Network, Ethereum, ResponseDto, NftAddressBalance} from '@tatumio/tatum'

const tatum = await TatumSDK.init<Ethereum>({network: Network.ETHEREUM})

const balance: ResponseDto<NftAddressBalance[]> = await tatum.nft.getBalance({
  addresses: ['0x727EA45B2EB6abb2badD3dC7106d146E0Dc0450d'], // replace with your address
})

console.log(balance.data)
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
    const balance = await tatum.nft.getBalance({
      addresses: ['0x727EA45B2EB6abb2badD3dC7106d146E0Dc0450d'], // replace with your address
    });
    console.log(balance.data);
  } catch (error) {
    console.error("Error fetching NFT balance:", error);
  }
})();
```
{% endcode %}
{% endtab %}

{% tab title="curl" %}
{% code overflow="wrap" lineNumbers="true" %}
```bash
curl --location --request GET 'https://api.tatum.io/v4/data/balances?chain=ethereum&addresses=0x727EA45B2EB6abb2badD3dC7106d146E0Dc0450d'
```
{% endcode %}
{% endtab %}
{% endtabs %}

{% embed url="https://codepen.io/tatum-devrel/pen/oNQJyJb" %}

<details>

<summary>Expected Response</summary>

```json5
[
    {
    "address": "0x727ea45b2eb6abb2badd3dc7106d146e0dc0450d",
    "balance": "2
    ",
    "chain": "ethereum-mainnet",
    "lastUpdatedBlockNumber": 14086122,
    "metadata": {
        "description": "# ***\"Sometimes I swear I can see .... | Joey Camacho ]*",
        "external_url": "https://punkscomic.com",
        "image": "ipfs://QmS21WhH94jBnYompXHD1SxS6Gw2bY8E81sTYRktWrYa7a/JUPITER.mp4",
        "name": "MetaHero Universe: Jupiter DAO Token"
    },
    "metadataURI": "ipfs://QmR9PokA9rnKKUF1uLtZyHYEhExqQU1Z7t8AbovMBxND4U/5",
    "tokenAddress": "0x7deb7bce4d360ebe68278dee6054b882aa62d19c",
    "tokenId": "5",
    "type": "multitoken"
    }
]
```

</details>

### Request interface

{% code overflow="wrap" lineNumbers="true" %}
```typescript
interface AddressBalanceDetails {
  /**
   * List of addresses to check.
   */
  addresses: string[]
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

interface NftAddressBalance {
  /**
   * Balance of the address.
   */
  balance: string
  /**
   * Blockchain network
   */
  chain: string
  /**
   * Token ID
   */
  tokenId: string
  /**
   * Token contract address
   */
  tokenAddress: string
  /**
   * Token type. Either 'nft' (ERC-721) or 'multitoken' (ERC-1155)
   */
  type: 'nft' | 'multitoken'
  /**
   * Token URI
   */
  metadataURI: string
  /**
   * Token metadata
   */
  metadata?: {
    name: string
    description: string
    image: string
    [metadataKey: string]: unknown
  }
  /**
   * Block number of the last balance update.
   */
  lastUpdatedBlock: number
}
```
{% endcode %}

### Supported blockchain networks

<table><thead><tr><th width="417">Network</th><th>Support</th></tr></thead><tbody><tr><td>Ethereum / Ethereum Sepolia / Ethereum Goerli<br>BNB Smart Chain / BNB Smart Chain Testnet<br>Celo / Celo Alfajores<br>Polygon / Polygon Mumbai</td><td>Multiple addresses per 1 invocation<br>NFTs (BAYC,...)<br>ERC-1155 Tokens</td></tr></tbody></table>
