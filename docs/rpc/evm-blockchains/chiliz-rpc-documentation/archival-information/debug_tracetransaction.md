# debug\_traceTransaction

### How to use it

{% tabs %}
{% tab title="TypeScript/JavaScript" %}
{% code overflow="wrap" lineNumbers="true" %}
```typescript
// yarn add @tatumio/tatum

import { TatumSDK, Chiliz, Network} from '@tatumio/tatum'

const tatum = await TatumSDK.init<Chiliz>({network: Network.CHILIZ})

const result = await tatum.rpc.debugTraceTransaction('0x98ce8f8d9b941cda7d1f199daba347a321514cb223dee06ef7e4fa0094882fc7', {
  tracer: 'callTracer',
  tracerConfig: {
      onlyTopCall: true,
      timeout: '5s',
  }
})

tatum.destroy() // Destroy Tatum SDK - needed for stopping background jobs
```
{% endcode %}
{% endtab %}
{% endtabs %}

### Overview

`debug_traceTransaction` is an RPC method that allows developers to inspect and trace the execution of a specific transaction, providing valuable insight into the internal workings of the transaction, including the calls made between contracts, the state of the contracts, and any errors encountered during the transaction.

By using the `callTracer` tracer, developers can obtain more detailed information about the calls made during the transaction, including the input, output, and the depth of the calls. This is particularly useful in debugging complex transactions, analyzing gas consumption, and understanding the flow of execution within smart contracts.

### Parameters

* `transaction_hash` (required): The hash of the transaction to trace.
  * Example: `"0x123f681646d4a755815f9cb19e1acc8565a0c2ac"`
* `options` (optional): An object containing configuration options for the tracer.
  * `tracer` (required, string): The tracer to use, in this case, `'callTracer'`.
  * `tracerConfig` (required, string): object containing `'timeout'` and `'onlyTopCall'` paramter
    * `timeout` (required, string): The maximum amount of time the tracer is allowed to run in seconds (e.g. "10s"). Default is "5s".
    * `onlyTopCall` (required, boolean): Setting this to true will only trace the main (top-level) call and none of the sub-calls. This avoids extra processing for each call frame if only the top-level call info is required (useful for getting revertReason).
  * Example: `{ tracer: 'callTracer', tracerConfig: { onlyTopCall: true, timeout: '5s', }}`

### Return Object

The return object is an object containing the following fields:

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

### JSON-RPC Request and Response Examples

#### Request

```json
{
  "jsonrpc": "2.0",
  "method": "debug_traceTransaction",
  "params": ["0x920d562e886a0c7c1f07ecee2ee5557f72d3056b205f8811c57e2615a3b6adb0", {"tracer":"callTracer"}],
  "id": 2
}
```

#### Response

```json
{
    "jsonrpc": "2.0",
    "id": 2,
    "result": {
        "from": "0x0a6d033f6628ef715732d61e059187b7330305ff",
        "gas": "0x51fba",
        "gasUsed": "0x41711",
        "to": "0x19e870855cb8fd8f6689743d3c28311c0d62a24c",
        "input": "0xcba9bc66000000000000000000000000f62ef040fb5ea7d0828ff50bced9a7720f1387c7000000000000000000000000325e343f1de602396e256b67efd1f61c3a6b38bd00000000000000000000000000000000000000000000000000000000000000e00000000000000000000000000000000000000000000000000000000000000160000000000000000000000000000000000000000000000001158e460913d000000000000000000000000000000000000000000000000000000100a08761e1547f0000000000000000000000000a6d033f6628ef715732d61e059187b7330305ff000000000000000000000000000000000000000000000000000000000000000300000000000000000000000055d398326f99059ff775485246999027b319795500000000000000000000000053e562b9b7e5e94b81f10e96ee70ad06df3d265700000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000",
        "output": "0x0000000000000000000000000000000000000000000000000102b1eda6a2682d",
        "calls": [
            {
                "from": "0x19e870855cb8fd8f6689743d3c28311c0d62a24c",
                "gas": "0x4f638",
                "gasUsed": "0x4cf",
                "to": "0x55d398326f99059ff775485246999027b3197955",
                "input": "0x70a082310000000000000000000000000a6d033f6628ef715732d61e059187b7330305ff",
                "output": "0x00000000000000000000000000000000000000000000002ca114a674b092dd94",
                "type": "STATICCALL"
            }
        ],
        "value": "0x0",
        "type": "CALL"
    }
}
```
