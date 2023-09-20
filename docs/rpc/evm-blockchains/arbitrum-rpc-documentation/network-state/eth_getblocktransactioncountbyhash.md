# eth\_getBlockTransactionCountByHash

### How to use it

{% tabs %}
{% tab title="TypeScript/JavaScript" %}
{% code overflow="wrap" lineNumbers="true" %}
```typescript
// yarn add @tatumio/tatum

import { TatumSDK, ArbitrumOne, Network } from '@tatumio/tatum'

const tatum = await TatumSDK.init<ArbitrumOne>({network: Network.ARBITRUM_ONE}

const response = await tatum.rpc.getBlockTransactionCountByHash('0xac02875a79dd5edd6595e4d4482a848f04d466e19ef8afcdf725722d9b0dabb2')

tatum.destroy() // Destroy Tatum SDK - needed for stopping background jobs
```
{% endcode %}
{% endtab %}
{% endtabs %}

### Overview

`eth_getBlockTransactionCountByHash` is a RPC method used to fetch the number of transactions in a block by the block's hash. It is useful when you want to know the total number of transactions included in a specific block and don't want to retrieve the entire block data. This method can be used in various scenarios, such as monitoring the network activity or estimating transaction confirmation times.

### Parameters

This method requires a single parameter:

* **`blockHash`**: The hash of the target block for which the transaction count will be retrieved. It should be a valid 32-byte hex string.

Example of the parameter:

* `blockHash`: `"0xac02875a79dd5edd6595e4d4482a848f04d466e19ef8afcdf725722d9b0dabb2"`

### Return

The method returns a single value:

* `transactionCount`: The total number of transactions included in the specified block. It is returned as a hexadecimal value.

### Examples

#### JSON-RPC request

```json
{
  "id": 1,
  "jsonrpc": "2.0",
  "method": "eth_getBlockTransactionCountByHash",
  "params": [
    "0xac02875a79dd5edd6595e4d4482a848f04d466e19ef8afcdf725722d9b0dabb2"
  ]
}
```

#### JSON-RPC response

```json
{
  "id": 1,
  "jsonrpc": "2.0",
  "result": "0xa"
}
```

In this example, the block with the hash `"`0xac02875a79dd5edd6595e4d4482a848f04d466e19ef8afcdf725722d9b0dabb2`"` has a total of 3 transactions (indicated by the hexadecimal value `"0x3"`).
