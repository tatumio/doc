---
description: >-
  This function checks if a wallet own's any or a specific nft from a
  collection, you can pass collection address, wallet address & tokenId as an
  option parameter.
---

# Check if the wallet owns a specific NFT

{% embed url="https://codepen.io/tatum-devrel/pen/bGQOjoQ" %}
Try this feature
{% endembed %}

### Overview

In the rapidly growing world of non-fungible tokens (NFTs), verifying the ownership of a particular NFT is crucial for creators, collectors, and traders alike. This guide introduces you to the operation of checking if a wallet owns a specific NFT, providing an efficient way to confirm the possession of unique digital assets. By leveraging this functionality, you can ensure the accuracy and authenticity of your NFT holdings, make well-informed decisions about buying, selling, or holding NFTs, and navigate the dynamic NFT landscape with greater confidence. Ultimately, this operation empowers you to manage your digital assets more effectively, fostering transparency and trust in your NFT transactions.

### How to get the owner of the NFT on the Ethereum network

Use the TatumSDK (`@tatumcom/js`) to check, if the wallet is the owner.

{% tabs %}
{% tab title="TypeScript" %}
<pre class="language-typescript" data-overflow="wrap" data-line-numbers><code class="lang-typescript">// yarn add @tatumio/tatum
import {TatumSDK, Network, Ethereum} from '@tatumio/tatum'

const tatum = await TatumSDK.init&#x3C;Ethereum>({network: Network.ETHEREUM})

const isOwner: boolean = await tatum.nft.checkNftOwner({
  tokenAddress: '0xbc4ca0eda7647a8ab7c2061c2e118a18a936f13d', // replace with your collection
<strong>  tokenId: '1',
</strong>  owner: '0x46efbaedc92067e6d60e84ed6395099723252496' // owner wallet
})

console.log(isOwner)
</code></pre>
{% endtab %}

{% tab title="JavaScript" %}
{% code overflow="wrap" lineNumbers="true" %}
```javascript
// Install with: npm install @tatumio/tatum
const { TatumSDK, Network } = require("@tatumio/tatum");

(async () => {
  try {
    const tatum = await TatumSDK.init({ network: Network.ETHEREUM });
    const isOwner = await tatum.nft.checkNftOwner({
      tokenAddress: "0xbc4ca0eda7647a8ab7c2061c2e118a18a936f13d", // replace with your collection
      tokenId: "1",
      owner: "0x46efbaedc92067e6d60e84ed6395099723252496" // owner wallet
    });
    console.log(isOwner);
  } catch (error) {
    console.error("Error checking NFT owner:", error);
  }
})();


// Expected outcome
// true
```
{% endcode %}
{% endtab %}

{% tab title="curl" %}
{% code overflow="wrap" lineNumbers="true" %}
```bash
curl --location --request GET 'https://api.tatum.io/v4/data/owners/address?tokenAddress=0xbc4ca0eda7647a8ab7c2061c2e118a18a936f13d&tokenId=1&chain=ethereum&address=0x46efbaedc92067e6d60e84ed6395099723252496'
```
{% endcode %}
{% endtab %}
{% endtabs %}

###

<details>

<summary>Expected Response</summary>

```json5
true
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
   * Owner address of the NFT token
   */
  owner: string
}
```
{% endcode %}

### Response interface

{% code overflow="wrap" lineNumbers="true" %}
```typescript
interface ResponseDto<boolean> {
  /**
   * Actual payload of the response - true or false result
   */
  data: boolean
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

