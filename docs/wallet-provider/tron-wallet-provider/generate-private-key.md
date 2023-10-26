---
description: Generate private key from Mnemonic
---

# Generate Private Key

Creating a private key is creating a unique and secret key that belongs to you. This key is crucial for accessing and controlling your funds.

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

// Generate private key from mnemonic
const privateKey = await tatumSdk.walletProvider.use(TronWalletProvider)
.generatePrivateKeyFromMnemonic(mnemonic, 0);

console.log(privateKey);  // This will print the generated private key

tatum.destroy()

```
{% endtab %}

{% tab title="Javascript" %}
```javascript
// Import the necessary library and initialize the SDK
import { TronWalletProvider } from '@tatumio/tron-wallet-provider';
import { TatumSDK, Network, Tron } from '@tatumio/tatum';

// Initialize the SDK for Tron
const tatumSdk = await TatumSDK.init({
  network: Network.TRON,
  configureWalletProviders: [TronWalletProvider]
});

// Generate private key from mnemonic
const privateKey = await tatumSdk.walletProvider
  .use(TronWalletProvider)
  .generatePrivateKeyFromMnemonic(mnemonic, 0);

console.log(privateKey);  // This will print the generated private key

tatum.destroy()

```
{% endtab %}
{% endtabs %}
