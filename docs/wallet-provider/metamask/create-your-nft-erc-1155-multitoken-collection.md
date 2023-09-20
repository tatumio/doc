# Create your NFT (ERC-1155 MultiToken) Collection

MetaMask is a widely used Ethereum wallet that allows users to manage their Ether and ERC-20 tokens. It also provides an interface for interacting with decentralized applications (dApps) and smart contracts. With the growing popularity of non-fungible tokens (NFTs), you can now leverage MetaMask to create your very own NFT collection contract, opening up a world of opportunities and benefits.

### Why create an NFT collection contract?

NFTs represent unique digital assets that can't be exchanged on a one-to-one basis, differentiating them from other cryptocurrencies. Creating an NFT collection contract allows you to mint, trade, and showcase a series of unique digital items, such as art, collectibles, virtual real estate, or game items. These contracts facilitate the management of your NFT collection, defining rules for minting, transferring, and managing the ownership of your tokens.

{% hint style="info" %}
MetaMask is designed as a browser extension to provide a user-friendly interface and secure key management for interacting with dApps and web services. Connecting from Node.js is not supported because MetaMask focuses on end-user interactions within web browsers, while Node.js is a server-side JavaScript runtime typically used for backend development.
{% endhint %}

### How to create your NFT (ERC-1155 MultiToken) collection with MetaMask from your browser-based application

Use the TatumSDK (`@tatumio/tatum`) to prepare, sign and broadcast the transaction using MetaMask.

{% embed url="https://codepen.io/tatum-devrel/pen/dyQwQOv" %}

{% hint style="info" %}
You will leverage the WalletProvider submodule, which includes multiple browser-based wallet extensions. MetaMask is just one of them.
{% endhint %}

{% tabs %}
{% tab title="TypeScript" %}
<pre class="language-typescript" data-overflow="wrap" data-line-numbers><code class="lang-typescript">// yarn add @tatumio/tatum
import {TatumSDK, Network, Ethereum} from '@tatumio/tatum'

const tatum = await TatumSDK.init&#x3C;Ethereum>({network: Network.ETHEREUM})

// We have prepared a deploy transaction of ERC-1155 contract from your default connected MetaMask account to the recipient
// Result is a transaction IF of a broadcasted transaction
const txId: string = await tatum.walletProvider.metaMask.createErc1155NftCollection()

console.log(txId)

<strong>// Once the transaction is included in a block, you can get the contract address of the newly created collection
</strong>const contractAddress: string | null = await tatum.rpc.getContractAddress(txId)
console.log(contractAddress)
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
    // We have prepared a deploy transaction of ERC-1155 contract from your default connected MetaMask account to the recipient
    // Result is a transaction IF of a broadcasted transaction
    const txId = await tatum.walletProvider.metaMask.createErc1155NftCollection();
    
    console.log(txId);
    
    // Once the transaction is included in a block, you can get the contract address of the newly created collection
    const contractAddress: string | null = await tatum.rpc.getContractAddress(txId)
    console.log(contractAddress)
  } catch (error) {
    console.error("Error signing a transaction using MetaMask:", error);
  }
})();
```
{% endcode %}
{% endtab %}
{% endtabs %}

### Request parameters

{% code overflow="wrap" lineNumbers="true" %}
```typescript
export interface CreateErc1155NftCollection {
  /**
   * base URI of the collection, defaults to empty string. Base URI is prepended to the token ID in the token URI.
   */
  baseURI?: string
  /**
   * (Optional) Address of the admin of the token. Defaults to the connected MetaMask account. Admin can add new minters and pausers.
   */
  author?: string
  /**
   * (Optional) Address of the minter of the token. Defaults to the connected MetaMask account. Minters can mint new tokens.
   */
  minter?: string
}

```
{% endcode %}

### Response

* **txId** - string, transaction hash of signed and broadcasted transaction
  * Example: `"0xdb1e03f4cea29265f031bfc0514b07c15a5fc5e5cc2fd47f7d9a54c74f5c5637"`
