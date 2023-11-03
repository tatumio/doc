# getHistoryMode

### How to use it

```typescript
// Import required libraries and modules from Tatum SDK
import { TatumSDK, Tezos, Network } from '@tatumio/tatum';

// Initialize the Tatum SDK for Tezos
const tatum = await TatumSDK.init<Tezos>({ network: Network.TEZOS });

// Fetch the history mode of the node's underlying storage
const historyMode = await tatum.rpc.getHistoryMode();

// Log the history mode
console.log(`Node's history mode:`, historyMode.historyMode);

// Always destroy the Tatum SDK instance when done to stop any background processes
tatum.destroy();
```

### Overview

The `getHistoryMode` method is utilized to retrieve the history mode of the node's underlying storage in the Tezos network. The history mode determines the extent of the historical data retained by the node, influencing storage requirements, the ability to query historical data, and recovery mechanisms.

### Example use cases:

1. **Storage Optimization:**
   Node operators can use the `getHistoryMode` method to understand the storage mode of their node. Depending on the mode, they might decide to adjust storage resources or transition to a different mode to meet their operational needs.

2. **Data Query and Analytics:**
   Developers and analysts can check the history mode to ensure they can query the historical data they need. For instance, a node in `rolling` mode might not retain the entire history of the blockchain.

3. **Node Configuration and Setup:**
   When setting up new nodes or performing maintenance tasks, operators might need to check the history mode to ensure consistency across different nodes or to optimize for specific use cases.

### Request Parameters

The `getHistoryMode` method doesn't require specific parameters in the request body.

### Return Object

The `getHistoryMode` method returns an object indicating the history mode of the node's underlying storage:

- `historyMode` (string): 
  Can be one of the following values:
  - `archive`: The node retains the entire history of the chain.
  - `full`: The node retains the full history but may prune some data.
  - `rolling`: The node retains only a limited history, maintaining the most recent blocks and pruning older ones.