# getApplicationBox

### How to use it

```typescript
// Import required libraries and modules from Tatum SDK
import { TatumSDK, AlgorandAlgod, Network } from '@tatumio/tatum';

// Initialize the Tatum SDK for Algorand
const tatum = await TatumSDK.init<AlgorandAlgod>({ network: Network.ALGORAND_ALGOD });

// Define the input parameters in a single object
const params = {
    applicationId: 123,    // Specify the application ID for which you want to get the box information (number).
    name: 'BOX_NAME'      // Specify the box name you want to get the information for (string).
};

// Get the box information for the given application and box name
const boxInfo = await tatum.rpc.getApplicationBox(params);

// Log the box information
console.log('Box Information:', boxInfo);

// Always destroy the Tatum SDK instance when done to stop any background processes
tatum.destroy();
```

### Overview

The `getApplicationBox` method allows you to retrieve information about a specific box in an Algorand application.

### Example Use Cases

1. **Box Information**: Developers can use this method to retrieve information about a specific box in an Algorand application, including the round, box name, and value (each base64 encoded).

### Request Parameters

The `getApplicationBox` method requires the following parameters:

- `applicationId` (number, required): Specify the application ID for which you want to get the box information.
- `name` (string, required): Specify the box name you want to get the information for. Box names must be in the goal app call arg encoding form 'encoding:value'. For ints, use the form 'int:1234'. For raw bytes, use the form 'b64:A=='. For printable strings, use the form 'str:hello'. For addresses, use the form 'addr:XYZ...'.

### Return Object

The method returns an object representing the box information for the specified application and box name. The returned object includes the round, box name, and value (each base64 encoded).

Please note that the structure of the returned object may change in different Algorand RPC versions.