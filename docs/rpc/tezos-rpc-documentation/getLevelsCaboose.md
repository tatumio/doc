# getLevelsCaboose

### How to use it

```typescript
// Import required libraries and modules from Tatum SDK
import { TatumSDK, Tezos, Network } from '@tatumio/tatum';

// Initialize the Tatum SDK for Tezos
const tatum = await TatumSDK.init<Tezos>({ network: Network.TEZOS });

// Fetch the caboose level for a specific Tezos chain
const cabooseLevel = await tatum.rpc.getLevelsCaboose({
  chainId: 'NetXdQprcVkpaWU'  // Specify the Tezos chain ID (e.g., 'NetXdQprcVkpaWU' for mainnet)
});

// Log the caboose level
console.log(`Current caboose level:`, cabooseLevel.level);

// Always destroy the Tatum SDK instance when done to stop any background processes
tatum.destroy();
```

### Overview

The `getLevelsCaboose` method is used to retrieve the current caboose level of a specified chain on the Tezos network. The caboose is the earliest block still retained in the chain's rolling history, meaning it represents the oldest block in the chain's limited history when running in `rolling` mode.

### Example use cases:

1. **Monitoring Chain History:**
   Developers and node operators can use the `getLevelsCaboose` method to monitor the extent of the rolling history maintained by their node, especially when running in `rolling` mode.

2. **Data Pruning Decisions:**
   By understanding the current caboose level, services can make informed decisions about pruning or archiving historical blockchain data that falls outside the rolling history.

3. **Synchronization and Backup:**
   Node operators might use the caboose level to synchronize or backup specific segments of the blockchain, ensuring they retain the desired portion of the chain's history.

### Request Parameters

The `getLevelsCaboose` method requires the following parameter:

- `chainId` (string, required): 
  The identifier of the Tezos chain for which the caboose level is being requested.

### Return Object

The `getLevelsCaboose` method returns an object containing the specific level number of the caboose:

- `level` (integer): 
  Represents the block number of the current caboose for the specified Tezos chain.