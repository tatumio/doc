# Sign and Broadcast a Transaction

Signing and broadcasting a transaction is about authorising a transfer of funds or interaction with a smart contract and then sending that authorisation to the blockchain to be processed.

{% tabs %}
{% tab title="Typescript" %}
```typescript
// Import the necessary library and initialize the SDK
import { EvmWalletProvider } from '@tatumio/evm-wallet-provider';
import { TatumSDK, Network, Ethereum } from '@tatumio/tatum';

const tatumSdk = await TatumSDK.init<Ethereum>({network: Network.ETHEREUM,
     configureWalletProviders: [
         EvmWalletProvider,
     ]});

// Define your transaction details
const payload = {
  privateKey: 'YOUR_PRIVATE_KEY',
  // other fields for your transaction...
}

// Sign and broadcast the transaction using the EVM Wallet Provider submodule
const txHash = await tatumSdk.walletProvider.use(EvmWalletProvider)
.signAndBroadcast(payload);

// This will print the transaction hash of the broadcasted transaction
console.log(txHash);

await tatum.destroy()
```
{% endtab %}

{% tab title="Javascript" %}
```javascript
 // Install with: npm install @tatumio/evm-wallet-provider @tatumio/tatum
const { EvmWalletProvider } = require("@tatumio/evm-wallet-provider");
const { TatumSDK, Network, Ethereum } = require("@tatumio/tatum");

(async () => {
  try {
    const tatumSdk = await TatumSDK.init({ network: Network.ETHEREUM,
     configureWalletProviders: [
         EvmWalletProvider,
     ]});
    const payload = {
      privateKey: 'YOUR_PRIVATE_KEY',
      // other fields for your transaction...
    }
    const txHash = await tatumSdk.walletProvider.use(EvmWalletProvider)
    .signAndBroadcast(payload);
    console.log(txHash);
  } catch (error) {
    console.error("Error signing and broadcasting transaction:", error);
  }
})();

await tatum.destroy()
```
{% endtab %}
{% endtabs %}
