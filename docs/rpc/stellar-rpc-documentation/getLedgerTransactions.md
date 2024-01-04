# getLedgersTransactions

### How to use it

```typescript
// Import required libraries and modules from Tatum SDK
import { TatumSDK, Stellar, Network } from '@tatumio/tatum';

// Initialize the Tatum SDK for Stellar
const tatum = await TatumSDK.init<Stellar>({ network: Network.STELLAR });

// Define the ledger sequence number and optional parameters (Replace placeholders with actual values and remove redundant)
const params = {
    sequence: 'YOUR_LEDGER_SEQUENCE',
    cursor: 'YOUR_CURSOR',
    order: 'asc',
    limit: 10,
    includeFailed: true
};

// Retrieve transactions for a specific ledger
const ledgerTransactions = await tatum.rpc.getLedgersTransactions(params);

// Log the list of ledger transactions
console.log('Ledger Transactions:', ledgerTransactions);

// Always destroy the Tatum SDK instance when done to stop any background processes
await tatum.destroy();
```

### Overview

The `getLedgersTransactions` method allows you to retrieve a list of successful transactions associated with a specific ledger on the Stellar blockchain. You can specify the ledger's sequence number and use optional parameters to customize the result.

### Request Parameters

The `getLedgersTransactions` method requires the following parameters:

- `sequence` (string, required): 
  Specify the sequence number of the ledger for which you want to retrieve transactions.

- `cursor` (string, optional): 
  Set the cursor to start listing transactions from a specific transaction within the ledger. If not specified, it starts from the beginning.

- `order` (string, optional): 
  Set the order of listing, which can be either 'asc' (ascending) or 'desc' (descending). If not specified, it defaults to 'asc'.

- `limit` (integer, optional): 
  Set the maximum number of transactions to return in a single request. The limit can range from 1 to an upper limit hardcoded in Horizon for performance reasons. If not specified, it defaults to 10.

- `includeFailed` (boolean, optional): 
  Specify whether to include failed transactions in the results. Set to `true` to include failed transactions, or `false` to exclude them. If not specified, it defaults to `false`.

### Return Object

The `getLedgersTransactions` method returns a JSON object representing a list of successful transactions associated with the specified ledger. Each transaction entry includes various properties describing the transaction, such as its transaction hash, source account, operation details, and more.

(Note: The exact fields in the return object might vary based on the Stellar blockchain's implementation and version.)