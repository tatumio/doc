# getTransactions

### How to use it

```typescript
// Import required libraries and modules from Tatum SDK
import { TatumSDK, Algorand, Network } from '@tatumio/tatum';

// Initialize the Tatum SDK
const tatum = await TatumSDK.init<Algorand>({ network: Network.ALGORAND_INDEXER });

// Define the input parameters as a dictionary object
const params = {
    address: 'ALGORAND_ADDRESS',    // Optional: Only include transactions with this address in one of the transaction fields (string).
    addressRole: 'sender',          // Optional: Combine with the address parameter to define what type of address to search for (enum: sender, receiver, freeze-target).
    afterTime: '2023-11-06T00:00:00Z', // Optional: Include results after the given time (RFC 3339 formatted string).
    applicationId: 123,             // Optional: Application ID (integer).
    assetId: 456,                   // Optional: Asset ID (integer).
    beforeTime: '2023-11-07T00:00:00Z', // Optional: Include results before the given time (RFC 3339 formatted string).
    currencyGreaterThan: 100,       // Optional: Results should have an amount greater than this value (number).
    currencyLessThan: 500,          // Optional: Results should have an amount less than this value (number).
    excludeCloseTo: true,           // Optional: Combine with address and address-role parameters to define what type of address to search for (boolean).
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

// Search for transactions based on the specified parameters
const transactions = await tatum.rpc.getTransactions(params);

// Log the list of transactions that match the criteria
console.log('Transactions:', transactions);

// Always destroy the Tatum SDK instance when done to stop any background processes
tatum.destroy();
```

### Overview

The `getTransactions` method allows you to search for transactions based on various criteria. Transactions can be filtered by address, address role, time, application ID, asset ID, currency amount, and more. By default, transactions are returned in chronological order from oldest to newest, but you can reverse the order using the `address` parameter.

### Request Parameters

The method requires the following parameters:

- `address` (string, optional): Only include transactions with this address in one of the transaction fields.
- `addressRole` (enum, optional): Combine with the address parameter to define what type of address to search for (sender, receiver, freeze-target).
- `afterTime` (string, optional): Include results after the given time (RFC 3339 formatted string).
- `applicationId` (integer, optional): Application ID for filtering transactions.
- `assetId` (integer, optional): Asset ID for filtering transactions.
- `beforeTime` (string, optional): Include results before the given time (RFC 3339 formatted string).
- `currencyGreaterThan` (number, optional): Results should have an amount greater than this value.
- `currencyLessThan` (number, optional): Results should have an amount less than this value.
- `excludeCloseTo` (boolean, optional): Combine with address and address-role parameters to define what type of address to search for.
- `limit` (number, optional): Maximum number of results to return.
- `maxRound` (number, optional): Include results at or before the specified max-round.
- `minRound` (number, optional): Include results at or after the specified min-round.
- `next` (string, optional): The next page of results. Use the next token provided by the previous results.
- `notePrefix` (string, optional): Specifies a prefix that must be contained in the note field.
- `rekeyTo` (boolean, optional): Include results which include the rekey-to field.
- `round` (number, optional): Include results for the specified round.
- `sigType` (enum, optional): Filter results using the specified type of signature (sig, msig, lsig).
- `txType` (enum, optional): Filter results by transaction type (pay, keyreg, acfg, axfer, afrz, appl, stpf).
- `txId` (string, optional): Lookup the specific transaction by ID.

### Return Object

The method returns a list of transactions that match the specified criteria. Transactions include details such as transaction ID, sender address, receiver address, transaction type, and more. The order of results can be reversed based on the `address` parameter.

Please note that the structure of the returned object may change in different RPC versions.