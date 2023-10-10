# Create NFT Collection

An NFT, or non-fungible token, is a type of cryptocurrency that represents a unique item or asset. Unlike regular cryptocurrencies such as Bitcoin or Ether, NFTs aren't interchangeable with other tokens of the same type but stand as unique tokens with their own specific value. They leverage blockchain technology to establish provenance and ownership.

An NFT collection is a group of NFTs, typically bound together by a common theme or brand. Each individual NFT within the collection is unique, but they are all part of the broader collection. Think of it like a collection of paintings from the same artist or a series of collectible toys.

> Note : This function mints a collection for you using your Tatum Plan and transfers the ownership to you.\
> \
> In case you would like to mint it directly from your wallet check the [createNftCollection](../wallet-provider/metamask/create-your-nft-collection.md) function in the Metamask Extension of the Wallet provider submodule.

### How to create NFT Collection (ERC-721 type) on the Ethereum network

Use the TatumSDK (`@tatumio/tatum`) to create the NFT collection.

{% tabs %}
{% tab title="TypeScript" %}
{% code overflow="wrap" lineNumbers="true" %}
```typescript
// yarn add @tatumio/tatum
import {TatumSDK, Network, Ethereum, ResponseDto} from '@tatumio/tatum'

const tatum = await TatumSDK.init<Ethereum>({network: Network.ETHEREUM})

const tx: ResponseDto<{txId: string}> = await tatum.nft.createNftCollection({
  name: 'My NFT Collection',
  symbol: 'MyNFT',
  owner: '0x727ea45b2eb6abb2badd3dc7106d146e0dc0450d', // replace with your address
})

console.log(tx.data.txId)
// 0x8e564406701caab6258501c794f5c1eece380f673be99b561d626c3d8d81b202

// you can get created collection address using this RPC call
const collectionAddress = await tatum.rpc.getContractAddress(tx.data.txId)
console.log(collectionAddress)
// 0x876977006988ce590e219f576077459a49c7318a
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
    const txs = await tatum.nft.createNftCollection({
      name: 'My NFT Collection,
      symbol: 'MyNFT'
      owner: '0x727ea45b2eb6abb2badd3dc7106d146e0dc0450d', // replace with your address
    });
    console.log(txs.data.txId);
    // 0x8e564406701caab6258501c794f5c1eece380f673be99b561d626c3d8d81b202
    
    const collectionAddress = await tatum.rpc.getContractAddress(tx.data.txId);
    console.log(collectionAddress);
    // 0x876977006988ce590e219f576077459a49c7318a
  } catch (error) {
    console.error("Error creating NFT collection:", error);
  }
})();
```
{% endcode %}
{% endtab %}

{% tab title="curl" %}
{% code overflow="wrap" lineNumbers="true" %}
```bash
curl --location --request POST 'https://api.tatum.io/v4/contract/deploy' \
--header 'Content-Type: application/json' \
--data-raw '{
    "contractType": "nft",
    "chain": "ethereum-sepolia",
    "name": "My NFT Collection",
    "symbol": "MyNFT",
    "owner": "0x727ea45b2eb6abb2badd3dc7106d146e0dc0450d"
}'
```
{% endcode %}
{% endtab %}
{% endtabs %}

{% embed url="https://codepen.io/tatum-devrel/pen/zYMyagO" %}

### Use Cases for NFT Collections

1. **Art**: Artists can mint their artworks as NFTs and sell them directly to collectors. Each NFT represents a unique piece of art or a limited edition series.
2. **Collectibles**: Virtual collectibles, such as CryptoPunks or NBA Top Shots, are often grouped into collections. Each unique item in the collection is an NFT.
3. **Virtual Real Estate and Goods**: Platforms like Decentraland allow users to own and trade virtual land and assets as NFTs.
4. **Music and Entertainment**: Musicians can mint their albums or songs as NFTs, providing a new way to monetize their work and connect with fans. Movies or show clips can also be tokenized as collectible NFTs.
5. **Identity and Certification**: NFTs can be used to represent ownership or the achievement of something, such as completing a course or owning a specific domain name.

By creating an NFT collection using the Tatum SDK, you can easily mint, manage, and distribute NFTs on the blockchain. Whether you're an artist launching a new series of artwork, a game developer creating unique in-game items, or a brand creating digital collectibles, the ability to create an NFT collection offers exciting new possibilities for digital ownership and commerce.

### Request interface

{% code overflow="wrap" lineNumbers="true" %}
```typescript
export interface CreateNftCollection {
  /**
   * Name of the NFT collection, e.g. Bored Ape Yacht Club
   */
  name: string
  /**
   * Symbol of the NFT collection, e.g. BAYC
   */
  symbol: string
  /**
   * Address of the NFT collection owner
   */
  owner: string
  /**
   * Address of the NFT collection minter, this is optional and defaults to the owner address
   */
  minter?: string
  /**
   * Optional base URI, which will be prepended to the token URI. If not specified, the token should be minted with the URI
   */
  baseURI?: string
}
```
{% endcode %}

### Response interface

{% code overflow="wrap" lineNumbers="true" %}
```typescript
interface ResponseDto<{txId: string}> {
  /**
   * Actual payload of the response
   */
  data: {txId: string}
  /**
   * Status of the response
   */
  status: Status
  /**
   * In case of ERROR status, this field contains the error message and detailed description
   */
  error?: ErrorWithMessage
}
```
{% endcode %}

### Supported blockchain networks

<table><thead><tr><th width="417">Network</th><th>Support</th></tr></thead><tbody><tr><td>Ethereum / Ethereum Sepolia / Ethereum Goerli<br>BNB Smart Chain / BNB Smart Chain Testnet<br>Celo / Celo Alfajores<br>Polygon / Polygon Mumbai</td><td>NFTs (BAYC,...)<br>ERC-1155 Tokens</td></tr></tbody></table>

### Limitations

