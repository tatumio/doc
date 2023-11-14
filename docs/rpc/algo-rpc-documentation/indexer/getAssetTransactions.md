# getAssetTransactions

### How to use it

```typescript
// Import required libraries and modules from Tatum SDK
import { TatumSDK, Algorand, Network } from '@tatumio/tatum';

// Initialize the Tatum SDK
const tatum = await TatumSDK.init<AlgorandIndexer>({ network: Network.ALGORAND_INDEXER });

// Define the input parameters as a dictionary object
const params = {
    assetId: 123,                   // Specify the asset ID (number) for which you want to lookup transactions.
    address: 'ALGORAND_ADDRESS',    // Optional: Include transactions with this address in one of the transaction fields (string).
    addressRole: 'sender',          // Optional: Define what type of address to search for (enum: sender, receiver, freeze-target).
    afterTime: '2023-11-06T00:00:00Z', // Optional: Include results after the given time (RFC 3339 formatted string).
    beforeTime: '2023-11-07T00:00:00Z', // Optional: Include results before the given time (RFC 3339 formatted string).
    currencyGreaterThan: 100,       // Optional: Results should have an amount greater than this value (number).
    currencyLessThan: 500,          // Optional: Results should have an amount less than this value (number).
    excludeCloseTo: true,           // Optional: Exclude close-to addresses when searching for a specific address (boolean).
    limit: 100,                     // Optional: Maximum number of results to return (number).
    maxRound: 1000,                 // Optional: Include results at or before the specified max-round (number).
    minRound: 900,                  // Optional: Include results at or after the specified min-round (number).
    next: 'NEXT_PAGE_TOKEN',        // Optional: The next page of results. Use the next token provided by the previous results (string).
    notePrefix: 'PREFIX_TEXT',      // Optional: Specify a prefix that must be contained in the note field (string).
    rekeyTo: true,                  // Optional: Include results which include the rekey-to field (boolean).
    round: 1000,                    // Optional: Include results for the specified round (number).
    sigType: 'sig',                 // Optional: Filter results using the specified type of signature (enum: sig, msig, lsig).
    txType: 'pay',                  // Optional: Filter results by transaction type (enum: pay, keyreg, acfg, axfer, afrz, appl, stpf).
    txId: 'TRANSACTION_ID'          // Optional: Lookup the specific transaction by ID (string).
};

// Lookup transactions for the specified asset
const assetTransactions = await tatum.rpc.getAssetTransactions(params);

// Log the list of transactions related to the asset
console.log('Asset Transactions:', assetTransactions);

// Always destroy the Tatum SDK instance when done to stop any background processes
tatum.destroy();
```

### Overview

The `getAssetTransactions` method allows you to lookup transactions for a specific asset. Transactions are returned in chronological order, from oldest to newest.

### Request Parameters

The method requires the following parameters:

- `assetId` (number, required): Specify the asset ID for which you want to lookup transactions.
- `address` (string, optional): Include transactions with this address in one of the transaction fields.
- `addressRole` (enum, optional): Define what type of address to search for (sender, receiver, freeze-target).
- `afterTime` (string, optional): Include results after the given time (RFC 3339 formatted string).
- `beforeTime` (string, optional): Include results before the given time (RFC 3339 formatted string).
- `currencyGreaterThan` (number, optional): Results should have an amount greater than this value.
- `currencyLessThan` (number, optional): Results should have an amount less than this value.
- `excludeCloseTo` (boolean, optional): Exclude close-to addresses when searching for a specific address.
- `limit` (number, optional): Maximum number of results to return.
- `maxRound` (number, optional): Include results at or before the specified max-round.
- `minRound` (number, optional): Include results at or after the specified min-round.
- `next` (string, optional): The next page of results. Use the next token provided by the previous results.
- `notePrefix` (string, optional): Specify a prefix that must be contained in the note field.
- `rekeyTo` (boolean, optional): Include results which include the rekey-to field.
- `round` (number, optional): Include results for the specified round.
- `sigType` (enum, optional): Filter results using the specified type of signature (

### Return Object

The method returns a list of transactions related to the specified asset. Transactions are returned in chronological order, from oldest to newest. Each transaction in the list includes details such as transaction ID, sender address, receiver address, transaction type, and more. 

Please note that the structure of the returned object may change in different RPC versions.