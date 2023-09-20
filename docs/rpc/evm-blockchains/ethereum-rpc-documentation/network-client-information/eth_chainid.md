# eth\_chainId

### How to use it

{% tabs %}
{% tab title="TypeScript/JavaScript" %}
{% code overflow="wrap" lineNumbers="true" %}
```typescript
// yarn add @tatumio/tatum

import { TatumSDK, Ethereum, Network } from '@tatumio/tatum'

const tatum = await TatumSDK.init<Ethereum>({network: Network.ETHEREUM})

const id = await tatum.rpc.chainId()

tatum.destroy() // Destroy Tatum SDK - needed for stopping background jobs
```
{% endcode %}
{% endtab %}
{% endtabs %}

### Overview

The `eth_chainId` method is an Ethereum JSON-RPC method that allows developers to retrieve the currently configured chain ID of the Ethereum network they are connected to. The chain ID is a unique identifier for different Ethereum networks, such as Ethereum Mainnet or various testnets.

This method is particularly useful when building applications that interact with multiple Ethereum networks or need to verify the network to prevent replay attacks. By checking the chain ID, an application can ensure it is interacting with the intended network.

{% embed url="https://codepen.io/tatum-devrel/pen/eYQxzzw" %}

### Parameters

The `eth_chainId` method does not have any input parameters.

### Return Object

The return object contains a single field:

* **`chainId`**: The hexadecimal string representation of the chain ID.

### Example Request and Response

JSON-RPC request:

```json
{
  "jsonrpc": "2.0",
  "id": 1,
  "method": "eth_chainId",
  "params": []
}
```

JSON-RPC response:

```json
{
  "jsonrpc": "2.0",
  "id": 1,
  "result": "0x1"
}
```

In this example, the returned chain ID is `0x1`, which corresponds to the Ethereum Mainnet.
