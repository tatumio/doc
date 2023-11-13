# getApplicationLogs

### How to use it

```typescript
// Import required libraries and modules from Tatum SDK
import { TatumSDK, Algorand, Network } from '@tatumio/tatum';

// Initialize the Tatum SDK for Algorand
const tatum = await TatumSDK.init<Algorand>({ network: Network.ALGORAND_INDEXER });

// Define the input parameters in a single object
const params = {
    applicationId: 123,       // Specify the application ID (number) for which you want to lookup logs.
    limit: 100,               // Optional: Maximum number of results to return (number).
    maxRound: 10000,          // Optional: Include results at or before the specified max-round (number).
    minRound: 9000,           // Optional: Include results at or after the specified min-round (number).
    next: 'NEXT_PAGE_TOKEN',   // Optional: The next page of results. Use the next token provided by the previous results (string).
    senderAddress: 'ALGORAND_SENDER_ADDRESS', // Optional: Only include transactions with this sender address (string).
    txId: 'TRANSACTION_ID'    // Optional: Lookup the specific transaction by ID (string).
};

// Lookup application logs for the Algorand application
const applicationLogs = await tatum.rpc.getApplicationLogs(params);

// Log the application logs
console.log('Algorand Application Logs:', applicationLogs);

// Always destroy the Tatum SDK instance when done to stop any background processes
tatum.destroy();
```

### Overview

The `getApplicationLogs` method allows you to lookup logs for an Algorand application.

### Example Use Cases

1. **Application Logs**: Developers can use this method to retrieve logs associated with a specific Algorand application.

### Request Parameters

The `getApplicationLogs` method requires the following parameters:

- `applicationId` (number, required): Specify the application ID for which you want to lookup logs.
- `limit` (number, optional): Maximum number of results to return.
- `maxRound` (number, optional): Include results at or before the specified max-round.
- `minRound` (number, optional): Include results at or after the specified min-round.
- `next` (string, optional): The next page of results. Use the next token provided by the previous results.
- `senderAddress` (string, optional): Only include transactions with this sender address.
- `txId` (string, optional): Lookup the specific transaction by ID.

### Return Object

The method returns an array of application logs for the specified Algorand application.

Please note that the structure of the returned object may change in different Algorand RPC versions.
