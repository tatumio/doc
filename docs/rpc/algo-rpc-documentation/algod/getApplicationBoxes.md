# getApplicationBoxes

### How to use it

```typescript
// Import required libraries and modules from Tatum SDK
import { TatumSDK, Algorand, Network } from '@tatumio/tatum';

// Initialize the Tatum SDK for Algorand
const tatum = await TatumSDK.init<AlgorandAlgod>({ network: Network.ALGORAND_ALGOD });

// Define the input parameters in a single object
const params = {
    applicationId: APPLICATION_ID,   // Specify the application ID for which you want to retrieve box names.
    max: 10                         // Optional: Max number of box names to return. If max is not set, or max == 0, returns all box-names (number).
};

// Retrieve box names for the Algorand application
const boxNames = await tatum.rpc.getApplicationBoxes(params);

// Log the box names
console.log('Algorand Application Boxes:', boxNames);

// Always destroy the Tatum SDK instance when done to stop any background processes
tatum.destroy();
```

### Overview

The `getApplicationBoxes` method allows you to retrieve the box names for a specific Algorand application.

### Example Use Cases

1. **Get Box Names**: Developers can use this method to retrieve the box names associated with an Algorand application.

### Request Parameters

The `getApplicationBoxes` method requires the following parameters:

- `applicationId` (integer, required): Specify the application ID for which you want to retrieve box names.
- `max` (integer, optional): Max number of box names to return. If max is not set, or max == 0, returns all box-names.

### Return Object

The method returns an object representing the box names of the specified Algorand application.

Please note that the structure of the returned object may change in different Algorand RPC versions.
