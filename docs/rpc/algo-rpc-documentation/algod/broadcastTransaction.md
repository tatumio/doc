# broadcastTransaction

### How to use it

```typescript
// Import required libraries and modules from Tatum SDK
import { TatumSDK, AlgorandAlgod, Network } from '@tatumio/tatum';

// Initialize the Tatum SDK for Algorand
const tatum = await TatumSDK.init<AlgorandAlgod>({ network: Network.ALGORAND_ALGOD });

// Define the input parameters in a single object
const params = {
    broadcastTransaction: 'RAW_TRANSACTION',  // Specify the byte encoded signed transaction to broadcast to network.
};

// Broadcast raw transaction to Algorand network
const transactionId = await tatum.rpc.broadcastTransaction(params);

// Log the transaction ID
console.log('Algorand Transaction ID:', transactionId);

// Always destroy the Tatum SDK instance when done to stop any background processes
await tatum.destroy();
```

### Overview

The `broadcastTransaction` method allows you to broadcast a raw transaction or transaction group to the Algorand network.

### Example Use Cases

1. **Transaction Broadcasting**: Developers can use this method to directly broadcast a byte encoded signed transaction to the Algorand network for further processing.

### Request Parameters

The `broadcastTransaction` method requires the following parameters:

- `broadcastTransaction` (string, required): The byte encoded signed transaction to broadcast to the Algorand network.

### Return Object

The method returns an object representing the transaction ID of the submitted transaction on the Algorand network.

Please note that the structure of the returned object may change in different Algorand RPC versions.