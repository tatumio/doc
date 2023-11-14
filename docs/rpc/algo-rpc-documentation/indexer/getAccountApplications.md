# getAccountApplications

### How to use it

```typescript
// Import required libraries and modules from Tatum SDK
import { TatumSDK, AlgorandIndexer, Network } from '@tatumio/tatum';

// Initialize the Tatum SDK for Algorand
const tatum = await TatumSDK.init<AlgorandIndexer>({ network: Network.ALGORAND_INDEXER });

// Define the input parameters in a single object
const params = {
    accountId: 'ALGORAND_ACCOUNT_ID', // Specify the Algorand account ID for which you want to retrieve created applications.
    applicationId: 123,               // Optional: Specify the application ID (number) for filtering.
    includeAll: true,                // Optional: Include all items, including closed accounts, deleted applications, destroyed assets, opted-out asset holdings, and closed-out application local states (boolean).
    limit: 100,                      // Optional: Maximum number of results to return (number).
    next: 'NEXT_PAGE_TOKEN'          // Optional: The next page of results. Use the next token provided by the previous results (string).
};

// Retrieve created application parameters for the Algorand account
const createdApplications = await tatum.rpc.getAccountApplications(params);

// Log the created application parameters
console.log('Algorand Account Created Applications:', createdApplications);

// Always destroy the Tatum SDK instance when done to stop any background processes
await tatum.destroy();
```

### Overview

The `getAccountApplications` method allows you to retrieve the created application parameters of a specific Algorand account.

### Example Use Cases

1. **Application Parameters**: Developers can use this method to retrieve the parameters of applications created by an Algorand account, including information about specific applications and their details.

### Request Parameters

The `getAccountApplications` method requires the following parameters:

- `accountId` (string, required): Specify the Algorand account ID for which you want to retrieve created application parameters.
- `applicationId` (number, optional): Specify the application ID for filtering the results.
- `includeAll` (boolean, optional): Include all items, including closed accounts, deleted applications, destroyed assets, opted-out asset holdings, and closed-out application local states.
- `limit` (number, optional): Maximum number of results to return.
- `next` (string, optional): The next page of results. Use the next token provided by the previous results.

### Return Object

The method returns an object representing the created application parameters of the specified Algorand account, including information about specific applications and their details. 

Please note that the structure of the returned object may change in different Algorand RPC versions.