# getBlockHashes

### How to use it

```typescript
// Import required libraries and modules from Tatum SDK
import { TatumSDK, Tezos, Network } from '@tatumio/tatum';

// Initialize the Tatum SDK for Tezos
const tatum = await TatumSDK.init<Tezos>({ network: Network.TEZOS });

// Fetch block hashes from a specific chain in Tezos using the getBlockHashes method
const blockHashes = await tatum.rpc.getBlockHashes({
  chainId: 'main',         // Specify the Tezos chain ID (usually 'main' for mainnet)
  length: 5,               // Optional: Number of predecessor blocks to return
  head: 'BLockHashHere',   // Optional: Specify a block hash to fetch specific fragments of the chain
  minDate: '2023-10-01'    // Optional: Filter out blocks before this date
});

// Always destroy the Tatum SDK instance when done to stop any background processes
tatum.destroy();
```

### Overview

The `getBlockHashes` method retrieves block hashes from a specified chain in Tezos, sorted by decreasing fitness. Without arguments, it returns the head of the chain. Optional arguments enable the return of the list of predecessors of a specified block or set of blocks.

### Example use cases:

1. **Chain Inspection:** 
   Quickly identify and inspect the most recent blocks in the chain by their hash, aiding in network monitoring and analysis.
   
2. **Historical Data Analysis:** 
   Fetch specific sections of the blockchain for in-depth study or to construct a localized view of the chain's history.
   
3. **Data Validation:** 
   Validators and node operators can use this method to cross-check and validate their local chain's state against the broader network.

### Request Parameters

The `getBlockHashes` method supports several optional parameters:

- `chainId` (string, required): 
  The unique identifier of the Tezos chain for which block hashes are being requested.

- `length` (uint, optional): 
  The number of predecessor blocks to return.

- `head` (block_hash, optional): 
  An empty argument requests blocks starting from the current head. Specifying block hashes allows fetching specific fragments of the chain.

- `minDate` (date, optional): 
  Blocks with a timestamp before this date will be filtered out. If `length` is also provided, up to that number of predecessors will be returned regardless of their date.

### Return Object

The `getBlockHashes` method returns an array of block hashes included in the specified chain:

- An array of block hashes, sorted by decreasing fitness.