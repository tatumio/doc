---
description: >-
  This endpoint can help you fetch all the Assets a wallet holds including
  native tokens, fungible tokens, non fungible tokens & multitokens.
---

# Get all assets the wallet holds

{% embed url="https://codepen.io/tatum-devrel/pen/xxQmQxG" %}

Managing digital assets across various blockchain networks can be a challenging task. However, with TatumSDK, a powerful TypeScript library, developers can effortlessly retrieve wallet balances from multiple blockchains using a unified interface. This guide will demonstrate how to leverage TatumSDK's cross-chain capabilities to obtain wallet balances on Ethereum and Bitcoin, two popular, yet different blockchain networks. By following the steps outlined, you'll be able to streamline the development process and build applications that easily interact with multiple blockchains, saving time and reducing complexity.

### How to get a balance on Ethereum network

Use the TatumSDK (`@tatumio/tatum`) to get a balance of the wallet.

{% hint style="info" %}
TatumSDK wraps multiple different calls to the Tatum API together in 1 function, so we don't show here the curl example for using direct HTTP API calls. You can check the [API documentation](https://apidoc.tatum.io/tag/Data-API#operation/GetBalances) for specific operations, which are internally used [inside the library](https://github.com/tatumio/tatum-js/blob/master/src/service/address/address.ts).
{% endhint %}

{% tabs %}
{% tab title="TypeScript" %}
{% code overflow="wrap" lineNumbers="true" %}
```typescript
// yarn add @tatumio/tatum
import {TatumSDK, Network, Ethereum, ResponseDto, AddressBalance} from '@@tatumio/tatum'

const tatum = await TatumSDK.init<Ethereum>({network: Network.ETHEREUM})

const balance: ResponseDto<AddressBalance[]> = await tatum.address.getBalance({
  addresses: ['0xF64E82131BE01618487Da5142fc9d289cbb60E9d'], // replace with your address
})

console.log(balance.data)
```
{% endcode %}
{% endtab %}

{% tab title="JavaScript" %}
{% code overflow="wrap" lineNumbers="true" %}
```javascript
// Install with: npm install @tatumio/tatum
import { TatumSDK, Network } from "@tatumio/tatum";

(async () => {
  try {
    const tatum = await TatumSDK.init({ network: Network.ETHEREUM });
    const balance = await tatum.address.getBalance({
      addresses: ['0xF64E82131BE01618487Da5142fc9d289cbb60E9d'], // replace with your address
    });
    console.log(balance.data);
  } catch (error) {
    console.error("Error fetching wallet balance:", error);
  }
})();
```
{% endcode %}
{% endtab %}
{% endtabs %}

<details>

<summary>Expected Response</summary>

```javascript
[
    {
        asset: 'ETH',
        address: '0xF64E82131BE01618487Da5142fc9d289cbb60E9d',
        decimals: 18,
        balance: '0.001',
        type: 'native',
    }
]
```

</details>

### How to get a balance on the Bitcoin network

In order to get a balance of a Bitcoin address, you can use the same approach and reuse the same code.

{% tabs %}
{% tab title="TypeScript" %}
{% code overflow="wrap" lineNumbers="true" %}
```typescript
// yarn add @tatumcom/js
import {TatumSDK, Network, Bitcoin, ResponseDto, AddressBalance} from '@tatumio/tatum'

const tatum = await TatumSDK.init<Bitcoin>({network: Network.BITCOIN})

const balance: ResponseDto<AddressBalance[]> = await tatum.address.getBalance({
  addresses: ['bc1q7zw9ax8tm4jk2k2674u6lcd9fwjut8kqtvfeg8'], // replace with your address
})

console.log(balance.data)

// Expected outcome
// [{
//     asset: 'BTC',
//     address: 'bc1q7zw9ax8tm4jk2k2674u6lcd9fwjut8kqtvfeg8',
//     decimals: 8,
//     balance: '0.001',
//     type: 'native',
// }]
```
{% endcode %}
{% endtab %}

