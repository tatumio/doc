# getApplications

### How to use it

```typescript
// Import required libraries and modules from Tatum SDK
import { TatumSDK, AlgorandIndexer, Network } from '@tatumio/tatum';

// Initialize the Tatum SDK for Algorand
const tatum = await TatumSDK.init<AlgorandIndexer>({ network: Network.ALGORAND_INDEXER });

// Define the input parameters as a dictionary object
const params = {
    applicationId: 123, // Application ID (integer).
    creator: 'ALGORAND_ADDRESS', // Filter just applications with the given creator address (string).
    includeAll: true, // Include all items including closed accounts, deleted applications, destroyed assets, opted-out asset holdings, and closed-out application localstates (boolean).
    limit: 10, // Maximum number of results to return (integer).
    next: 'NEXT_TOKEN', // The next page of results. Use the next token provided by the previous results (string).
};

// Search for applications
const applications = await tatum.indexer.getApplications(params);

// Log the applications
console.log('Applications:', applications);

// Always destroy the Tatum SDK instance when done to stop any background processes
tatum.destroy();
```

### Overview

The `getApplications` method allows you to search for applications on the Algorand network using various filtering criteria. You can filter applications by their Application ID, creator address, and more.

### Request Parameters

The `getApplications` method requires the following parameters:

- `applicationId` (integer, optional): Application ID used to filter applications.

- `creator` (string, optional): Filter applications by the creator's address.

- `includeAll` (boolean, optional): Whether to include all items, including closed accounts, deleted applications, destroyed assets, opted-out asset holdings, and closed-out application localstates.

- `limit` (integer, optional): Maximum number of results to return. Additional pages may be available even if the limit is not reached.

- `next` (string, optional): The next page token to use for pagination. Provide this token when making another request to retrieve the next set of results.

### Return Object

The method returns a response object containing information about the applications:

- `applications` (array of objects): An array of application objects that match the search criteria.

- `current-round` (integer): The round at which the results were computed.

- `next-token` (string): Used for pagination. When making another request, provide this token with the `next` parameter to retrieve the next set of results.

Please note that the structure of the returned object may change in different Algorand Indexer API versions.