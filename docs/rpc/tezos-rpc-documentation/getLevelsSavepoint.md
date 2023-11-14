# getLevelsSavepoint

### How to use it 

```typescript
// Import required libraries and modules from Tatum SDK
import { TatumSDK, Tezos, Network } from '@tatumio/tatum';

// Initialize the Tatum SDK for Tezos
const tatum = await TatumSDK.init<Tezos>({ network: Network.TEZOS });

// Define the chain ID (For this example, we use "NetXdQprcVkpaWU" as a placeholder)
const chainId = { chainId: 'NetXdQprcVkpaWU' };

// Fetch a list of savepoint levels for the specified chain
const savepointLevels = await tatum.rpc.getLevelsSavepoint(chainId);

// Log the list of savepoint levels
console.log('Savepoint levels:', savepointLevels);

// Always destroy the Tatum SDK instance when done to stop any background processes
await tatum.destroy();
```

### Overview

The `getLevelsSavepoint` method allows you to retrieve a list of savepoint levels for a specific chain in the Tezos network. Savepoints are specific levels in the blockchain's history that can be used for various purposes, such as optimizing synchronization or rolling back to a specific point.

### Example use cases:

1. **Blockchain Optimization:**
   Node operators and developers can use this method to obtain a list of savepoint levels to optimize their Tezos node's synchronization process by starting from a known savepoint.

2. **Rollback Capability:**
   Savepoints provide the ability to roll back the blockchain to a specific point in time. This can be helpful for handling issues or anomalies by reverting to a previous state.

3. **Historical Data Retrieval:**
   Researchers and analysts may use savepoints to fetch historical data for analysis and research purposes, ensuring consistent and accurate data retrieval.

### Request Parameters

The `getLevelsSavepoint` method requires the following parameter:

- `chainId` (string, required): 
  The identifier of the Tezos chain for which to retrieve the savepoint levels.

### Return Object

The `getLevelsSavepoint` method returns an array of savepoint level objects, each containing relevant information about the savepoint level:

- `block_hash` (string): The hash of the block at the savepoint level, e.g., "BLockGenesisGenesisGenesisGenesisGenesisf79b5d1CoW2".
- `level` (integer): The level (block number) of the savepoint, e.g., 0.

(Note: The exact fields in the return object might vary based on the Tezos blockchain's implementation and version.)