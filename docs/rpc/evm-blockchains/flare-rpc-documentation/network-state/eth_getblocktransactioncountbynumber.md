# eth\_getBlockTransactionCountByNumber

### How to use it

{% tabs %}
{% tab title="TypeScript/JavaScript" %}
{% code overflow="wrap" lineNumbers="true" %}
```typescript
// yarn add @tatumio/tatum

import { TatumSDK, Flare, Network } from '@tatumio/tatum'
  
const tatum = await TatumSDK.init<Flare>({network: Network.FLARE})

const response = await tatum.rpc.getBlockTransactionCountByNumber('0xAD7C5E')

tatum.destroy() // Destroy Tatum SDK - needed for stopping background jobs
```
{% endcode %}
{% endtab %}
{% endtabs %}

### Overview

The `eth_getBlockTransactionCountByNumber` Flare JSON-RPC method allows you to retrieve the number of transactions in a specified block. This method is particularly useful when you need to analyze the transaction activity of a specific block. You can use it to gain insights into network usage, analyze the impact of specific events on the Flare network, or monitor transaction congestion in certain blocks.

### Parameters

1. **`blockNumber`**: The block number for which the transaction count should be retrieved. It should be a hex-encoded value representing the block number.
   * Example: `"0x1b4"` (block number 436)

### Return Object

The return object is a hex-encoded value representing the number of transactions in the specified block.

* Example: `"0xa"` (10 transactions)

### JSON-RPC Request and Response Examples

#### Request

```json
{
  "jsonrpc": "2.0",
  "id": 1,
  "method": "eth_getBlockTransactionCountByNumber",
  "params": ["0x1b4"]
}
```

#### Response

```json
{
  "jsonrpc": "2.0",
  "id": 1,
  "result": "0xa"
}
```



\
