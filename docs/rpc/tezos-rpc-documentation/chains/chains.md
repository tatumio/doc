# set_bootstrapped_flag

### How to use it

{% tabs %}
{% tab title="TypeScript/JavaScript" %}
{% code overflow="wrap" lineNumbers="true" %}
```typescript
// yarn add @tatumio/tatum

import { TatumSDK, Tezos, Network } from '@tatumio/tatum'

const tatum = await TatumSDK.init<Tezos>({ network: Network.TEZOS })

const response = await tatum.rpc.setBootstrappedFlag({ chainId: 'main' })

tatum.destroy() // Destroy Tatum SDK - needed for stopping background jobs
```
{% endcode %}
{% endtab %}
{% endtabs %}

### Overview

The `setBootstrappedFlag` method forcefully sets the bootstrapped flag of the node on the Tezos network. This RPC method is essential when needing to manually set a node's bootstrapped status.

### Example use cases:

1. **Node Initialization:** 
   Operators might want to manually set a node's bootstrapped status during initialization or during network resets.
   
2. **Network Monitoring and Maintenance:** 
   In scenarios where automated detection fails, this method provides a manual override to set the node's bootstrapped status.

### Request Parameters

The `patchChains` method requires the following parameter:

- `chainId` (string, required): 
  The chain ID of the Tezos network (e.g., 'main').

### Return Object

The `set_bootstrapped_flag` method typically returns an acknowledgment that the bootstrapped flag has been set. However, the exact structure might vary based on the Tezos node implementation. Here's a generic representation:

- `status` (string): 
  Status message, e.g., "Bootstrapped flag set successfully."