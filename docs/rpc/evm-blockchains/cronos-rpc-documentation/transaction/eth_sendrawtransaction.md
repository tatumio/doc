# eth\_sendRawTransaction

### How to use it

{% tabs %}
{% tab title="TypeScript/JavaScript" %}
{% code overflow="wrap" lineNumbers="true" %}
```typescript
// yarn add @tatumio/tatum

import { TatumSDK, Cronos, Network } from '@tatumio/tatum'
  
const tatum = await TatumSDK.init<Cronos>({network: Network.CRONOS})

const gasPrice = await tatum.rpc.sendRawTransaction('0x0000.......')

await tatum.destroy() // Destroy Tatum SDK - needed for stopping background jobs
```
{% endcode %}
{% endtab %}
{% endtabs %}

### Overview

The `eth_sendRawTransaction` RPC method is used to send a signed and serialized transaction to the network. This method is particularly useful when you want to have full control over the signing process, e.g., when using hardware wallets, cold storage, or custom signing libraries. It can be utilized in various use cases, such as transferring currency, interacting with smart contracts, or deploying new contracts.

### Parameters

The method accepts a single parameter:

* **`data`**: The signed and serialized transaction data as a hexadecimal string.

### Return Value

The method returns a single value:

* `transactionHash`: The hash of the submitted transaction as a hexadecimal string, e.g., `"0x9fc76417374aa880d4449a1f7f31ec597f00b1f6f3dd2d66f4c9c6c445836d8b"`.