{% tab title="JavaScript" %}
{% code overflow="wrap" lineNumbers="true" %}
```javascript
// Install with: npm install @tatumcom/js
const { TatumSDK, Network } = require("@tatumio/tatum");

(async () => {
  try {
    const tatum = await TatumSDK.init({ network: Network.BITCOIN });
    const balance = await tatum.address.getBalance({
      addresses: ["bc1q7zw9ax8tm4jk2k2674u6lcd9fwjut8kqtvfeg8"], // replace with your address
    });
    console.log(balance.data);
  } catch (error) {
    console.error("Error fetching wallet balance:", error);
  }
})();

// Expected outcome
// [{
//     asset: 'BTC',
//     address: 'bc1q7zw9ax8tm4jk2k2674u6lcd9fwjut8kqtvfeg8',
//     decimals: 8,
//     balance: '0.001',
//     type: 'native',
// }]
```
{% endcode %}
{% endtab %}
{% endtabs %}

You can see, that the same request and response is used for different blockchain networks.

### Request interface

{% code overflow="wrap" lineNumbers="true" %}
```typescript
interface AddressBalanceDetails {
  /**
   * List of addresses to check. Some blockchain network supports only 1 address at a time
   */
  addresses: string[]
  /**
   * Optional page size. If not specified, the default page size is used, which is 10.
   */
  pageSize?: number
  /**
   * Optional page number. If not specified, the first page is returned.
   */
  page?: number
}
```
{% endcode %}

### Response interface

{% code overflow="wrap" lineNumbers="true" %}
```typescript
interface ResponseDto<T> {
  /**
   * Actual payload of the response
   */
  data: T
  /**
   * Status of the response
   */
  status: Status
  /**
   * In case of ERROR status, this field contains the error message and detailed description
   */
  error?: ErrorWithMessage
}

interface AddressBalance {
  /**
   * Blockchain address of the balance.
   */
  address: string
  /**
   * Asset of the balance. For native currencies, it's always present. For tokens, only when readable from the contract `symbol()` method.
   */
  asset?: string
  /**
   * Decimals of the asset. Valid for native and fungible tokens. For tokens, only when readable from the contract `decimals()` method.
   */
  decimals?: number
  /**
   * Balance of the address.
   */
  balance: string
  /**
   * Type of the balance.
   */
  type: 'native' | 'fungible' | 'nft' | 'mutlitoken'
  /**
   * Optional token contract address. Valid only for tokens (USDT, NFTs of any kind), not for native network balances (ETH, BTC).
   */
  tokenAddress?: string
  /**
   * Optional token ID. Valid only for non-fungible and semi-fungible tokens.
   */
  tokenId?: string
  /**
   * Block number of the last balance update.
   */
  lastUpdatedBlock?: number
}
```
{% endcode %}

### Supported blockchain networks

<table><thead><tr><th width="417">Network</th><th>Support</th></tr></thead><tbody><tr><td>Ethereum / Ethereum Sepolia / Ethereum Goerli<br>BNB Smart Chain / BNB Smart Chain Testnet<br>Celo / Celo Alfajores<br>Polygon / Polygon Mumbai</td><td>Multiple addresses per 1 invocation<br>Native Assets<br>ERC-20 Tokens (USDT, USDC,...)<br>NFTs (BAYC,...)<br>ERC-1155 Tokens</td></tr><tr><td>Solana / Solana Devnet</td><td>Multiple addresses per 1 invocation<br>Native Assets (SOL)</td></tr><tr><td>XRP / XRP Testnet<br>Bitcoin / Bitcoin Testnet<br>Litecoin / Litecoin Testnet<br>Dogecoin / Dogecoin Testnet<br>Cardano / Cardano Preprod</td><td>Native Assets<br>Only 1 address per 1 invocation</td></tr></tbody></table>
