# isBootstrapped

### How to use it

```typescript
// Import required libraries and modules from Tatum SDK
import { TatumSDK, Tezos, Network } from '@tatumio/tatum';

// Initialize the Tatum SDK for Tezos
const tatum = await TatumSDK.init<Tezos>({ network: Network.TEZOS });

// Fetch the bootstrap and synchronization status for a specific Tezos chain
const bootstrapStatus = await tatum.rpc.isBootstrapped({
  chainId: 'NetXdQprcVkpaWU'  // Specify the Tezos chain ID (e.g., 'NetXdQprcVkpaWU' for mainnet)
});

// Log the status results
console.log(`Is the node bootstrapped?`, bootstrapStatus.bootstrapped);
console.log(`Current synchronization state:`, bootstrapStatus.sync_state);

// Always destroy the Tatum SDK instance when done to stop any background processes
tatum.destroy();
```

### Overview

The `isBootstrapped` method is used to retrieve the bootstrap status of a specified chain on the Tezos network. The bootstrap status indicates whether the node has synchronized with the network (i.e., downloaded all blocks up to the network's current state).

### Example use cases:

1. **Network Synchronization Verification:**
   This method is crucial for developers and services to verify whether a node is fully synchronized with the rest of the Tezos network, ensuring that operations and queries are executed based on the latest blockchain state.

2. **Node Setup and Maintenance:**
   During the setup or maintenance of a Tezos node, `isBootstrapped` helps in determining the synchronization status, assisting operators in making informed decisions about starting or resuming services that depend on the node.

3. **Health Checks and Monitoring:**
   Services can regularly poll the bootstrap status of their nodes, enabling timely detection of potential synchronization issues and facilitating continuous monitoring of node health.

### Request Parameters

The `isBootstrapped` method requires the following parameter:

- `chainId` (string, required): 
  The identifier of the Tezos chain for which the bootstrap status is being requested.

### Return Object

The `isBootstrapped` method returns an object containing detailed information regarding the node's bootstrap and synchronization status:

- `bootstrapped` (boolean): 
  Indicates whether the node has completed the bootstrapping process. `true` signifies that the node has bootstrapped, while `false` indicates otherwise.

- `sync_state` (`$chain_status`):
  Provides the current synchronization status of the node in relation to its peers. The possible values for `$chain_status` are:
  - `stuck`: The node considers itself synchronized with its peers, but from its perspective, the chain seems halted.
  - `synced`: The node believes it is in sync with its peers and its current head timestamp is recent.
  - `unsynced`: The node is not currently synchronized with any of its peers, likely because it is still in the bootstrapping phase and its head is lagging behind the chain's current state.

  (Note: The exact fields in the return object might vary based on the Tezos blockchain's implementation and version.)