# getBlock

### How to use it

```typescript
// Import required libraries and modules from Tatum SDK
import { TatumSDK, AlgorandIndexer, Network } from '@tatumio/tatum';

// Initialize the Tatum SDK
const tatum = await TatumSDK.init<AlgorandIndexer>({ network: Network.ALGORAND_INDEXER });

// Define the input parameters as a dictionary object
const params = {
    roundNumber: 1000,  // Specify the round number (integer) for which you want to lookup the block.
    headerOnly: true    // Optional: Set to true to retrieve only the block header without transactions (boolean).
};

// Lookup the block for the specified round number
const blockInfo = await tatum.rpc.getBlock(params);

// Log the block information
console.log('Block Information:', blockInfo);

// Always destroy the Tatum SDK instance when done to stop any background processes
await tatum.destroy();
```

### Overview

The `getBlock` method allows you to lookup a block by specifying its round number. You can retrieve both the block header and transactions, or only the block header using the `headerOnly` flag.

### Request Parameters

The method requires the following parameters:

- `roundNumber` (number, required): Specify the round number for which you want to lookup the block.
- `headerOnly` (boolean, optional): Set to true to retrieve only the block header without transactions (boolean).

### Return Object

The method returns information about the specified block, which includes details such as the block's round number, timestamp, previous block ID, seed, transactions, and more. If the `headerOnly` flag is set to true, the returned object will contain only the block header information.

Please note that the structure of the returned object may change in different RPC versions.