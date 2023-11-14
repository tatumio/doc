# Generate Mnemonic

Generating a mnemonic means creating a special phrase that will be the foundation for your wallet. This phrase is like a master key from which all your wallet addresses and their private keys can be generated. It's a crucial step for ensuring the security and recoverability of your wallet.

The UTXO Wallet Provider submodule helps in generating a mnemonic easily. This mnemonic phrase, also known as a seed phrase, is vital for creating and recovering wallets on UTXO chains.

{% tabs %}
{% tab title="Typescript" %}
```typescript
// Import the necessary library and initialize the SDK
import { UtxoWalletProvider } from '@tatumio/utxo-wallet-provider';
import { TatumSDK, Network, Bitcoin } from '@tatumio/tatum';

const tatumSdk = await TatumSDK.init<Bitcoin>({network: Network.BITCOIN,
     configureWalletProviders: [
         UtxoWalletProvider,
     ]});

// Generate mnemonic using the UTXO Wallet Provider submodule
const mnemonic = tatumSdk.walletProvider.use(UtxoWalletProvider).generateMnemonic();

console.log(mnemonic);  // This will print the generated mnemonic

await tatum.destroy();
```
{% endtab %}

{% tab title="Javascript" %}
```javascript
// Import the necessary library and initialize the SDK
import { UtxoWalletProvider } from '@tatumio/utxo-wallet-provider';
import { TatumSDK, Network } from '@tatumio/tatum';

const tatumSdk = await TatumSDK.init({network: Network.BITCOIN,
     configureWalletProviders: [
         UtxoWalletProvider,
     ]});

// Generate mnemonic using the UTXO Wallet Provider submodule
const mnemonic = tatumSdk.walletProvider.use(UtxoWalletProvider).generateMnemonic();

console.log(mnemonic);  // This will print the generated mnemonic

await tatum.destroy();
```
{% endtab %}
{% endtabs %}
