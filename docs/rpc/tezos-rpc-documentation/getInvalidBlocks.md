# getInvalidBlocks

### How to use it

```typescript
// Import required libraries and modules from Tatum SDK
import { TatumSDK, Tezos, Network } from '@tatumio/tatum';

// Initialize the Tatum SDK for Tezos
const tatum = await TatumSDK.init<Tezos>({ network: Network.TEZOS });

// Fetch the list of invalid blocks for a specific Tezos chain using the listInvalidBlocks method
const invalidBlocks = await tatum.rpc.listInvalidBlocks({
  chainId: 'main'  // Specify the Tezos chain ID (usually 'main' for mainnet)
});

console.log(`The list of invalid blocks:`, invalidBlocks);

// Always destroy the Tatum SDK instance when done to stop any background processes
tatum.destroy();
```

### Overview

The `getInvalidBlocks` method retrieves blocks from a specified chain in Tezos that have been declared invalid. Alongside these blocks, the method provides details on the errors that led to their invalidation.

### Example use cases:

1. **Chain Audit & Monitoring:** 
   By identifying and studying invalid blocks, developers and network monitors can gain insights into potential issues or attacks on the Tezos network.
   
2. **Network Health Analysis:** 
   Regularly checking for invalid blocks can be part of a routine health check of the Tezos blockchain, ensuring the network's integrity and robustness.
   
3. **Error Handling:** 
   For developers building on Tezos, understanding why certain blocks were invalidated can aid in improving their applications and handling potential future errors.

### Request Parameters

The `getInvalidBlocks` method requires:

- `chainId` (string, required): 
  The identifier of the Tezos chain from which the list of invalid blocks is being requested.

### Return Object

The `getInvalidBlocks` method returns an array of objects, where each object provides:

- Block details and the associated errors that led to its invalidation.

