# getApplication

### How to use it

```typescript
// Import required libraries and modules from Tatum SDK
import { TatumSDK, Algorand, Network } from '@tatumio/tatum';

// Initialize the Tatum SDK for Algorand
const tatum = await TatumSDK.init<Algorand>({ network: Network.ALGORAND });

// Define the input parameters in a single object
const params = {
    applicationId: 123,            // Specify the application ID (number) you want to lookup.
    includeAll: true               // Optional: Include all items, including closed accounts, deleted applications, destroyed assets, opted-out asset holdings, and closed-out application local states (boolean).
};

// Lookup the Algorand application
const applicationInfo = await tatum.rpc.getApplication(params);

// Log the application information
console.log('Algorand Application Information:', applicationInfo);

// Always destroy the Tatum SDK instance when done to stop any background processes
tatum.destroy();
```

### Overview

The `getApplication` method allows you to lookup an Algorand application.

### Example Use Cases

1. **Application Information**: Developers can use this method to retrieve detailed information about a specific Algorand application, including its status and details.

### Request Parameters

The `getApplication` method requires the following parameters:

- `applicationId` (number, required): Specify the application ID you want to lookup.
- `includeAll` (boolean, optional): Include all items, including closed accounts, deleted applications, destroyed assets, opted-out asset holdings, and closed-out application local states.

### Return Object

The method returns an object representing the information about the specified Algorand application, including its status and details. 

Please note that the structure of the returned object may change in different Algorand RPC versions.