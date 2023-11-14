# Generate Address

Generating an address is about creating a public address where others can send you funds. It's like an account number in the blockchain world.

You can generate an address with both Mnemonic or Xpub

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

// Generate address from mnemonic or xpub
const addressFromMnemonic = await tatumSdk.walletProvider
.use(EvmWalletProvider).generateAddressFromMnemonic(mnemonic, 0);
const addressFromXpub = await tatumSdk.walletProvider
.use(EvmWalletProvider).generateAddressFromXpub(xpubDetails.xpub, 0);

// This will print the generated address from mnemonic
console.log(addressFromMnemonic);
// This will print the generated address from xpub
console.log(addressFromXpub);

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
    const addressFromMnemonic = await tatumSdk.walletProvider
    .use(EvmWalletProvider).generateAddressFromMnemonic(mnemonic, 0);
    const addressFromXpub = await tatumSdk.walletProvider
    .use(EvmWalletProvider).generateAddressFromXpub(xpubDetails.xpub, 0);
    console.log(addressFromMnemonic);
    console.log(addressFromXpub);
  } catch (error) {
    console.error("Error generating address:", error);
  }
})();

await tatum.destroy()
```
{% endtab %}
{% endtabs %}
