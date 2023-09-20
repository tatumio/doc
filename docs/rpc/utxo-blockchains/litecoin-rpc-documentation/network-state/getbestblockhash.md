# getbestblockhash

### How to use it

{% tabs %}
{% tab title="TypeScript/JavaScript" %}
{% code overflow="wrap" lineNumbers="true" %}
```typescript
// yarn add @tatumio/tatum

import { TatumSDK, Litecoin, Network } from '@tatumio/tatum'

const tatum = await TatumSDK.init<Litecoin>({network: Network.LITECOIN})

const result = await tatum.rpc.getBestBlockHash()

tatum.destroy() // Destroy Tatum SDK - needed for stopping background jobs
```
{% endcode %}
{% endtab %}
{% endtabs %}

### Overview

`getbestblockhash` is a Litecoin RPC method that returns the hash of the best (tip) block in the longest blockchain. This method is useful for obtaining the latest block hash, which can be used to fetch block details or confirmations for transactions.

{% embed url="https://codepen.io/tatum-devrel/pen/vYQPLOd" %}

### Parameters

This method does not have any parameters.

### Return Object

The returned object is a string containing the hash of the best block.

### JSON Examples

Request example:

{% code overflow="wrap" lineNumbers="true" %}
```json
{
  "id": 1,
  "jsonrpc": "2.0",
  "method": "getbestblockhash"
}
```
{% endcode %}

Response example:

{% code overflow="wrap" lineNumbers="true" %}
```json
{
  "id": 1,
  "result": "0000000000000000000ef0e1f703b56f2b0d6724e4eeccf00e4f8d55b9c3c3f6e",
  "error": null
}
```
{% endcode %}

\
