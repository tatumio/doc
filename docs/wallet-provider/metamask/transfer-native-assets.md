# Transfer native assets

Preparing a transaction for signing via MetaMask means creating a transaction object containing essential details, such as the sender's address, recipient's address, amount to be sent, and gas fees. This transaction object is then presented to MetaMask, which securely signs the transaction using the user's private key, ensuring the transaction's authenticity and integrity before it's broadcasted to the Ethereum network.

{% hint style="info" %}
MetaMask is designed as a browser extension to provide a user-friendly interface and secure key management for interacting with dApps and web services. Connecting from Node.js is not supported because MetaMask focuses on end-user interactions within web browsers, while Node.js is a server-side JavaScript runtime typically used for backend development.
{% endhint %}

{% embed url="https://codepen.io/tatum-devrel/pen/bGQOQej" %}

### How to perform a transaction with MetaMask from your browser-based application

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

const txId: string = await tatum.walletProvider.use(MetaMask).transferNative('0x4675C7e5BaAFBFFbca748158bEcBA61ef3b0a263', '1.5')

console.log(txId)

// We have prepared a native transfer of 1.5 ETH from your default connected MetaMask account to the recipient of 0x4675C7e5BaAFBFFbca748158bEcBA61ef3b0a263
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
    const txId = await tatum.walletProvider.use(MetaMask).transferNative('0x4675C7e5BaAFBFFbca748158bEcBA61ef3b0a263', '1.5');
    console.log(txId);
  } catch (error) {
    console.error("Error signing a transaction using MetaMask:", error);
  }
})();

// We have prepared a native transfer of 1.5 ETH from your default connected MetaMask account to the recipient of 0x4675C7e5BaAFBFFbca748158bEcBA61ef3b0a263
// Result is a transaction IF of a broadcasted transaction
```
{% endcode %}
{% endtab %}
{% endtabs %}

### Request parameters

* **`recipient`** - string, recipient of your transaction
  * Example: `"0x4675C7e5BaAFBFFbca748158bEcBA61ef3b0a263"`
* **`amount`** - string, amount to be sent, always in native currency like ETH for Ethereum or MATIC for Polygon
  * Example: `"1.5"`

### Response

* **txId** - string, transaction hash of signed and broadcasted transaction
  * Example: `"0xdb1e03f4cea29265f031bfc0514b07c15a5fc5e5cc2fd47f7d9a54c74f5c5637"`
