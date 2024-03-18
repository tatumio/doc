---
description: Here's all that has been updated or shipped recently.
---

# 🎁 What's New

{% hint style="info" %}
[**Join our Discord**](https://discord.com/invite/tatum) to stay up to date with the latest updates from product news to upcoming events. You'll also be able to submit feedback and help shape future updates. Learn more about our community [here](https://tatum.io/community).&#x20;
{% endhint %}

### Improved Fee Estimations for Transaction Success

**March 15, 2024 -** We're excited to announce significant enhancements to our Fee Estimation system! Our latest update introduces a more dynamic approach to handling transaction fees, especially designed to adapt to varying network conditions.

* **Adaptive Fee Estimations:** Our system now better recognises network congestion, adjusting fees accordingly to maximize the likelihood of your transactions being processed smoothly.
* **Uninterrupted Performance:** These improvements are designed to work seamlessly, ensuring that standard transaction activities remain unaffected, even during periods of high traffic.

You can enjoy a more reliable transaction experience on our platform, even during busy times.

***

### Expanded Payments & Billing Options with Yearly Subscriptions

**March 13, 2024** - We're thrilled to announce several exciting updates to our Payments & Billing system that make managing your subscriptions and payments easier and more flexible than ever!

* **Yearly Subscriptions:** By popular demand, Tatum now offers the option for Yearly Subscriptions, allowing you to enjoy our services with even more convenience and savings.

{% hint style="danger" %}
**Get ready for the bull market with a special yearly offer!**\
~~<mark style="color:red;">$39</mark>~~ <mark style="color:green;">**$25**</mark> / month for a year\
:point\_right: [**Upgrade plan**](https://dashboard.tatum.io/upgrade-plan)
{% endhint %}

* **Invoice Management:** Whenever a new invoice is generated, we'll share it directly with you as a PDF attachment via email, ensuring you always have easy access to billing documents.
* **Payment Methods:** We've broadened payment options to include WeChat Pay, Link, Cash App Pay, Google Pay, and Apple Pay - providing a wide range of choices to manage payments effortlessly.\
  \
  You can check and update your plan details and billing [here on dashboard](https://dashboard.tatum.io/upgrade-plan).

***

### Base (new RPC Offering)

**March 13, 2024** - We're excited to announce the launch of **Base**.

<img src=".gitbook/assets/full-base-logo.webp" alt="" data-size="original">

_Base is a secure, Ethereum Layer 2 network aimed at Web3 scalability - developed by Coinbase._\
_It offers a developer-friendly environment with low fees, full EVM compatibility, and does not require a native token. Designed to support a wide array of applications, including DeFi and NFTs._

:point\_right: [Get started using the Base network](https://docs.tatum.io/docs/rpc/evm-blockchains/base-rpc-documentation)

***

### Cronos (new RPC Offering)

**March 11, 2024** - We're excited to announce the launch of **Cronos**.

<img src=".gitbook/assets/full-cronos-logo.png" alt="" data-size="original">

_Cronos is a blockchain network that enhances interoperability with both Ethereum and Cosmos, aiming to expand the Web3 community. It supports DeFi, gaming, NFTs, and the Metaverse by enabling quick app porting with low costs, high throughput, and rapid finality._\
:point\_right: [Get started using the Cronos network](https://docs.tatum.io/docs/rpc/evm-blockchains/cronos-rpc-documentation)

***

### Chilliz Testnet Tokens available on Dashboard

**March 8, 2024 -** Access Chilliz testnet tokens directly from our platform through the newly implemented Chilliz Faucets on the dashboard. This feature is designed to support your testing and development activities, providing you with the resources you need to explore and innovate. \
:point\_right: [Get Chilliz tokens](https://dashboard.tatum.io/faucets)

<figure><img src=".gitbook/assets/Screenshot 2024-03-18 at 12.23.40.png" alt=""><figcaption><p>Chilliz Faucet on Dashboard</p></figcaption></figure>

***

### Full Control over API Keys: Create/delete/regenerate

**March 6, 2024** - With the new dashboard update, you have the ability to not only regenerate your API keys in response to security concerns but also to create new keys and delete those no longer needed.

You can manage your API keys completely, providing a secure, customisable experience.\
:point\_right: [Manage API keys](https://dashboard.tatum.io/)

> :key: **Don’t have an API key?** Unlock all networks, features and monitor error logs & usage.\
> [<mark style="color:green;">**Create API key for FREE**</mark>](https://dashboard.tatum.io/)

***

### Sunset of Goerli Network

**March 01, 2024** - As Goerli (Testnet Ethereum Network) has reached its end of life support, we have have removed the support for Goerli from all our Core Products Like RPC, Data Solution & more, from both API's & SDK.&#x20;

***

### Batch operations for BTC Related Endpoints

**February 26, 2024** - We have added batch support for two BTC Related Endpoints:

* [Get Unspent UTXO's for addresses batch](https://apidoc.tatum.io/tag/Data-API#operation/GetUtxosByAddressBatch)
* [Get Transactions for an address by Batch](https://apidoc.tatum.io/tag/Bitcoin#operation/BtcGetTxByAddressBatch)

***

### Dashboard - Extended Notifications Builder Support.

**February 20, 2024** - The Notification Builder in dashboard now supports creating notifications for **Tezos, Flare, Holesky & Cronos**, directly from the dashboard [here](https://dashboard.tatum.io/).

***

### Holesky (new RPC Offering)

**February 13, 2024** - We are excited to announce the support of Goerli Testnet.\
You can specify Holesky in SDK as Network.ETHEREUM\_HOLESKY\
:point\_right:  [Get started using the Holesky network](https://docs.tatum.io/docs/rpc/evm-blockchains/ethereum-rpc-documentation)

***

### Fantom (new RPC Offering)

**February 07, 2024 -** - We are excited to announce the support of Fantom Network.\
:point\_right:  [Get started using the Fantom network](https://docs.tatum.io/docs/rpc/evm-blockchains/fantom-rpc-documentation)

***

### Dashboard - Enhanced Notifications

**January 15, 2024** - We've revamped the Notifications UI for a smoother experience. We've merged the tables into one comprehensive, filterable, and searchable table. Users can now search for specific notifications using _transaction id_ or _address_. See more on [Notifications page](https://dashboard.tatum.io/notifications).

<figure><img src=".gitbook/assets/Screenshot 2024-01-15 at 6.52.04 PM.png" alt=""><figcaption><p>The user searched for the transaction ID which returned the exact notification that was triggered with Request &#x26; Response.<br> <a href="https://dashboard.tatum.io/notifications">https://dashboard.tatum.io/notifications</a></p></figcaption></figure>

***

### Flare Network  (new RPC offering)&#x20;

**December 12, 2023** - [Get started using the Flare network here.](docs/rpc/evm-blockchains/flare-rpc-documentation/)

***

### API Key is now a required parameter for Faucets

**November 24, 2023** -  To ensure that the faucet service is not abused we have updated the [fund](broken-reference) function in the Faucets submodule to require a testnet key, which can be acquired for free in our [dashboard](https://dashboard.tatum.io).

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

### Haqq Network (new RPC offering)

**November 12, 2023** - [Get started using the Haqq network here.](docs/rpc/evm-blockchains/haqq-rpc-documentation/)

***

### Transactions Simulator available as Extension in SDK

**October 15, 2023** - Transaction Simulator has finally arrived and you can now use the [Simulate Transfer function](docs/transaction-simulator/simulate-transfer.md) to see what changes a transaction would make on the balances when sent on chain. We currently support Simulator only for EVM chains. \
[Read more in the Transaction Simulator Submodule Page](docs/transaction-simulator/)

***

### Horizen Eon (new RPC offering)

**October 12, 2023** - [Get started using the Horizen network here.](docs/rpc/evm-blockchains/horizen-eon-rpc-documentation/)

***

### IPFS features supported in Tatum SDK

**October 4, 2023 -** IPFS is very crucial in the web3 world, whether you need to store the metadata of NFTs or some information about the levels of the game you might be building. We totally get that, and that's why we are happy to introduce you to the IPFS Submodule, Currently we only support upload functionality, which can be accessed on this[ upload function page.](docs/ipfs/upload-file.md)

***

### &#x20;Exchange Rates available in Tatum SDK

**September 12, 2023** - Exchange rate submodule allows you to fetch the current exchange rates of wide range of cryptocurrencies against major fiats, you can read about the supported currencies in the [Exchange Rate Submodule Section.](docs/exchange-rates/)
