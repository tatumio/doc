# genesis

### How to Use It

```typescript
// Importing Tatum SDK for Beacon Chain
import { TatumSDK, Network } from '@tatumio/tatum';

// Initializing SDK for Beacon Chain network
const tatum = await TatumSDK.init({ network: Network.BEACON_CHAIN });

// Retrieve the genesis information
const genesisInfo = await tatum.rpc.genesis();
console.log(genesisInfo);

// Destroy Tatum SDK - needed for stopping background jobs
tatum.destroy();
```

### Overview

The `genesis` method is used to retrieve the genesis information of the Beacon Chain.

### Parameters

This method does not require any parameters.

### Return Object (Required)

The method returns a Promise that resolves to a JSON-RPC response containing the following field:

- `genesis` (object): General information about the Beacon Chain genesis.

(Note: The exact structure of the transaction objects and response may vary based on the BNB beacon chain's implementation and version.)