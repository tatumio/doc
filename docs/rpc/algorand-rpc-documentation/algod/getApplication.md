# getApplicationInfo

### How to use it

```typescript
// Import required libraries and modules from Tatum SDK
import { TatumSDK, Algorand, Network } from '@tatumio/tatum';

// Initialize the Tatum SDK for Algorand
const tatum = await TatumSDK.init<Algorand>({ network: Network.ALGORAND });

// Define the input parameters in a single object
const params = {
    applicationId: 123  // Specify the application ID for which you want to retrieve information.
};

// Retrieve information about the specified Algorand application
const applicationInfo = await tatum.rpc.getApplication(params);

// Log the application information
console.log('Algorand Application Information:', applicationInfo);

// Always destroy the Tatum SDK instance when done to stop any background processes
tatum.destroy();
```

### Overview

The `getApplication` method allows you to retrieve information about a specific Algorand application, including the creator, approval and clear programs, global and local schemas, and global state.

### Example Use Cases

1. **Application Details**: Developers can use this method to retrieve detailed information about a specific Algorand application, including its creator, approval and clear programs, global and local schemas, and global state.

### Request Parameters

The `getApplication` method requires the following parameter:

- `applicationId` (number, required): An application identifier.

### Return Object

The method returns an object representing the information about the specified Algorand application.

Please note that the structure of the returned object may change in different Algorand RPC versions.