# eth\_maxPriorityFeePerGas

### How to use it

{% tabs %}
{% tab title="TypeScript/JavaScript" %}
{% code overflow="wrap" lineNumbers="true" %}
```typescript
// yarn add @tatumio/tatum

import { TatumSDK, Cronos, Network } from '@tatumio/tatum'
  
const tatum = await TatumSDK.init<Cronos>({network: Network.CRONOS})

const gasPrice = await tatum.rpc.maxPriorityFeePerGas()

await tatum.destroy() // Destroy Tatum SDK - needed for stopping background jobs
```
{% endcode %}
{% endtab %}
{% endtabs %}

### Overview

The `eth_maxPriorityFeePerGas` RPC method is used to retrieve the maximum priority fee per gas set by the user for a transaction. This method can be used to determine the maximum fee that can be paid for a transaction to be included in a block quickly.

### Use case

This method is particularly useful when the user wants to ensure that a transaction is processed quickly, even in a congested network where transaction fees may fluctuate rapidly. By setting a high maximum priority fee per gas, the user can ensure that the transaction is processed as quickly as possible.

### Parameters

`None.`

## Return Object

* `maxPriorityFeePerGas` - The maximum priority fee per gas the user is willing to pay, in wei.