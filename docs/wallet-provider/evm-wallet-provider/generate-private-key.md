# Generate Private Key

Creating a private key is creating a unique and secret key that belongs to you. This key is crucial for accessing and controlling your funds.

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

// Generate private key from mnemonic
const privateKey = await tatumSdk.walletProvider.use(EvmWalletProvider)
.generatePrivateKeyFromMnemonic(mnemonic, 0);

console.log(privateKey);  // This will print the generated private key

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
    const privateKey = await tatumSdk.walletProvider.use(EvmWalletProvider)
    .generatePrivateKeyFromMnemonic(mnemonic, 0);
    console.log(privateKey);
  } catch (error) {
    console.error("Error generating private key:", error);
  }
})();


await tatum.destroy()
```
{% endtab %}
{% endtabs %}
