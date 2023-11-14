# getTransactionById

### How to use it

```typescript
// Import required libraries and modules from Tatum SDK
import { TatumSDK, Algorand, Network } from '@tatumio/tatum';

// Initialize the Tatum SDK
const tatum = await TatumSDK.init<AlgorandIndexer>({ network: Network.ALGORAND_INDEXER });

// Define the input parameters as a dictionary object
const txId = { txId : 'TRANSACTION_ID'}; // Specify the transaction ID you want to lookup (string).

// Lookup a single transaction by its ID
const transaction = await tatum.rpc.getTransactionById(txId);

// Log the transaction information
console.log('Transaction Information:', transaction);

// Always destroy the Tatum SDK instance when done to stop any background processes
tatum.destroy();
```

### Overview

The `getTransactionById` method allows you to lookup a single transaction by its unique transaction ID.

### Request Parameters

The method requires the following parameter:

- `txId` (string, required): Specify the transaction ID you want to lookup.

### Return Object

The method returns information about the specified transaction, including details such as the transaction's ID, sender address, receiver address, transaction type, amount, and more.

Please note that the structure of the returned object may change in different RPC versions.