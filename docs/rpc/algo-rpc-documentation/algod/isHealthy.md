# isHealthy

### How to use it

```typescript
// Import required libraries and modules from Tatum SDK
import { TatumSDK, Algorand, Network } from '@tatumio/tatum';

// Initialize the Tatum SDK for Algorand
const tatum = await TatumSDK.init<Algorand>({ network: Network.ALGORAND_ALGOD });

// Retrieve health check status for the Algorand node
const isHealthy = await tatum.rpc.isHealthy();

// Log the health check status
console.log('Algorand Health Check:', isHealthy);

// Always destroy the Tatum SDK instance when done to stop any background processes
tatum.destroy();
```

### Overview

The `isHealthy` method allows you to check the health of the Algorand node.

### Example Use Cases

1. **Health Monitoring**: Developers can use this method to regularly monitor the health status of the Algorand node and ensure that it is functioning properly.

### Request Parameters

The `isHealthy` method does not require any parameters.

### Return Object

The method returns an empty object with a response code indicating the health status of the Algorand node.
