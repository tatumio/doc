# getBlock

### How to use it

```typescript
// Import required libraries and modules from Tatum SDK
import { TatumSDK, AlgorandAlgod, Network } from '@tatumio/tatum';

// Initialize the Tatum SDK for Algorand
const tatum = await TatumSDK.init<AlgorandAlgod>({ network: Network.ALGORAND_ALGOD });

// Define the input parameters in a single object
const params = {
    round: 12345,        // Specify the round from which to fetch block information.
    format: 'json'       // Optional: Configure whether the response object is JSON or MessagePack encoded (enum: json, msgpack).
};

// Retrieve the block for the given round
const block = await tatum.rpc.getBlock(params);

// Log the block
console.log('Algorand Block:', block);

// Always destroy the Tatum SDK instance when done to stop any background processes
await tatum.destroy();
```

### Overview

The `getBlock` method allows you to retrieve the block for the given round in Algorand.

### Request Parameters

The `getBlock` method requires the following parameters:

- `round` (integer, required): Specify the round from which to fetch block information.
- `format` (enum: json, msgpack, optional): Configure whether the response object is JSON or MessagePack encoded. Defaults to JSON if not provided.

### Return Object

The method returns an object representing the block for the given round in Algorand, including block header data and an optional certificate object. 

Please note that the structure of the returned object may change in different Algorand RPC versions.