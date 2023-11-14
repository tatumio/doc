# genesis

### How to Use It

```typescript
// Importing Tatum SDK for Beacon Chain
import { TatumSDK, Network, Bnb } from '@tatumio/tatum';

// Initializing SDK for Beacon Chain network
const tatum = await TatumSDK.init<Bnb>({ network: Network.BNB });

// Retrieve the genesis information
const genesisInfo = await tatum.rpc.genesis();
console.log(genesisInfo);

// Destroy Tatum SDK - needed for stopping background jobs
await tatum.destroy();
```

### Overview

The `genesis` method is used to retrieve the genesis information of the Beacon Chain.

### Parameters

This method does not require any parameters.

### Return Object (Required)

The method returns a Promise that resolves to a JSON-RPC response containing the following field:

- `genesis` (object): General information about the Beacon Chain genesis.

(Note: The exact fields in the return object might vary based on the BNB Beacon Chain's implementation and version.)