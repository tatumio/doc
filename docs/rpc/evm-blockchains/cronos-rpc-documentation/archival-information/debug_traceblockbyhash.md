# debug\_traceBlockByHash

### How to use it

{% tabs %}
{% tab title="TypeScript/JavaScript" %}
{% code overflow="wrap" lineNumbers="true" %}
```typescript
// yarn add @tatumio/tatum

import { TatumSDK, Cronos, Network } from '@tatumio/tatum'
  
const tatum = await TatumSDK.init<Cronos>({network: Network.CRONOS})

const result = await tatum.rpc.debugTraceBlockByHash(
'0xe1ceb5e388aecc721a60691659ca7b388612d323cf75da6b9e766b8a440864c2',
{
  tracer: 'callTracer',
  tracerConfig: {
      onlyTopCall: true,
      timeout: '5s',
  }
}
)

await tatum.destroy() // Destroy Tatum SDK - needed for stopping background jobs
```
{% endcode %}
{% endtab %}
{% endtabs %}

### Overview

`debug_traceBlockByHash` is an RPC method that allows developers to trace all transactions within a block using a given tracer. This is particularly useful for analyzing the behavior of all transactions in a block, investigating potential issues, and understanding the flow of execution within smart contracts.

By using the `callTracer` tracer, developers can obtain more detailed information about the calls made during each transaction, including the input, output, and depth of the calls.

### Parameters

* `block_hash` (required): The hash of the block to be traced.
  * Example: `"0xe1ceb5e388aecc721a60691659ca7b388612d323cf75da6b9e766b8a440864c2"`
* `options` (optional): An object containing configuration options for the tracer.
  * `tracer` (required, string): The tracer to use, in this case, `'callTracer'`.
  * `tracerConfig` (required, string): object containing `'timeout'` and `'onlyTopCall'` paramter
    * `timeout` (required, string): The maximum amount of time the tracer is allowed to run in seconds (e.g. "10s"). Default is "5s".
    * `onlyTopCall` (required, boolean): Setting this to true will only trace the main (top-level) call and none of the sub-calls. This avoids extra processing for each call frame if only the top-level call info is required (useful for getting revertReason).
  * Example: `{ tracer: 'callTracer', tracerConfig: { onlyTopCall: true, timeout: '5s', }}`

### Return Object

The return object is an array of objects, each representing the trace result of a transaction within the block. Each object contains the following fields:

* `from`: The address the transaction was sent from.
* `gas`: The gas provided for the transaction.
* `gasUsed`: The total gas used by the transaction.
* `to`: The address the transaction was sent to.
* `input`: The input data for the transaction.
* `output`: The output data from the transaction.
* `calls`: An array of objects, each representing a call made during the transaction. Each object contains:
  * `from`: The address the call was made from.
  * `gas`: The gas provided for the call.
  * `gasUsed`: The gas used by the call.
  * `to`: The address the call was made to.
  * `input`: The input data for the call.
  * `output`: The output data from the call.
  * `type`: The type of the call (e.g., "STATICCALL").

{% hint style="info" %}
This method is available only on the full archive node.
{% endhint %}