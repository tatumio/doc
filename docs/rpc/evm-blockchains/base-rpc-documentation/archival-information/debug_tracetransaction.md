# debug_traceTransaction

### How to use it

{% tabs %}
{% tab title="TypeScript/JavaScript" %}
{% code overflow="wrap" lineNumbers="true" %}

```typescript
// yarn add @tatumio/tatum

import { TatumSDK, Base, Network } from "@tatumio/tatum";

const tatum = await TatumSDK.init<Base>({ network: Network.BASE });

const result = await tatum.rpc.debugTraceTransaction(
  "0xa36e0435dd125093711d3ef25b1d4eb87cb39889ca8d351625cdfe7d0186b439",
  {
    tracer: "callTracer",
    tracerConfig: {
      onlyTopCall: true,
      timeout: "5s",
    },
  }
);

await tatum.destroy(); // Destroy Tatum SDK - needed for stopping background jobs
```

{% endcode %}
{% endtab %}
{% endtabs %}

### Overview

`debug_traceTransaction` is an RPC method that allows developers to inspect and trace the execution of a specific transaction, providing valuable insight into the internal workings of the transaction, including the calls made between contracts, the state of the contracts, and any errors encountered during the transaction.

By using the `callTracer` tracer, developers can obtain more detailed information about the calls made during the transaction, including the input, output, and the depth of the calls. This is particularly useful in debugging complex transactions, analyzing gas consumption, and understanding the flow of execution within smart contracts.

### Parameters

- `transaction_hash` (required): The hash of the transaction to trace.
  - Example: `"0xa36e0435dd125093711d3ef25b1d4eb87cb39889ca8d351625cdfe7d0186b439"`
- `options` (optional): An object containing configuration options for the tracer.
  - `tracer` (required, string): The tracer to use, in this case, `'callTracer'`.
  - `tracerConfig` (required, string): object containing `'timeout'` and `'onlyTopCall'` paramter
    - `timeout` (required, string): The maximum amount of time the tracer is allowed to run in seconds (e.g. "10s"). Default is "5s".
    - `onlyTopCall` (required, boolean): Setting this to true will only trace the main (top-level) call and none of the sub-calls. This avoids extra processing for each call frame if only the top-level call info is required (useful for getting revertReason).
  - Example: `{ tracer: 'callTracer', tracerConfig: { onlyTopCall: true, timeout: '5s', }}`

### Return Object

The return object is an object containing the following fields:

- `from`: The address the transaction was sent from.
- `gas`: The gas provided for the transaction.
- `gasUsed`: The total gas used by the transaction.
- `to`: The address the transaction was sent to.
- `input`: The input data for the transaction.
- `output`: The output data from the transaction.
- `calls`: An array of objects, each representing a call made during the transaction. Each object contains:
  - `from`: The address the call was made from.
  - `gas`: The gas provided for the call.
  - `gasUsed`: The gas used by the call.
  - `to`: The address the call was made to.
  - `input`: The input data for the call.
  - `output`: The output data from the call.
  - `type`: The type of the call (e.g., "STATICCALL").

{% hint style="info" %}
This method is available only on the full archive node.
{% endhint %}

#### Response

```json
{
    "jsonrpc": "2.0",
    "id": 1,
    "result": {
        "gas": 46913,
        "failed": false,
        "returnValue": "",
        "structLogs": [
            {
                "pc": 0,
                "op": "PUSH1",
                "gas": 977072,
                "gasCost": 3,
                "depth": 1,
                "stack": []
            },
            {
                "pc": 2,
                "op": "PUSH1",
                "gas": 977069,
                "gasCost": 3,
                "depth": 1,
                "stack": [
                    "0x80"
                ]
            },...
        ]
    }
}
```
