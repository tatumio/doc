# health

### How to Use It

```typescript
// Importing Tatum SDK for Beacon Chain
import { TatumSDK, Network, Bnb } from '@tatumio/tatum';

// Initializing SDK for Beacon Chain network
const tatum = await TatumSDK.init<Bnb>({ network: Network.BNB });

// Check the health status
const healthStatus = await tatum.rpc.health();
console.log(healthStatus);

// Destroy Tatum SDK - needed for stopping background jobs
await tatum.destroy();
```

### Overview

The `health` method is used to check the health status of the Beacon Chain.

### Parameters

This method does not require any parameters.

### Return Object (Required)

The method returns a Promise that resolves to a JSON-RPC response containing information about the health status of the Beacon Chain.

(Note: The exact structure of the transaction objects and response may vary based on the BNB beacon chain's implementation and version.)