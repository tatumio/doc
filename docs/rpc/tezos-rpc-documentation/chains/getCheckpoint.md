# getCheckpoint

### How to use it

```typescript
// Import required libraries and modules from Tatum SDK
import { TatumSDK, Tezos, Network } from '@tatumio/tatum';

// Initialize the Tatum SDK for Tezos
const tatum = await TatumSDK.init<Tezos>({ network: Network.TEZOS });

// Fetch the checkpoint for a specific Tezos chain using the deprecated getCheckpoint method
const checkpoint = await tatum.rpc.getCheckpoint({
  chainId: 'main'  // Specify the Tezos chain ID (usually 'main' for mainnet)
});

console.log(`The checkpoint for the chain is:`, checkpoint);

// Always destroy the Tatum SDK instance when done to stop any background processes
tatum.destroy();
```

### Overview

**DEPRECATED**: This method is deprecated. It is recommended to use `../levels/{checkpoint, savepoint, caboose, history_mode}` instead. The `getCheckpoint` method provides information about the current checkpoint for a specified chain in Tezos.

### Example use cases:

1. **Legacy System Support:** 
   While this method is deprecated, it may still be relevant for legacy systems or applications that have not transitioned to newer endpoints.
   
2. **Checkpoint Retrieval:** 
   Checkpoints are crucial for validating the blockchain's integrity. The method allows for quick retrieval of the current checkpoint for audit or validation purposes.

### Request Parameters

The `getCheckpoint` method requires:

- `chainId` (string, required): 
  The identifier of the Tezos chain from which the checkpoint information is being requested.

### Return Object

The `getCheckpoint` method returns an object containing details about the current checkpoint for the specified chain.