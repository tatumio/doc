---
description: Generate private key from Mnemonic
---

# Generate Private Key

Creating a private key is creating a unique and secret key that belongs to you. This key is crucial for accessing and controlling your funds.

{% tabs %}
{% tab title="Typescript" %}
```typescript
// Import the necessary library and initialize the SDK
import { TezosWalletProvider } from '@tatumio/tezos-wallet-provider';
import { TatumSDK, Network, Tezos } from '@tatumio/tatum';

const tatumSdk = await TatumSDK.init<Tezos>({network: Network.TEZOS,
     configureWalletProviders: [TezosWalletProvider],
});

// Generate Private Key from Mnemonic
const privateKey = await tatumSdk.walletProvider
  .use(TezosWalletProvider)
  .generatePrivateKeyFromMnemonic(mnemonic, 0);

console.log(privateKey);  // This will print the generated private key

tatum.destroy();
```
{% endtab %}

{% tab title="Javascript" %}
```javascript
// Import the necessary library and initialize the SDK
import { TezosWalletProvider } from '@tatumio/tezos-wallet-provider';
import { TatumSDK, Network } from '@tatumio/tatum';

const tatumSdk = await TatumSDK.init({network: Network.TEZOS,
     configureWalletProviders: [TezosWalletProvider],
});

// Generate Private Key from Mnemonic
const privateKey = await tatumSdk.walletProvider
  .use(TezosWalletProvider)
  .generatePrivateKeyFromMnemonic(mnemonic, 0);

console.log(privateKey);  // This will print the generated private key

tatum.destroy();
```
{% endtab %}
{% endtabs %}
