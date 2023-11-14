# Generate Address

Generating an address is about creating a public address where others can send you funds. It's like an account number in the blockchain world.

You can generate an address with private key.

{% tabs %}
{% tab title="Typescript" %}
```typescript
// Import the necessary library and initialize the SDK
import { TezosWalletProvider } from '@tatumio/tezos-wallet-provider';
import { TatumSDK, Network, Tezos } from '@tatumio/tatum';

const tatumSdk = await TatumSDK.init<Tezos>({network: Network.TEZOS,
     configureWalletProviders: [TezosWalletProvider],
});

// Generate Address from Private Key
const address = await tatumSdk.walletProvider
  .use(TezosWalletProvider)
  .generateAddressFromPrivateKey(privateKey);

console.log(address);  // This will print the generated address


await tatum.destroy()

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

// Generate Address from Private Key
const address = await tatumSdk.walletProvider
  .use(TezosWalletProvider)
  .generateAddressFromPrivateKey(privateKey);

console.log(address);  // This will print the generated address

await tatum.destroy();

```
{% endtab %}
{% endtabs %}
