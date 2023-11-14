# isReady

### How to use it

```typescript
// Import required libraries and modules from Tatum SDK
import { TatumSDK, Algorand, Network } from '@tatumio/tatum';

// Initialize the Tatum SDK for Algorand
const tatum = await TatumSDK.init<AlgorandAlgod>({ network: Network.ALGORAND_ALGOD });

// Retrieve the health status of the Algorand node
const readyStatus = await tatum.rpc.isReady();

// Log the health status
console.log('Algorand Node Ready:', readyStatus);

// Always destroy the Tatum SDK instance when done to stop any background processes
tatum.destroy();
```

### Overview

The `isReady` method allows you to check the health status of the Algorand node and confirm if it is fully caught up.

### Example Use Cases

1. **Node Health Check**: Developers can use this method to check if the Algorand node is healthy and fully caught up, ensuring that it is ready to process requests.

### Request Parameters

The `isReady` method does not require any parameters.

### Return Object

The method returns a response indicating the health status of the Algorand node.

Please note that the structure of the returned object may change in different Algorand RPC versions.