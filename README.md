# 🥳 Tatum Developer Documentation

> We just released the new Tatum SDK which will make your web3 development flow super fun.\
> Looking for our old documentation? [Click Here](https://docs-v3.tatum.io)

## Welcome to Tatum SDK! 🚀

Tatum SDK is here to make your life easier when building blockchain applications! No more complicated setups, no need for previous blockchain experience. We've got you covered.

### Why Tatum SDK? 💡

1. **Super fast development:** Start building blockchain applications in no time.
2. **No previous blockchain experience required:** Perfect for beginners and experts alike.
3. **One line of code:** Perform complex tasks with minimal effort.

### Key Features :tada:

* Monitor activity on a blockchain address 🕵️‍♂️
* Perform RPC calls to various blockchains 📞
* Read information about NFTs such as balances, transactions, or ownerships 🖼️
* Get information about a specific wallet like balances or transaction history 💰

> :key: **Don’t have an API key?** Unlock all networks, features and monitor error logs & usage.\
> [<mark style="color:green;">**Create API key for FREE**</mark>](https://dashboard.tatum.io/)

### Get Started 🌟

To get started with Tatum SDK, simply run the following command based on the language of your choice:

{% tabs %}
{% tab title="TypeScript / JavaScript SDK" %}
{% code overflow="wrap" lineNumbers="true" %}
```bash
npm install @tatumio/tatum
```
{% endcode %}
{% endtab %}
{% endtabs %}

### Examples 📚

Here are some quick examples to show you how easy it is to use Tatum SDK:

#### Perform RPC calls

{% tabs %}
{% tab title="TypeScript" %}
{% code overflow="wrap" lineNumbers="true" %}
```typescript
import { TatumSDK, Ethereum, Network } from '@tatumio/tatum'

(async () => {
    const tatum = await TatumSDK.init<Ethereum>({network: Network.ETHEREUM})
    const latestBlock = await tatum.rpc.blockNumber()
    console.log(`Latest block is ${latestBlock.result}`)
    tatum.destroy();
})()
```
{% endcode %}
{% endtab %}

{% tab title="JavaScript" %}
{% code overflow="wrap" lineNumbers="true" %}
```javascript
const { TatumSDK, Network } = require('@tatumio/tatum');

(async () => {
  const tatum = await TatumSDK.init({ network: Network.ETHEREUM });
  const latestBlock = await tatum.rpc.blockNumber();
  console.log(`Latest block is ${latestBlock.result}`)
  tatum.destroy();
})();
```
{% endcode %}
{% endtab %}
{% endtabs %}

#### Monitor activity on a blockchain address

{% tabs %}
{% tab title="TypeScript" %}
{% code overflow="wrap" lineNumbers="true" %}
```typescript
import { TatumSDK, Ethereum, Network } from '@tatumio/tatum'

(async () => {
    const tatum = await TatumSDK.init<Ethereum>({network: Network.ETHEREUM})
    const monitoredAddress = '0xF64E82131BE01618487Da5142fc9d289cbb60E9d'
    const subscription = await tatum.notification.subscribe.incomingNativeTx({
        address: monitoredAddress,
        url: 'https://<YOUR_WEBHOOK_URL>' // replace with your handler URL
    })
    console.log(`Now you are subscribed for all incoming ETH transactions on ${monitoredAddress}`)
})()
```
{% endcode %}
{% endtab %}

{% tab title="JavaScript" %}
{% code overflow="wrap" lineNumbers="true" %}
```javascript
const { TatumSDK, Ethereum, Network } = require('@tatumio/tatum');

(async () => {
    const tatum = await TatumSDK.init<Ethereum>({network: Network.ETHEREUM});
    const monitoredAddress = '0xF64E82131BE01618487Da5142fc9d289cbb60E9d';
    const subscription = await tatum.notification.subscribe.incomingNativeTx({
        address: monitoredAddress,
        url: 'https://<YOUR_WEBHOOK_URL>' // replace with your handler URL
    });
    console.log(`Now you are subscribed for all incoming ETH transactions on ${monitoredAddress}`);
})();
```
{% endcode %}
{% endtab %}

{% tab title="curl" %}
{% code overflow="wrap" lineNumbers="true" %}
```bash
curl -i -X POST \
  https://api.tatum.io/v4/subscription?type=mainnet \
  -H 'Content-Type: application/json' \
  -d '{
    "type": "INCOMING_NATIVE_TX",
    "attr": {
      "address": "0xF64E82131BE01618487Da5142fc9d289cbb60E9d",
      "chain": "ETH",
      "url": "https://<YOUR_WEBHOOK_URL>"
    }
  }'
```
{% endcode %}
{% endtab %}
{% endtabs %}

Ready to build fantastic blockchain applications? Check out the official documentation for more information and examples!

Happy coding! 🎉

{% hint style="info" %}
### Join our Web3 Developer Community

Get support with our products, meet other developers, and collaborate.\
[Discord](https://discord.gg/tatum) · [Twitter](https://twitter.com/tatum\_io) · [Github](https://github.com/tatumio)
{% endhint %}
