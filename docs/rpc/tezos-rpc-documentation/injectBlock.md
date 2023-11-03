# injectBlock

### How to use it

```typescript
// Import required libraries and modules from Tatum SDK
import { TatumSDK, Tezos, Network } from '@tatumio/tatum';

// Initialize the Tatum SDK for Tezos
const tatum = await TatumSDK.init<Tezos>({ network: Network.TEZOS });

// Define the block data and operations
const blockData = {
    async: false,                 // Optional: Set to 'true' for asynchronous injection
    force: false,                // Optional: Set to 'true' to inject even on non-strictly increasing fitness
    chain: 'main',                // Optional: Specify the chain identifier (Replace with 'test' for test chain)
    data: 'YOUR_BLOCK_DATA',      // Replace with the block data as a string
    operations: [
        // Define your operations here as an array
        // Example:
        [
            {
                // Define the operation details here
            }
        ]
    ]
};

// Inject a block in the node and broadcast it
const blockId = await tatum.rpc.injectBlock(blockData);

// Log the block ID
console.log('Block ID:', blockId);

// Always destroy the Tatum SDK instance when done to stop any background processes
tatum.destroy();
```

### Overview

The `injectBlock` method allows you to inject a block into the Tezos node and broadcast it. You can embed operations within the `blockData` parameter, which may be pre-validated using contextual RPCs from the latest block. This method returns the ID of the injected block. By default, the RPC waits for the block to be validated before responding. You can set the `async` parameter to 'true' for an immediate response. Additionally, you can use the `force` parameter to inject the block even on non-strictly increasing fitness. An optional `chain` parameter allows you to specify whether to inject on the main chain or the test chain.

### Example Use Cases

1. **Broadcast Custom Blocks:**
   Developers can use this method to inject custom blocks into the Tezos network. This is useful for testing and development purposes, as well as for broadcasting custom transactions.

2. **Advanced Testing:**
   Test scenarios that involve specific block conditions or custom data can be simulated and injected into the Tezos network for validation.

3. **Custom Operation Injections:**
   When working with custom smart contracts or complex transactions, you can create custom blocks with specific operations and inject them using this method.

### Request Parameters

The `injectBlock` method accepts the following parameters:

- `data` (string, required): 
  The block data as a string.

- `operations` (array, required): 
  An array of operations to be included in the block. Each operation should be an array with the operation details.

- `async` (boolean, optional): 
Set to 'true' to receive an asynchronous response. Default is 'false'.

- `force` (boolean, optional): 
  Set to 'true' to inject the block even on non-strictly increasing fitness. Default is 'false'.

- `chain` (string, optional): 
  The chain identifier, which can be a chain hash in Base58Check notation or one of the predefined aliases: 'main' or 'test'. Default is 'main'.

### Return Object

The `injectBlock` method returns an object containing the ID of the injected block:

- `blockId` (string): 
  A block identifier in Base58Check-encoded format.

(Note: The exact fields in the return object might vary based on the Tezos blockchain's implementation and version.)