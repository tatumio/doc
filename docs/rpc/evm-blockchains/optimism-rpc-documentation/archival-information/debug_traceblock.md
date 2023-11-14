# debug\_traceBlock

### How to use it

{% tabs %}
{% tab title="TypeScript/JavaScript" %}
{% code overflow="wrap" lineNumbers="true" %}
```typescript
// yarn add @tatumio/tatum

import { TatumSDK, Optimism, Network } from '@tatumio/tatum'
  
const tatum = await TatumSDK.init<Optimism>({network: Network.OPTIMISM})

const result = await tatum.rpc.debugTraceBlock('0xAD7C5E' ,{
  tracer: 'callTracer',
  tracerConfig: {
      onlyTopCall: true,
      timeout: '5s',
  }
})

await tatum.destroy() // Destroy Tatum SDK - needed for stopping background jobs
```
{% endcode %}
{% endtab %}
{% endtabs %}

### Overview

`debug_traceBlock` is an RPC method that allows developers to trace all transactions within a block using a given tracer. This is particularly useful for analyzing the behavior of all transactions in a block, investigating potential issues, and understanding the flow of execution within smart contracts.

By using the `debug_traceBlock`, developers can obtain detailed insights into the execution flow of each transaction, allowing for in-depth analysis and debugging

### Parameters

* `block` - `String`
  * RLP encoded block object.
* `options` (optional): An object containing configuration options for the tracer.
  * `tracer`: The tracer object with the following fields:
    * `callTracer`: The calltracer keeps track of all call frames, including depth 0 calls, made during a transaction.
    * `prestateTracer`: The prestateTracer replays the transaction and tracks every part of the state that occurred during the transaction.
  * `tracerConfig`: The object to specify the configurations of the tracer.
    * onlyTopCall: When set to true, it traces only the primary (top-level) call and not any sub-calls, eliminating additional processing for each call frame.

### Return Object

The return object is an array of all invoked opcodes of all transaction that were included in this block.

* `type`: The type of the call.
* `from`: The address from which the transaction is sent.
* `to`: The address to which the transaction is directed.
* `value`: The integer value sent with this transaction.
* `gas`: The integer value of the gas provided for the transaction execution.
* `gasUsed`: The integer value of the gas used.
* `input`: The data given at the time of input.
* `output`: The data returned as an output.
* `calls`: A list of sub-calls made during the transaction, including detailed trace information for each sub-call.

{% hint style="info" %}
This method is available only on the full archive node.
{% endhint %}

### JSON-RPC Request and Response Examples

#### Request

```json
{
  "id": 1,
  "jsonrpc": "2.0",
  "method": "debug_traceBlock",
  "params": [
    "0x1dc....",
    {
      "tracer": "callTracer"
    }
  ]
}

```

#### Response

```json
{
  "id": 1,
  "jsonrpc": "2.0",
  "result": [
        {
            "result": {
                "from": "0x8894e0a0c962cb723c1976a4421c95949be2d4e3",
                "gas": "0x2d48c",
                "gasUsed": "0xc7ab",
                "to": "0x55d398326f99059ff775485246999027b3197955",
                "input": "0xa9059cbb0000000000000000000000003b9f33b3a9d382fa60283c555bde8f78855957be00000000000000000000000000000000000000000000000d4e7f4f79da7c0000",
                "output": "0x0000000000000000000000000000000000000000000000000000000000000001",
                "value": "0x0",
                "type": "CALL"
            }
        }
    ]
}

```
