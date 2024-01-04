# getAccountOperations

## How to use it

```typescript
// Import required libraries and modules from Tatum SDK
import { TatumSDK, Stellar, Network } from '@tatumio/tatum';

// Initialize the Tatum SDK for Stellar
const tatum = await TatumSDK.init<Stellar>({ network: Network.STELLAR });

// Define input parameters as an object (Replace placeholders with actual values and remove redundant)
const params = {
    accountId: 'YOUR_ACCOUNT_ID', 
    cursor: 'now', 
    order: 'asc', 
    limit: 10, 
    includeFailed: true, 
    join: '', 
};

// Retrieve successful operations for a given account
const operations = await tatum.rpc.getAccountOperations(params);

// Log the list of operations
console.log('Account Operations:', operations);

// Always destroy the Tatum SDK instance when done to stop any background processes
await tatum.destroy();
```

## Overview

The `getAccountOperations` method allows you to retrieve successful operations for a given account on the Stellar blockchain. You can use this endpoint in streaming mode to listen for new operations for the specified account as they are added to the Stellar ledger. When called in streaming mode, Horizon will start at the earliest known operation unless a cursor is set, in which case it will start from that cursor. Setting the cursor value to 'now' allows you to stream operations created since your request time.

## Request Parameters

The `getAccountOperations` method accepts the following request parameters:

- `accountId` (string, required): 
  The unique identifier (account ID) of the account for which you want to retrieve operations.

- `cursor` (string, optional): 
  A cursor value that determines the starting point for retrieving operations. Set it to 'now' to stream operations created since your request time.

- `order` (string, optional): 
  A designation of the order in which records should appear. Options include 'asc' (ascending) or 'desc' (descending). If this argument isn’t set, it defaults to 'asc'.

- `limit` (number, optional): 
  The maximum number of records returned. It defines the number of operations to fetch in a single request.

- `includeFailed` (boolean, optional): 
  A flag to indicate whether to include failed operations in the results. Set to `true` to include failed operations.

- `join` (string, optional): 
  Set this parameter to "transactions" in the query to include the transactions which created each of the operations in the response. It is not required and is used to enrich the response with transaction details pertinent to the operations.


## Return Object

The `getAccountOperations` method returns a JSON object containing the list of operations associated with the specified account. Each operation may represent a variety of actions such as payments, account creations, and more.

(Note: The exact fields in the return object might vary based on the Stellar blockchain's implementation and version.)
