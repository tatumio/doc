# Approve the transfer of a fungible token like USDT

In the context of ERC20 tokens, "approve" refers to a function in the ERC20 standard that allows a token holder to grant permission to another address (called the "spender") to transfer a specified amount of tokens on their behalf. This mechanism is useful for enabling smart contracts or other addresses to perform token transactions on behalf of the token owner without the need to transfer the tokens directly.

{% hint style="info" %}
MetaMask is designed as a browser extension to provide a user-friendly interface and secure key management for interacting with dApps and web services. Connecting from Node.js is not supported because MetaMask focuses on end-user interactions within web browsers, while Node.js is a server-side JavaScript runtime typically used for backend development.
{% endhint %}

In summary, approving the transfer of an ERC20 token is a way to delegate the ability to spend tokens to another address while maintaining control over the tokens and their allowance.

### How to approve a USDT transaction for someone else with MetaMask from your browser-based application

Use the TatumSDK (`@tatumio/tatum`) to prepare, sign and broadcast the transaction using MetaMask.

{% hint style="info" %}
You will leverage the WalletProvider submodule, which includes multiple browser-based wallet extensions. MetaMask is just one of them.
{% endhint %}

{% tabs %}
{% tab title="TypeScript" %}
{% code overflow="wrap" lineNumbers="true" %}
```typescript
// yarn add @tatumio/tatum
import {TatumSDK, Network, Ethereum, MetaMask} from '@tatumio/tatum'

const tatum = await TatumSDK.init<Ethereum>({network: Network.ETHEREUM})

//This is the USDT token address
const USDT = '0xdAC17F958D2ee523a2206206994597C13D831ec7'

const txId: string = await tatum.walletProvider.use(MetaMask).approveErc20('0x4675C7e5BaAFBFFbca748158bEcBA61ef3b0a263', '1.5', USDT)

console.log(txId)

// We have prepared an approval operation of 1.5 USDT from your default connected MetaMask account to the spender - 0x4675C7e5BaAFBFFbca748158bEcBA61ef3b0a263
```
{% endcode %}
{% endtab %}

{% tab title="JavaScript" %}
{% code overflow="wrap" lineNumbers="true" %}
```javascript
// Install with: npm install @tatumio/tatum
const { TatumSDK, Network, MetaMask } = require("@tatumio/tatum");

(async () => {
  try {
    const tatum = await TatumSDK.init({ network: Network.ETHEREUM });
    //This is the USDT token address
    const USDT = '0xdAC17F958D2ee523a2206206994597C13D831ec7'
    
    const txId = await tatum.walletProvider.use(MetaMask).approveErc20('0x4675C7e5BaAFBFFbca748158bEcBA61ef3b0a263', '1.5', USDT);
    console.log(txId);
  } catch (error) {
    console.error("Error signing a transaction using MetaMask:", error);
  }
})();

// We have prepared an approval operation of 1.5 USDT from your default connected MetaMask account to the spender - 0x4675C7e5BaAFBFFbca748158bEcBA61ef3b0a263
```
{% endcode %}
{% endtab %}
{% endtabs %}

### Request parameters

* **`spender`** - string, address, which will be able to transfer the tokens on behalf of the owner
  * Example: `"0x4675C7e5BaAFBFFbca748158bEcBA61ef3b0a263"`
* **`amount`** - string, amount to be approved, always in a token currency like USDT
  * Example: `"1.5"`
* **`tokenAddress`** - string, token address of a token you want to approve
  * Example: `"0xdAC17F958D2ee523a2206206994597C13D831ec7"`

### Response

* **txId** - string, transaction hash of signed and broadcasted transaction
  * Example: `"0xdb1e03f4cea29265f031bfc0514b07c15a5fc5e5cc2fd47f7d9a54c74f5c5637"`
