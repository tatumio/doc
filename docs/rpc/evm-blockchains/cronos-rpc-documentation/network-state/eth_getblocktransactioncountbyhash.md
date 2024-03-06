# eth\_getBlockTransactionCountByHash

### How to use it

{% tabs %}
{% tab title="TypeScript/JavaScript" %}
{% code overflow="wrap" lineNumbers="true" %}
```typescript
// yarn add @tatumio/tatum

import { TatumSDK, Cronos, Network } from '@tatumio/tatum'
  
const tatum = await TatumSDK.init<Cronos>({network: Network.CRONOS})

const response = await tatum.rpc.getBlockTransactionCountByHash('0x6565fd5921f93655e77d8cfeab8aa6caaf7155aeae24e91cdca33eedc66e6c5a')

await tatum.destroy() // Destroy Tatum SDK - needed for stopping background jobs
```
{% endcode %}
{% endtab %}
{% endtabs %}

### Overview

`eth_getBlockTransactionCountByHash` is an RPC method used to fetch the number of transactions in a block by the block's hash. It is useful when you want to know the total number of transactions included in a specific block and don't want to retrieve the entire block data. This method can be used in various scenarios, such as monitoring the network activity or estimating transaction confirmation times.

### Parameters

This method requires a single parameter:

* **`blockHash`**: The hash of the target block for which the transaction count will be retrieved. It should be a valid 32-byte hex string.

Example of the parameter:

* `blockHash`: `"0x6565fd5921f93655e77d8cfeab8aa6caaf7155aeae24e91cdca33eedc66e6c5a"`

### Return

The method returns a single value:

* `transactionCount`: The total number of transactions included in the specified block. It is returned as a hexadecimal value.