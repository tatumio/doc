# Build your own custom transaction

Preparing a transaction for signing via MetaMask means creating a transaction object containing essential details, such as the sender's address, recipient's address, amount to be sent, and gas fees. This transaction object is then presented to MetaMask, which securely signs the transaction using the user's private key, ensuring the transaction's authenticity and integrity before it's broadcasted to the Ethereum network.

{% hint style="info" %}
MetaMask is designed as a browser extension to provide a user-friendly interface and secure key management for interacting with dApps and web services. Connecting from Node.js is not supported because MetaMask focuses on end-user interactions within web browsers, while Node.js is a server-side JavaScript runtime typically used for backend development.
{% endhint %}

In summary, you can prepare any transaction, like deploying a new smart contract or interacting with any existing one.

### How to prepare a custom transaction with MetaMask from your browser-based application

Use the TatumSDK (`@tatumio/tatum`) to prepare, sign and broadcast the transaction using MetaMask.

{% hint style="info" %}
You will leverage the WalletProvider submodule, which includes multiple browser-based wallet extensions. MetaMask is just one of them.
{% endhint %}

{% tabs %}
{% tab title="TypeScript" %}
{% code overflow="wrap" lineNumbers="true" %}
```typescript
// yarn add @tatumio/tatum
import {TatumSDK, Network, Ethereum} from '@tatumio/tatum'

const tatum = await TatumSDK.init<Ethereum>({network: Network.ETHEREUM})

// Prepare your payload for a signing
const payload = {
  to: '0x4675C7e5BaAFBFFbca748158bEcBA61ef3b0a263',
  amount: '0x012F',
  data: '0x000......' // your custom data
}

const txId: string = await tatum.walletProvider.metaMask.customPayload(payload)

console.log(txId)

// We have prepared a custom transaction from your default connected MetaMask account
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
    // Prepare your payload for a signing
    const payload = {
      to: '0x4675C7e5BaAFBFFbca748158bEcBA61ef3b0a263',
      amount: '0x012F',
      data: '0x000......' // your custom data
    };
    
    const txId = await tatum.walletProvider.metaMask.customPayload(payload);
    console.log(txId);
  } catch (error) {
    console.error("Error signing a transaction using MetaMask:", error);
  }
})();


// We have prepared a custom transaction from your default connected MetaMask account
```
{% endcode %}
{% endtab %}
{% endtabs %}

### Request interface

{% code overflow="wrap" lineNumbers="true" %}
```typescript
interface TxPayload {
  //  - The string of the address to the transaction is directed to
  to?: string

  //  - (optional) The string of the address the transaction is sent from
  from?: string

  //  - (optional) The integer of the gas provided for the transaction execution
  gas?: string

  //  - (optional) The integer of the gasPrice used for each paid gas encoded as hexadecimal
  gasPrice?: string

  //  - (optional) The integer of the value sent with this transaction encoded as hexadecimal
  value?: string

  // The string of the hash of the method signature and encoded parameters, see the Ethereum Contract ABI
  data?: string
}
```
{% endcode %}

### Response

* **txId** - string, transaction hash of signed and broadcasted transaction
  * Example: `"0xdb1e03f4cea29265f031bfc0514b07c15a5fc5e5cc2fd47f7d9a54c74f5c5637"`
