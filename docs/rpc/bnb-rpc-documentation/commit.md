# commit

### How to use it

```typescript
// Importing Tatum SDK for Beacon Chain
import { TatumSDK, Network, Bnb } from '@tatumio/tatum';

// Initializing SDK for Beacon Chain network
const tatum = await TatumSDK.init<Bnb>({ network: Network.BNB });

// Defining the block height parameter for the query
const commitParams = {
  height: 'YOUR_HEIGHT_VALUE',  // e.g., "12345"
};

// Fetching commit information for the specified block height
const commitData = await tatum.rpc.commit(commitParams);
console.log(commitData);

// Destroy Tatum SDK - needed for stopping background jobs
tatum.destroy();
```

### Overview

The `commit` method is used to retrieve the commit information of a specific block in the BNB Beacon Chain by providing the block height. If no height is provided, it will fetch commit information regarding the latest block.

### Parameters

- `height` (string, optional): The height of the block for which you want to retrieve commit information.

### Return Object

This method returns an object containing commit information for the specified block, including details like commit hash, precommit validators, and more. 

(Note: The exact fields in the return object might vary based on the BNB Beacon Chain's implementation and version.)
