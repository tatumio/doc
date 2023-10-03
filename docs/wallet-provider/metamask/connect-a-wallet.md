# Connect a wallet

Connecting to a MetaMask wallet means establishing a link between a decentralized application (dApp) or a web-based service and your MetaMask wallet. MetaMask is a browser extension that acts as a cryptocurrency wallet and a gateway to blockchain-based applications on the Ethereum network.

When you connect to a MetaMask wallet, you're granting the dApp or web service permission to access your wallet's Ethereum address and interact with the Ethereum blockchain on your behalf. This may include actions such as signing transactions, sending tokens, or participating in decentralised finance (DeFi) protocols. This connection enables seamless interaction between users and blockchain applications while keeping private keys secure within the wallet.

{% embed url="https://codepen.io/tatum-devrel/pen/xxQmQOZ" %}

{% hint style="info" %}
MetaMask is designed as a browser extension to provide a user-friendly interface and secure key management for interacting with dApps and web services. Connecting from Node.js is not supported because MetaMask focuses on end-user interactions within web browsers, while Node.js is a server-side JavaScript runtime typically used for backend development.
{% endhint %}

### How to get connect to MetaMask from your browser-based application

Use the TatumSDK (`@tatumio/tatum`) to check if there is a MetaMask extension available and get the default address from it.

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

const metamaskAccount: string = await tatum.walletProvider.use(MetaMask).getWallet();

console.log(metamaskAccount)
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
    const metamaskAccount = await tatum.walletProvider.use(MetaMask).getWallet();
    console.log(metamaskAccount);
  } catch (error) {
    console.error("Error fetching default account from MetaMask:", error);
  }
})();
```
{% endcode %}
{% endtab %}
{% endtabs %}

<details>

<summary>Expected Response</summary>

```json5
0xF64E82131BE01618487Da5142fc9d289cbb60E9d
```

</details>
