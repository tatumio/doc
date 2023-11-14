# getApplicationDetails

### How to use it

```typescript
// Import required libraries and modules from Tatum SDK
import { TatumSDK, AlgorandIndexer, Network } from '@tatumio/tatum';

// Initialize the Tatum SDK for Algorand
const tatum = await TatumSDK.init<AlgorandIndexer>({ network: Network.ALGORAND_INDEXER });

// Define the input parameters in a single object
const params = {
    applicationId: 'APPLICATION_ID', // Application ID to filter the applications (number, optional).
    creator: 'CREATOR_ADDRESS',      // Filter applications by the creator address (string, optional).
    includeAll: true,                // Include all items like closed accounts and deleted applications (boolean, optional).
    limit: 100,                      // Maximum number of results to return (number, optional).
    next: 'NEXT_PAGE_TOKEN'          // The next page of results. Use the next token from previous results (string, optional).
};

// Retrieve details of the specified Algorand application
const applicationDetails = await tatum.rpc.getApplicationDetails(params);

// Log the details of the Algorand application
console.log('Algorand Application Details:', applicationDetails);

// Always destroy the Tatum SDK instance when done to stop any background processes
await tatum.destroy();
```

### Overview

The `getApplicationDetails` method fetches details for Algorand applications, with the ability to filter based on the application ID, creator, and other criteria.

### Request Parameters

- `applicationId` (number, optional): Application ID to filter the applications.
- `creator` (string, optional): Filter applications by the creator address.
- `includeAll` (boolean, optional): Include all related items in the results.
- `limit` (number, optional): Maximum number of results to return.
- `next` (string, optional): The next page of results, using the next token from previous results.

### Return Object

The method returns detailed information about the specified Algorand applications based on the provided filters. 

Please note that the structure of the returned object may change in different Algorand RPC versions.