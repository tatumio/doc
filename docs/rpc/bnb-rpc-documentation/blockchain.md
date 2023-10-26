# blockchain

### How to use it

```typescript
// Importing Tatum SDK for Beacon Chain
import { TatumSDK, Network, Bnb } from '@tatumio/tatum';

// Initializing SDK for Beacon Chain network
const tatum = await TatumSDK.init<Bnb>({ network: Network.BNB });

// Defining the block height range parameters for the query (optional)
const blockchainParams = {
  minHeight: 'YOUR_MIN_HEIGHT_VALUE',  // Optional: e.g., "12345"
  maxHeight: 'YOUR_MAX_HEIGHT_VALUE'   // Optional: e.g., "67890"
};

// Fetching blockchain data within the specified block height range
const blockchainData = await tatum.rpc.blockchain(blockchainParams);
console.log(blockchainData);

// Destroy Tatum SDK - needed for stopping background jobs
tatum.destroy();
```
### Overview

The `blockchain` method is utilized to fetch blockchain data from the BNB Beacon Chain. Users can optionally specify a block height range to filter the results.

### Parameters

- `minHeight` (string, optional): The minimum block height from which to fetch the data. If not provided, there is no lower limit.
- `maxHeight` (string, optional): The maximum block height up to which to fetch the data. If not provided, there is no upper limit.

### Return Object

The `blockchain` method returns an object that provides a snapshot of the blockchain data within the specified block height range. The exact structure of the return object can vary, but it generally includes information related to blocks, transactions, and possibly other blockchain-specific details.

(Note: The exact fields in the return object can differ based on the BNB Beacon Chain's implementation and version.)