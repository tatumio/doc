# eth\_gasPrice

### How to use it

{% tabs %}
{% tab title="TypeScript/JavaScript" %}
{% code overflow="wrap" lineNumbers="true" %}
```typescript
// yarn add @tatumio/tatum

import { TatumSDK, Cronos, Network } from '@tatumio/tatum'
  
const tatum = await TatumSDK.init<Cronos>({network: Network.CRONOS})

const gasPrice = await tatum.rpc.gasPrice()

await tatum.destroy() // Destroy Tatum SDK - needed for stopping background jobs
```
{% endcode %}
{% endtab %}
{% endtabs %}

### Overview

The `eth_gasPrice` method is an JSON-RPC method used to estimate the average gas price required for transactions in the network. This method provides a suggestion for the gas price to be used in a transaction to increase the likelihood of it being mined and included in a block in a reasonable amount of time. The `eth_gasPrice` method is particularly useful for developers and users who want to create and send transactions, as it helps them estimate the appropriate gas price to ensure timely processing.

### Parameters

The `eth_gasPrice` method does not require any parameters.&#x20;

### Return Value

The `eth_gasPrice` method returns a single value as a hexadecimal string:

* `gasPrice`: The estimated average gas price in wei. Example: `"0x4a817c800"`