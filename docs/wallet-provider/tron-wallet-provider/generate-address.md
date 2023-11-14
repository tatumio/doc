---
description: Generate Address from Mnemonic or an Xpub
---

# Generate Address

These functions allow you to derive a wallet address from a mnemonic or an xpub using the `TronWalletProvider` from the Tatum SDK.

{% tabs %}
{% tab title="Typescript" %}
<pre class="language-typescript"><code class="lang-typescript"><strong>// Import the necessary library and initialize the SDK
</strong>import { TronWalletProvider } from '@tatumio/tron-wallet-provider';
import { TatumSDK, Network } from '@tatumio/tatum';

// Initialize the SDK for Tron
const tatumSdk = await TatumSDK.init&#x3C;Tron>({
  network: Network.TRON,
  configureWalletProviders: [TronWalletProvider]
});

// Derive address from mnemonic
const addressFromMnemonic = await tatumSdk.walletProvider
  .use(TronWalletProvider)
  .generateAddressFromMnemonic(mnemonic, 0);

// Derive address from xpub
const addressFromXpub = await tatumSdk.walletProvider
  .use(TronWalletProvider)
  .generateAddressFromXpub(xpubDetails.xpub, 0);

// Output the derived addresses
console.log(addressFromMnemonic);  // Prints the address derived from mnemonic
console.log(addressFromXpub);  // Prints the address derived from xpub

await tatum.destroy();
</code></pre>
{% endtab %}

{% tab title="Javascript" %}
<pre class="language-javascript"><code class="lang-javascript"><strong>// Import the necessary library and initialize the SDK
</strong>import { TronWalletProvider } from '@tatumio/tron-wallet-provider';
import { TatumSDK, Network } from '@tatumio/tatum';

// Initialize the SDK for Tron
const tatumSdk = await TatumSDK.init({
  network: Network.TRON,
  configureWalletProviders: [TronWalletProvider]
});

// Derive address from mnemonic
const addressFromMnemonic = await tatumSdk.walletProvider
  .use(TronWalletProvider)
  .generateAddressFromMnemonic(mnemonic, 0);

// Derive address from xpub
const addressFromXpub = await tatumSdk.walletProvider
  .use(TronWalletProvider)
  .generateAddressFromXpub(xpubDetails.xpub, 0);

// Output the derived addresses
console.log(addressFromMnemonic);  // Prints the address derived from mnemonic
console.log(addressFromXpub);  // Prints the address derived from xpub

await tatum.destroy();
</code></pre>
{% endtab %}
{% endtabs %}
