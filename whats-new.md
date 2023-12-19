---
description: Here's all that has been updated or shipped recently.
---

# 🎁 What's New

{% hint style="info" %}
[**Join our Discord**](https://discord.com/invite/tatum) to stay up to date with the latest updates from product news to upcoming events. You'll also be able to submit feedback and help shape future updates. Learn more about our community [here](https://tatum.io/community).&#x20;
{% endhint %}

### Dec 12 - Flare Network  (new RPC offering)&#x20;

[Get started using the Flare network here.](docs/rpc/evm-blockchains/flare-rpc-documentation/)

***

### Nov 24 - API Key is now a required parameter for Faucets

To ensure that the faucet service is not abused we have updated the [fund](docs/faucets/fund.md) function in the Faucets submodule to require a testnet key, which can be acquired for free in our [dashboard](https://dashboard.tatum.io).

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
> [<mark style="color:green;">**Create API key for F**</mark>](https://dashboard.tatum.io/)<mark style="color:green;">**REE**</mark> &#x20;

***

### Nov 21 - Faucets now available in Tatum SDK

We now have a Faucet Submodule which has a fund function to get you your testnet tokens without the need of leaving your coding environment. We allow any wallet that has a low wallet balance for supported testnets to request a testnet token once a day. \
[Read more on the Faucets Submodule Page.](docs/faucets/)

***

### Nov 12 - Haqq Network (new RPC offering)

[Get started using the Haqq network here.](docs/rpc/evm-blockchains/haqq-rpc-documentation/)

***

### Oct 15 - Transactions Simulator available as Extension in SDK

Transaction Simulator has finally arrived and you can now use the [Simulate Transfer function](docs/transaction-simulator/simulate-transfer.md) to see what changes a transaction would make on the balances when sent on chain. We currently support Simulator only for EVM chains. \
[Read more in the Transaction Simulator Submodule Page](docs/transaction-simulator/)

***

### Oct 12 - Horizen Eon (new RPC offering)

[Get started using the Horizen network here.](docs/rpc/evm-blockchains/horizen-eon-rpc-documentation/)

***

### Oct 4 - IPFS features supported in Tatum SDK

IPFS is very crucial in the web3 world, whether you need to store the metadata of NFTs or some information about the levels of the game you might be building. We totally get that, and that's why we are happy to introduce you to the IPFS Submodule, Currently we only support upload functionality, which can be accessed on this[ upload function page.](docs/ipfs/upload-file.md)

***

### Sep 12 - Exchange Rates available in Tatum SDK

Exchange rate submodule allows you to fetch the current exchange rates of wide range of cryptocurrencies against major fiats, you can read about the supported currencies in the [Exchange Rate Submodule Section.](docs/exchange-rates/)
