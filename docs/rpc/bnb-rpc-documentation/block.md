# block

### How to use it

```typescript
// Importing Tatum SDK for Beacon Chain
import { TatumSDK, Network, Bnb } from '@tatumio/tatum';

// Initializing SDK for Beacon Chain network
const tatum = await TatumSDK.init<Bnb>({ network: Network.BNB });

// Defining the parameters for fetching a specific block from the blockchain
const blockParams = {
  height: YOUR_HEIGHT_VALUE
};

// Fetching the block data using the 'block' method and the defined parameters
const blockData = await tatum.rpc.block(blockParams);

console.log(blockData);

// Destroying the Tatum SDK instance to stop any background jobs and free up resources
tatum.destroy();

```

### Overview

The `block` method is utilized to fetch block details for a specific height from the BNB Beacon Chain. Without specific block `height`, method returns last known block.

### Parameters

- `height` (string number, optional): The height of the block to be fetched. This is a optional parameter.

### Return Object

The `block` method returns an object containing the details of the block at the specified height. While the exact structure might vary, the return object may include fields like:

- `header` (object): Information about the block header.
- `transactions` (array): List of transactions within the block.
- `blockHash` (string): Hash of the block.
- ... and other details depending on the BNB Beacon Chain's implementation and version.

(Note: The exact fields in the return object might vary based on the BNB Beacon Chain's implementation and version.)
