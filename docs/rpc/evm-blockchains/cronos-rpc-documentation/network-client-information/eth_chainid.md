# eth\_chainId

### How to use it

{% tabs %}
{% tab title="TypeScript/JavaScript" %}
{% code overflow="wrap" lineNumbers="true" %}
```typescript
// yarn add @tatumio/tatum

import { TatumSDK, Cronos, Network } from '@tatumio/tatum'
  
const tatum = await TatumSDK.init<Cronos>({network: Network.CRONOS})

const id = await tatum.rpc.chainId()

await tatum.destroy() // Destroy Tatum SDK - needed for stopping background jobs
```
{% endcode %}
{% endtab %}
{% endtabs %}

### Overview

The `eth_chainId` method is an JSON-RPC method that allows developers to retrieve the currently configured chain ID of the network they are connected to. The chain ID is a unique identifier for different networks, such as Mainnet or various testnets.

This method is particularly useful when building applications that interact with multiple networks or need to verify the network to prevent replay attacks. By checking the chain ID, an application can ensure it is interacting with the intended network.

### Parameters

The `eth_chainId` method does not have any input parameters.

### Return Object

The return object contains a single field:

* **`chainId`**: The hexadecimal string representation of the chain ID.