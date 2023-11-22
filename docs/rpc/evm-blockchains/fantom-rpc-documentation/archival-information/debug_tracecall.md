# debug\_traceCall

### How to use it

{% tabs %}
{% tab title="TypeScript/JavaScript" %}
{% code overflow="wrap" lineNumbers="true" %}
```typescript
// yarn add @tatumio/tatum

import { TatumSDK, Fantom, Network } from '@tatumio/tatum'
  
const tatum = await TatumSDK.init<Fantom>({ network: Network.FANTOM })

const result = await tatum.rpc.debugTraceCall({
      "from": "0x365a2dabcdb56f4f595c3af088b8975c26331448",
      "to": "0x365a2dabcdb56f4f595c3af088b8975c26331449",
      "gas": "0x76c0",
      "gasPrice": "0x9184e72a000",
      "value": "0x9184e72a",
      "data": "0x606060..."
    },
    "0x42C1D80",
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

`debug_traceCall` is an method that allows you to execute a given call (message), tracing the steps of its execution. This can be helpful for developers and auditors who want to inspect and analyze the internal operations and state changes of a contract call without modifying the blockchain state. This method can assist in debugging and identifying potential issues with contract execution, as well as understanding how gas is consumed during the execution of a call.

### Parameters

The `debug_traceCall` method accepts the following parameters:

* `transaction`: An object that contains the following fields:
  * `from`: The address from which the call is initiated. Example: `"0xa7d9ddbe1f17865597fbd27ec712455208b6b76d"`
  * `to`: The address of the contract to be called. Example: `"0x742d35Cc6634C0532925a3b844Bc454e4438f44e"`
  * `gas`: (Optional) The gas limit for the call. Example: `"0x76c0"`
  * `gasPrice`: (Optional) The gas price for the call. Example: `"0x9184e72a000"`
  * `value`: (Optional) The value to be transferred during the call. Example: `"0x9184e72a"`
  * `data`: (Optional) The input data for the call, encoded as a hexadecimal string. Example: `"0x606060..."`
* `blockNumber`: The block number as a hexadecimal string for which the call should be traced. Example: `"0x42C1D80"`

### Return Object

The return object is an object containing the following fields:

* `output`: The output data from the call.
* `gasUsed`: The total gas used by the call.
* `calls`: An array of objects, each representing a nested call made during the call. Each object contains:
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

<pre class="language-json"><code class="lang-json">{
  "jsonrpc": "2.0",
  "id": 1,
  "method": "debug_traceCall",
  "params": [
    {
      "from": "0xa7d9ddbe1f17865597fbd27ec712455208b6b76d",
      "to": "0x742d35Cc6634C0532925a3b844Bc454e4438f44e",
      "gas": "0x76c0",
      "gasPrice": "0x9184e72a000",
      "value": "0x9184e72a",
<strong>      "data": "0x606060..."
</strong>    },
    "0x1b4"
  ]
}
</code></pre>

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
