# Retrieve the owner of the NFT

In the rapidly evolving world of non-fungible tokens (NFTs), it is essential for creators, collectors, and traders to have the ability to verify the ownership of individual NFTs. This guide introduces you to the operation of retrieving the owner of a specific NFT, providing you with the necessary information to confirm the current holder of the unique digital asset. By leveraging this functionality, you can ensure the authenticity and provenance of the NFT, make informed decisions about buying, selling, or holding it, and navigate the dynamic NFT market with confidence. Ultimately, this operation enables you to manage your digital assets more effectively and maintain the integrity of your NFT transactions.

### How to get the owner of the NFT on the Ethereum network

Use the TatumSDK (`@tatumio/tatum`) to get an owner of the NFT.

{% tabs %}
{% tab title="TypeScript" %}
{% code overflow="wrap" lineNumbers="true" %}
```typescript
// yarn add @tatumio/tatum
import {TatumSDK, Network, Ethereum, ResponseDto, NftTransaction} from '@tatumio/tatum'

const tatum = await TatumSDK.init<Ethereum>({network: Network.ETHEREUM})

const owner: ResponseDto<string[]> = await tatum.nft.getNftOwner({
  tokenAddress: '0xbc4ca0eda7647a8ab7c2061c2e118a18a936f13d', // replace with your collection
  tokenId: '1'
})

console.log(owner.data)
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
    const txs = await tatum.nft.getNftOwner({
      tokenAddress: "0xbc4ca0eda7647a8ab7c2061c2e118a18a936f13d", // replace with your collection
      tokenId: "1"
    });
    console.log(txs.data);
  } catch (error) {
    console.error("Error fetching NFT owner:", error);
  }
})();
```
{% endcode %}
{% endtab %}

{% tab title="curl" %}
{% code overflow="wrap" lineNumbers="true" %}
```bash
curl --location --request GET 'https://api.tatum.io/v4/data/owners?tokenAddress=0xbc4ca0eda7647a8ab7c2061c2e118a18a936f13d&tokenId=1&chain=ethereum'
```
{% endcode %}
{% endtab %}
{% endtabs %}

{% embed url="https://codepen.io/tatum-devrel/pen/rNQorxB" %}

<details>

<summary>Expected Response</summary>

```json5
[
 "0x46efbaedc92067e6d60e84ed6395099723252496"
]
```

</details>

### Request interface

{% code overflow="wrap" lineNumbers="true" %}
```typescript
interface GetTokenOwner {
  /**
   * Token ID
   */
  tokenId: string
  /**
   * Token contract address
   */
  tokenAddress: string
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
interface ResponseDto<string[]> {
  /**
   * Actual payload of the response - list of the owner address
   */
  data: string[]
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

<table><thead><tr><th width="417">Network</th><th>Support</th></tr></thead><tbody><tr><td>Ethereum / Ethereum Sepolia<br>BNB Smart Chain / BNB Smart Chain Testnet<br>Celo / Celo Alfajores<br>Polygon / Polygon Mumbai</td><td>NFTs (BAYC,...)<br>ERC-1155 Tokens</td></tr></tbody></table>

