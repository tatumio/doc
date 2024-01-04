# getAccountTransactions

### How to use it

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
    includeFailed: true
};

// Retrieve successful transactions for a given account
const transactions = await tatum.rpc.getAccountTransactions(params);

// Log the list of transactions
console.log('Account Transactions:', transactions);

// Always destroy the Tatum SDK instance when done to stop any background processes
await tatum.destroy();
```

### Overview

The `getAccountTransactions` method allows you to retrieve successful transactions for a given account on the Stellar blockchain. You can use this endpoint in streaming mode to listen for new transactions for the specified account as they are added to the Stellar ledger. When called in streaming mode, Horizon will start at the earliest known transaction unless a cursor is set, in which case it will start from that cursor. Setting the cursor value to 'now' allows you to stream transactions created since your request time.

## Example use cases:

1. **Transaction History:**
   Developers and applications can use this method to retrieve the transaction history for a specific Stellar account.

2. **Real-time Transaction Monitoring:**
   By using streaming mode with the appropriate cursor, you can monitor and react to new transactions in real-time.

### Request Parameters

The `getAccountTransactions` method accepts the following parameters:

- `accountId` (string, required): 
  The unique identifier (account ID) of the account for which you want to retrieve transactions.

- `cursor` (string, optional): 
  A cursor value that determines the starting point for retrieving transactions. Set it to 'now' to stream transactions created since your request time.

- `order` (string, optional): 
  A designation of the order in which records should appear. Options include 'asc' (ascending) or 'desc' (descending). If this argument isn’t set, it defaults to 'asc'.

- `limit` (number, optional): 
  The maximum number of records returned. It defines the number of transactions to fetch in a single request.

- `includeFailed` (boolean, optional): 
  A flag to indicate whether to include failed transactions in the results. Set to `true` to include failed transactions.

### Return Object

The `getAccountTransactions` method returns a JSON object containing the list of transactions associated with the specified account. Each transaction includes details such as its source, destination, amount, and other relevant information.

(Note: The exact fields in the return object might vary based on the Stellar blockchain's implementation and version.)
