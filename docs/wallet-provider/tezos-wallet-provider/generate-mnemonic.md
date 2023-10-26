# Generate Mnemonic

Generating a mnemonic means creating a special phrase that will be the foundation for your wallet. This phrase is like a master key from which all your wallet addresses and their private keys can be generated. It's a crucial step for ensuring the security and recoverability of your wallet.

The Tezos Wallet Provider submodule helps in generating a mnemonic easily. This mnemonic phrase, also known as a seed phrase, is vital for creating and recovering wallets on Tezos.

{% tabs %}
{% tab title="Typescript" %}
```typescript
// Import the necessary library and initialize the SDK
import { TezosWalletProvider } from '@tatumio/tezos-wallet-provider';
import { TatumSDK, Network, Tezos } from '@tatumio/tatum';

const tatumSdk = await TatumSDK.init<Tezos>({network: Network.TEZOS,
     configureWalletProviders: [TezosWalletProvider]
});

// Generate mnemonic using the Tezos Wallet Provider submodule
const mnemonic = tatumSdk.walletProvider.use(TezosWalletProvider).generateMnemonic();

console.log(mnemonic);  // This will print the generated mnemonic

tatum.destroy();
```
{% endtab %}

{% tab title="Javascript" %}
```javascript
// Import the necessary library and initialize the SDK
import { TezosWalletProvider } from '@tatumio/tezos-wallet-provider';
import { TatumSDK, Network } from '@tatumio/tatum';

const tatumSdk = await TatumSDK.init({
  network: Network.TEZOS,
  configureWalletProviders: [TezosWalletProvider],
});

// Generate mnemonic using the Tezos Wallet Provider submodule
const mnemonic = tatumSdk.walletProvider.use(TezosWalletProvider).generateMnemonic();

console.log(mnemonic);  // This will print the generated mnemonic

tatum.destroy();
```
{% endtab %}
{% endtabs %}
