---
description: Here's all that has been updated or shipped recently.
---

# 🎁 What's New

{% hint style="info" %}
[**Join our Discord**](https://discord.com/invite/tatum) to stay up to date with the latest updates from product news to upcoming events. You'll also be able to submit feedback and help shape future updates. Learn more about our community [here](https://tatum.io/community).&#x20;
{% endhint %}

### March 15 2024 - Fee Estimation Improvements

We have adjusted our Fee Estimations to be more reactive towards the congestion scenario's - what that means is that is that without affecting the regular transaction volume scenario, in case of transaction congestions, our Fee Estimations will have a higher likelihood of getting your transaction through.

### March 01 2024 - Sunset of Goerli Network

As Goerli (Testnet Ethereum Network) has reached its end of life support, we have have removed teh support for Goerli from all our Core Products Like RPC, Data Solution & more, from both API's & SDK.&#x20;



### Jan 15 2024 - Dashboard - Enhanced Notifications

We've revamped the Notifications UI for a smoother experience. We've merged the tables into one comprehensive, filterable, and searchable table. Users can now search for specific notifications using _transaction id_ or _address_. See more on [Notifications page](https://dashboard.tatum.io/notifications).

<figure><img src=".gitbook/assets/Screenshot 2024-01-15 at 6.52.04 PM.png" alt=""><figcaption><p>The user searched for the transaction ID which returned the exact notification that was triggered with Request &#x26; Response.<br> <a href="https://dashboard.tatum.io/notifications">https://dashboard.tatum.io/notifications</a></p></figcaption></figure>

***

### Dec 12 2023 - Flare Network  (new RPC offering)&#x20;

[Get started using the Flare network here.](docs/rpc/evm-blockchains/flare-rpc-documentation/)

***

### Nov 24 2023 - API Key is now a required parameter for Faucets

To ensure that the faucet service is not abused we have updated the [fund](broken-reference) function in the Faucets submodule to require a testnet key, which can be acquired for free in our [dashboard](https://dashboard.tatum.io).

```typescript
import { TatumSDK, Network, Ethereum } from '@tatumio/tatum'

// What changed
const tatum = await TatumSDK.init<Ethereum>({
  network: Network.ETHEREUM_SEPOLIA,
  // Include this line to have api key.
  apiKey: { v4: 'YOUR-API-KEY'}
})
```

> :key: **Don’t have an API key?** Unlock all networks, features and monitor error logs & usage.\
> [<mark style="color:green;">**Create API key for FREE**</mark>](https://dashboard.tatum.io/)

***

### Nov 12 2023 - Haqq Network (new RPC offering)

[Get started using the Haqq network here.](docs/rpc/evm-blockchains/haqq-rpc-documentation/)

***

### Oct 15 2023 - Transactions Simulator available as Extension in SDK

Transaction Simulator has finally arrived and you can now use the [Simulate Transfer function](docs/transaction-simulator/simulate-transfer.md) to see what changes a transaction would make on the balances when sent on chain. We currently support Simulator only for EVM chains. \
[Read more in the Transaction Simulator Submodule Page](docs/transaction-simulator/)

***

### Oct 12 2023 - Horizen Eon (new RPC offering)

[Get started using the Horizen network here.](docs/rpc/evm-blockchains/horizen-eon-rpc-documentation/)

***

### Oct 4 2023 - IPFS features supported in Tatum SDK

IPFS is very crucial in the web3 world, whether you need to store the metadata of NFTs or some information about the levels of the game you might be building. We totally get that, and that's why we are happy to introduce you to the IPFS Submodule, Currently we only support upload functionality, which can be accessed on this[ upload function page.](docs/ipfs/upload-file.md)

***

### Sep 12 2023 - Exchange Rates available in Tatum SDK

Exchange rate submodule allows you to fetch the current exchange rates of wide range of cryptocurrencies against major fiats, you can read about the supported currencies in the [Exchange Rate Submodule Section.](docs/exchange-rates/)
