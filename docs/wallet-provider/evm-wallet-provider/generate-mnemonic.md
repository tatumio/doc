# Generate Mnemonic

Generating a mnemonic means creating a special phrase that will be the foundation for your wallet. This phrase is like a master key from which all your wallet addresses and their private keys can be generated. It's a crucial step for ensuring the security and recoverability of your wallet.

The EVM Wallet Provider submodule helps in generating a mnemonic easily. This mnemonic phrase, also known as a seed phrase, is vital for creating and recovering wallets on EVM chains.

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

// Generate mnemonic using the EVM Wallet Provider submodule
const mnemonic = tatumSdk.walletProvider.use(EvmWalletProvider).generateMnemonic();

console.log(mnemonic);  // This will print the generated mnemonic

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
     ]
    });
    const mnemonic = await tatumSdk.walletProvider.use(EvmWalletProvider).generateMnemonic();
    console.log(mnemonic);
  } catch (error) {
    console.error("Error generating mnemonic:", error);
  }
})();

```
{% endtab %}
{% endtabs %}
