# getAccountPayments

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
    join: true, 
};

// Retrieve successful payments for a given account
const payments = await tatum.rpc.getAccountPayments(params);

// Log the list of payments
console.log('Account Payments:', payments);

// Always destroy the Tatum SDK instance when done to stop any background processes
await tatum.destroy();
```

## Overview

The `getAccountPayments` method allows you to retrieve successful payments for a given account on the Stellar blockchain. You can use this endpoint in streaming mode to listen for new payments for the specified account as they are added to the Stellar ledger. When called in streaming mode, Horizon will start at the earliest known payment unless a cursor is set, in which case it will start from that cursor. Setting the cursor value to 'now' allows you to stream payments created since your request time.

## Request Parameters

The `getAccountPayments` method accepts the following request parameters:

- `accountId` (string, required): 
  The unique identifier (account ID) of the account for which you want to retrieve payments.

- `cursor` (string, optional): 
  A cursor value that determines the starting point for retrieving payments. Set it to 'now' to stream payments created since your request time.

- `order` (string, optional): 
  A designation of the order in which records should appear. Options include 'asc' (ascending) or 'desc' (descending). If this argument isn’t set, it defaults to 'asc'.

- `limit` (number, optional): 
  The maximum number of records returned. It defines the number of payments to fetch in a single request.

- `includeFailed` (boolean, optional): 
  A flag to indicate whether to include failed payments in the results. Set to `true` to include failed payments.

- `join` (string, optional): 
  Set this parameter to "transactions" in the query to include the transactions which created each of the operations in the response. It is not required and is used to enrich the response with transaction details pertinent to the operations.

## Return Object

The `getAccountPayments` method returns a JSON object containing the list of payments associated with the specified account. Each payment includes details such as its source, destination, amount, and other relevant information.

(Note: The exact fields in the return object might vary based on the Stellar blockchain's implementation and version.)
