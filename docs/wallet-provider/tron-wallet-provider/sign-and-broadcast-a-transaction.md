# Sign and Broadcast a Transaction

Signing and broadcasting a transaction is about authorising a transfer of funds or interaction with a smart contract and then sending that authorisation to the blockchain to be processed.

{% tabs %}
{% tab title="Typescript" %}
```typescript
// Import the necessary library and initialize the SDK
import { TronWalletProvider } from '@tatumio/tron-wallet-provider';
import { TatumSDK, Network, Tron } from '@tatumio/tatum';

const tatumSdk = await TatumSDK.init<Tron>({network: Network.TRON,
     configureWalletProviders: [
         TronWalletProvider,
     ]});

// Define your transaction details
const payloadTron = {
  privateKey: 'YOUR_PRIVATE_KEY',
  to: 'TARGET_WALLET_ADDRESS',
  amount: '0.01'  // TRX_AMOUNT
}

// Sign and broadcast the transaction using the Tron Wallet Provider submodule
const txHash = await tatumSdk.walletProvider.use(TronWalletProvider)
.signAndBroadcast(payloadTron);

// This will print the transaction hash of the broadcasted transaction
console.log(txHash);

tatum.destroy();
```
{% endtab %}

{% tab title="Javascript" %}
```javascript
// Import the necessary library and initialize the SDK
import { TronWalletProvider } from '@tatumio/tron-wallet-provider';
import { TatumSDK, Network, Tron } from '@tatumio/tatum';

const tatumSdk = await TatumSDK.init<Tron>({network: Network.TRON,
     configureWalletProviders: [
         TronWalletProvider,
     ]});

// Define your transaction details
const payloadTron = {
  privateKey: 'YOUR_PRIVATE_KEY',
  to: 'TARGET_WALLET_ADDRESS',
  amount: '0.01'  // TRX_AMOUNT
}

// Sign and broadcast the transaction using the Tron Wallet Provider submodule
const txHash = await tatumSdk.walletProvider.use(TronWalletProvider)
.signAndBroadcast(payloadTron);

// This will print the transaction hash of the broadcasted transaction
console.log(txHash);

tatum.destroy();

```
{% endtab %}
{% endtabs %}
