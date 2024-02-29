# Get the metadata of a specific NFT

As non-fungible tokens (NFTs) gain popularity in the digital asset space, it becomes increasingly important for creators, collectors, and traders to have access to detailed information about individual NFTs. This guide introduces you to the operation of retrieving the metadata of a specific NFT, providing valuable insights into the unique properties, characteristics, and history of the digital asset. By leveraging this functionality, you can better understand the provenance, rarity, and artistic attributes of the NFT, make well-informed decisions about buying, selling, or holding it, and navigate the dynamic NFT market with greater confidence. Ultimately, this operation allows you to manage your digital assets more effectively and fosters a deeper appreciation for the unique qualities of each NFT.

### How to get the metada of the NFT on the Ethereum network

Use the TatumSDK (`@tatumio/tatum`) to get the metadata of the specific NFT.

{% tabs %}
{% tab title="TypeScript" %}
{% code overflow="wrap" lineNumbers="true" %}
```typescript
// yarn add @tatumio/tatum
import {TatumSDK, Network, Ethereum, ResponseDto, NftTokenDetail} from '@tatumio/tatum'

const tatum = await TatumSDK.init<Ethereum>({network: Network.ETHEREUM})

const metadata: ResponseDto<NftTokenDetail|null> = await tatum.nft.getNftMetadata({
  tokenAddress: '0xbc4ca0eda7647a8ab7c2061c2e118a18a936f13d', // replace with your collection
  tokenId: '1'
})

console.log(metadata.data)
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
    const metadata = await tatum.nft.getNftMetadata({
      tokenAddress: "0xbc4ca0eda7647a8ab7c2061c2e118a18a936f13d", // replace with your collection
      tokenId: "1"
    });
    console.log(metadata.data);
  } catch (error) {
    console.error("Error getting NFT metadata:", error);
  }
})();
```
{% endcode %}
{% endtab %}

{% tab title="curl" %}
{% code overflow="wrap" lineNumbers="true" %}
```bash
curl --location --request GET 'https://api.tatum.io/v4/data/metadata?chain=ethereum&tokenAddress=0xbc4ca0eda7647a8ab7c2061c2e118a18a936f13d&tokenIds=1'
```
{% endcode %}
{% endtab %}
{% endtabs %}

{% embed url="https://codepen.io/tatum-devrel/pen/XWyoBYd" %}

### Request interface

{% code overflow="wrap" lineNumbers="true" %}
```typescript
interface GetNftMetadata {
  /**
   * Token ID
   */
  tokenId: string
  /**
   * Token contract address
   */
  tokenAddress: string
}
```
{% endcode %}

### Response interface

{% code overflow="wrap" lineNumbers="true" %}
```typescript
interface NftTokenDetail {
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
}
```
{% endcode %}

### Supported blockchain networks

<table><thead><tr><th width="417">Network</th><th>Support</th></tr></thead><tbody><tr><td>Ethereum / Ethereum Sepolia<br>BNB Smart Chain / BNB Smart Chain Testnet<br>Celo / Celo Alfajores<br>Polygon / Polygon Mumbai</td><td>NFTs (BAYC,...)<br>ERC-1155 Tokens</td></tr></tbody></table>
