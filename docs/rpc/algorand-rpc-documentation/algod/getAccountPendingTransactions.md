# getAccountPendingTransactions

### How to use it

```typescript
// Import required libraries and modules from Tatum SDK
import { TatumSDK, Algorand, Network } from '@tatumio/tatum';

// Initialize the Tatum SDK for Algorand
const tatum = await TatumSDK.init<Algorand>({ network: Network.ALGORAND });

// Define the input parameters in a single object
const params = {
    address: 'PUBLIC_KEY', // Specify the Algorand account address for which you want to retrieve pending transactions.
    max: 10,              // Optional: Truncated number of transactions to display (number).
    format: 'json'        // Optional: Configures whether the response object is JSON or MessagePack encoded (enum: json, msgpack).
};

// Retrieve pending transactions by address for the Algorand account
const pendingTransactions = await tatum.rpc.getAccountPendingTransactions(params);

// Log the pending transactions
console.log('Algorand Pending Transactions:', pendingTransactions);

// Always destroy the Tatum SDK instance when done to stop any background processes
tatum.destroy();
```

### Overview

The `getAccountPendingTransactions` method allows you to retrieve a list of unconfirmed transactions currently in the transaction pool by address.

### Example Use Cases

1. **Pending Transactions**: Developers can use this method to retrieve a list of pending transactions for a specific Algorand account. This can help monitor and manage unconfirmed transactions.

### Request Parameters

The `getAccountPendingTransactions` method requires the following parameters:

- `address` (string, required): Specify the Algorand account address for which you want to retrieve pending transactions.
- `max` (number, optional): Truncated number of transactions to display. If max=0, returns all pending transactions.
- `format` (enum: json, msgpack, optional): Configures whether the response object is JSON or MessagePack encoded. If not provided, defaults to JSON.

### Return Object

The method returns an object representing the pending transactions for the specified Algorand account. It includes the following properties:

- `top-transactions` (array): An array of signed transaction objects.
- `total-transactions` (number): Total number of transactions in the pool.

Please note that the structure of the returned object may change in different Algorand RPC versions.

### Error Response

If there is an error with the request, the method may return an error response with the following properties:

- `message` (string): A message describing the error.

Please note that the error responses may vary depending on the specific error encountered.

