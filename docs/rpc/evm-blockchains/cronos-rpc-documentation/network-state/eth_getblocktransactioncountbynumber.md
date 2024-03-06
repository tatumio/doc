# eth\_getBlockTransactionCountByNumber

### How to use it

{% tabs %}
{% tab title="TypeScript/JavaScript" %}
{% code overflow="wrap" lineNumbers="true" %}
```typescript
// yarn add @tatumio/tatum

import { TatumSDK, Cronos, Network } from '@tatumio/tatum'
  
const tatum = await TatumSDK.init<Cronos>({network: Network.CRONOS})

const response = await tatum.rpc.getBlockTransactionCountByNumber('0xC44FF8')

await tatum.destroy() // Destroy Tatum SDK - needed for stopping background jobs
```
{% endcode %}
{% endtab %}
{% endtabs %}

### Overview

The `eth_getBlockTransactionCountByNumber` JSON-RPC method allows you to retrieve the number of transactions in a specified block. This method is particularly useful when you need to analyze the transaction activity of a specific block. You can use it to gain insights into network usage, analyze the impact of specific events on the network, or monitor transaction congestion in certain blocks.

### Parameters

1. **`blockNumber`**: The block number for which the transaction count should be retrieved. It should be a hex-encoded value representing the block number.
   * Example: `"0xC44FF8"` 

### Return Object

The return object is a hex-encoded value representing the number of transactions in the specified block.

* Example: `"0xa"` (10 transactions)