# eth\_chainId

### How to use it

{% tabs %}
{% tab title="TypeScript/JavaScript" %}
{% code overflow="wrap" lineNumbers="true" %}
```typescript
// yarn add @tatumio/tatum

import { TatumSDK, Klaytn, Network } from '@tatumio/tatum'

const tatum = await TatumSDK.init<Klaytn>({network: Network.KLAYTN})

const id = await tatum.rpc.chainId()

tatum.destroy() // Destroy Tatum SDK - needed for stopping background jobs
```
{% endcode %}
{% endtab %}
{% endtabs %}

### Overview

The `klay_chainId` method is an JSON-RPC method that allows developers to retrieve the currently configured chain ID of the network they are connected to. The chain ID is a unique identifier for different networks, such as mainnet or various testnets.

This method is particularly useful when building applications that interact with multiple networks or need to verify the network to prevent replay attacks. By checking the chain ID, an application can ensure it is interacting with the intended network.

### Parameters

The `klay_chainId` method does not have any input parameters.

### Return Object

The return object contains a single field:

* **`chainId`**: The hexadecimal string representation of the chain ID.

### Example Request and Response

JSON-RPC request:

```json
{
  "jsonrpc": "2.0",
  "id": 1,
  "method": "klay_chainId",
  "params": []
}
```

JSON-RPC response:

```json
{
    "jsonrpc": "2.0",
    "id": 1,
    "result": "0xe"
}
```

