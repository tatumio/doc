# getBlockHash

### How to use it

```typescript
// Import required libraries and modules from Tatum SDK
import { TatumSDK, Algorand, Network } from '@tatumio/tatum';

// Initialize the Tatum SDK for Algorand
const tatum = await TatumSDK.init<AlgorandAlgod>({ network: Network.ALGORAND_ALGOD });

// Define the input parameters in a single object
const params = {
    round: 12345,  // Specify the round from which you want to fetch block hash information (integer).
};

// Get the block hash for the specified round
const blockHash = await tatum.rpc.getBlockHash(params);

// Log the block hash
console.log('Block Hash:', blockHash);

// Always destroy the Tatum SDK instance when done to stop any background processes
tatum.destroy();
```

### Overview

The `getBlockHash` method allows you to fetch the block hash information for a specific block on the Algorand blockchain.

### Example Use Cases

1. **Retrieve Block Hash**: Developers can use this method to fetch the block hash for a specific block on the Algorand blockchain.

### Request Parameters

The `getBlockHash` method requires the following parameter:

- `round` (integer, required): Specify the round from which you want to fetch block hash information.

### Return Object

The method returns an object representing the block hash of the specified round on the Algorand blockchain.

Please note that the structure of the returned object may change in different Algorand RPC versions.