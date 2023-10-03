# Create your Fungible Token

MetaMask, a widely adopted Ethereum wallet, enables users to manage their Ether and ERC-20 tokens while providing a convenient interface for interacting with decentralized applications (dApps) and smart contracts. With the increasing significance of fungible tokens in the digital asset landscape, MetaMask offers a simple and accessible way to create your own ERC-20 token contract, opening the door to numerous possibilities and benefits.

#### Why create an ERC-20 token contract?

Fungible tokens like ERC-20 tokens are digital assets that can be exchanged on a one-to-one basis, making them an ideal choice for various applications, such as:

* Creating a digital currency for your project or platform
* Launching an initial coin offering (ICO) or token sale event
* Developing a reward or loyalty program for your business
* Establishing a decentralized governance system for your community

{% hint style="info" %}
MetaMask is designed as a browser extension to provide a user-friendly interface and secure key management for interacting with dApps and web services. Connecting from Node.js is not supported because MetaMask focuses on end-user interactions within web browsers, while Node.js is a server-side JavaScript runtime typically used for backend development.
{% endhint %}

### How to create your Fungible token with MetaMask from your browser-based application

Use the TatumSDK (`@tatumio/tatum`) to prepare, sign and broadcast the transaction using MetaMask.

{% embed url="https://codepen.io/tatum-devrel/pen/rNQoQWN" %}

{% hint style="info" %}
You will leverage the WalletProvider submodule, which includes multiple browser-based wallet extensions. MetaMask is just one of them.
{% endhint %}

{% tabs %}
{% tab title="TypeScript" %}
<pre class="language-typescript" data-overflow="wrap" data-line-numbers><code class="lang-typescript">// yarn add @tatumio/tatum
import {TatumSDK, Network, Ethereum} from '@tatumio/tatum'

const tatum = await TatumSDK.init&#x3C;Ethereum>({network: Network.ETHEREUM})

// We have prepared a deploy transaction of ERC-20 contract from your default connected MetaMask account to the recipient
// Result is a transaction IF of a broadcasted transaction
const txId: string = await tatum.walletProvider.use(MetaMask).createFungibleToken({
    name: 'Your Token Name',
    symbol: 'Your Token Symbol',
    decimals: 18,
    initialSupply: 1_000_000})

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
    // We have prepared a deploy transaction of ERC-20 contract from your default connected MetaMask account to the recipient
    // Result is a transaction IF of a broadcasted transaction
    const txId = await tatum.walletProvider.use(MetaMask).createFungibleToken({
    name: 'Your Token Name',
    symbol: 'Your Token Symbol',
    decimals: 18,
    initialSupply: 1_000_000})
    
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

### Request object parameters

{% code overflow="wrap" lineNumbers="true" %}
```typescript
export interface CreateFungibleToken {
  /**
   * Name of the token.
   */
  name: string
  /**
   * Symbol of the token.
   */
  symbol: string
  /**
   * Number of decimals of the token. Defaults to 18.
   */
  decimals?: number
  /**
   * Total supply of the token.
   */
  initialSupply: string
  /**
   * (Optional) Address of the initial holder of the token. Defaults to the connected MetaMask account.
   */
  initialHolder?: string
  /**
   * (Optional) Address of the admin of the token. Defaults to the connected MetaMask account. Admin can add new minters and pausers.
   */
  admin?: string
  /**
   * (Optional) Address of the minter of the token. Defaults to the connected MetaMask account. Minters can mint new tokens.
   */
  minter?: string
  /**
   * (Optional) Address of the pauser of the token. Defaults to the connected MetaMask account. Pausers can pause and unpause the token transactions.
   */
  pauser?: string
}

```
{% endcode %}

### Response

* **txId** - string, transaction hash of signed and broadcasted transaction
  * Example: `"0xdb1e03f4cea29265f031bfc0514b07c15a5fc5e5cc2fd47f7d9a54c74f5c5637"`
