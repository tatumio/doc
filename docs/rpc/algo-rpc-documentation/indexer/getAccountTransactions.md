# getAccountTransactions

### How to use it

```typescript
// Import required libraries and modules from Tatum SDK
import { TatumSDK, Algorand, Network } from '@tatumio/tatum';

// Initialize the Tatum SDK for Algorand
const tatum = await TatumSDK.init<AlgorandIndexer>({ network: Network.ALGORAND_INDEXER });

// Define the input parameters in a single object
const params = {
    accountId: 'ALGORAND_ACCOUNT_ID', // Specify the Algorand account ID for which you want to retrieve transactions.
    afterTime: 'RFC3339_DATETIME',   // Optional: Include results after the given time (string in RFC 3339 format).
    assetId: 123,                    // Optional: Specify the asset ID (number) for filtering.
    beforeTime: 'RFC3339_DATETIME',  // Optional: Include results before the given time (string in RFC 3339 format).
    currencyGreaterThan: 1000,       // Optional: Results should have an amount greater than this value (number).
    currencyLessThan: 5000,          // Optional: Results should have an amount less than this value (number).
    limit: 100,                      // Optional: Maximum number of results to return (number).
    maxRound: 10000,                 // Optional: Include results at or before the specified max-round (number).
    minRound: 9000,                  // Optional: Include results at or after the specified min-round (number).
    next: 'NEXT_PAGE_TOKEN',          // Optional: The next page of results. Use the next token provided by the previous results (string).
    notePrefix: 'NOTE_PREFIX',        // Optional: Specifies a prefix which must be contained in the note field (string).
    rekeyTo: true,                   // Optional: Include results which include the rekey-to field (boolean).
    round: 8000,                     // Optional: Include results for the specified round (number).
    sigType: 'sig',                  // Optional: SigType filters just results using the specified type of signature (enum: sig, msig, lsig).
    txType: 'pay',                   // Optional: Filters results by transaction type (enum: pay, keyreg, acfg, axfer, afrz, appl, stpf).
    txId: 'TRANSACTION_ID'            // Optional: Lookup the specific transaction by ID (string).
};

// Retrieve account transactions for the Algorand account
const accountTransactions = await tatum.rpc.getAccountTransactions(params);

// Log the account transactions
console.log('Algorand Account Transactions:', accountTransactions);

// Always destroy the Tatum SDK instance when done to stop any background processes
tatum.destroy();
```

### Overview

The `getAccountTransactions` method allows you to retrieve transactions of a specific Algorand account.

### Example Use Cases

1. **Transaction History**: Developers can use this method to retrieve the transaction history of an Algorand account, including information about specific transactions and their details.

### Request Parameters

The `getAccountTransactions` method requires the following parameters:

- `accountId` (string, required): Specify the Algorand account ID for which you want to retrieve transactions.
- `afterTime` (string in RFC 3339 format, optional): Include results after the given time.
- `assetId` (number, optional): Specify the asset ID for filtering.
- `beforeTime` (string in RFC 3339 format, optional): Include results before the given time.
- `currencyGreaterThan` (number, optional): Results should have an amount greater than this value.
- `currencyLessThan` (number, optional): Results should have an amount less than this value.
- `limit` (number, optional): Maximum number of results to return.
- `maxRound` (number, optional): Include results at or before the specified max-round.
- `minRound` (number, optional): Include results at or after the specified min-round.
- `next` (string, optional): The next page of results. Use the next token provided by the previous results.
- `notePrefix` (string, optional): Specifies a prefix which must be contained in the note field.
- `rekeyTo` (boolean, optional): Include results which include the rekey-to field.
- `round` (number, optional): Include results for the specified round.
- `sigType` (enum: sig, msig, lsig, optional): Filters just results using the specified type of signature.
- `txType` (enum: pay, keyreg, acfg, axfer, afrz, appl, stpf, optional): Filters results by transaction type.
- `txId` (string, optional): Lookup the specific transaction by ID.

### Return Object

The method returns an object representing the transactions of the specified Algorand account, including information about specific transactions and their details. 

Please note that the structure of the returned object may change in different Algorand RPC versions.