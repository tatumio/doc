# blockResult

### How to use it

```typescript
// Importing Tatum SDK for Beacon Chain
import { TatumSDK, Network, Bnb } from '@tatumio/tatum';

// Initializing SDK for Beacon Chain network
const tatum = await TatumSDK.init<Bnb>({ network: Network.BNB });

// Defining the block height parameter for the query
const blockParams = {
  height: YOUR_HEIGHT_VALUE  
};

// Fetching and logging the block result data from the BNB Beacon Chain
const blockResultData = await tatum.rpc.blockResult(blockParams);
console.log(blockResultData);

// Cleaning up resources used by Tatum SDK
tatum.destroy();
```

### Overview

The `blockResult` method is used to fetch the results of transactions in a specified block on the BNB Beacon Chain.

### Parameters

- `height`: (string number, optional) The height of the block you are interested in. If not specified, it will default to the latest block.

### Return Object

The method returns an object containing detailed information about the transactions in the specified block. The exact structure of the returned object can depend on the BNB Beacon Chain's implementation and version. Some of the fields you might see include:

- `block_meta` (object): Metadata about the block.
- `block` (object): Detailed information about the block itself.
- `results` (object): Results of transactions included in the block.
- `validator_updates` (array): Information about any validator updates.
- `consensus_param_updates` (object): Information about any updates to consensus parameters.

(Note: The exact fields in the return object can differ based on the BNB Beacon Chain's implementation and version.)