# getPendingTransactions

### How to use it

```typescript
// Import required libraries and modules from Tatum SDK
import { TatumSDK, Algorand, Network } from '@tatumio/tatum';

// Initialize the Tatum SDK for Algorand
const tatum = await TatumSDK.init<Algorand>({ network: Network.ALGORAND });

// Define the input parameters in a single object
const params = {
    max: 10,          // Optional: Truncated number of transactions to display. If max=0, returns all pending txns (number).
    format: 'json',   // Optional: Configures whether the response object is JSON or MessagePack encoded (enum: json, msgpack).
};

// Retrieve the list of pending transactions
const pendingTransactions = await tatum.rpc.getPendingTransactions(params);

// Log the pending transactions
console.log('Pending Transactions:', pendingTransactions);

// Always destroy the Tatum SDK instance when done to stop any background processes
tatum.destroy();
```

### Overview

The `getPendingTransactions` method allows you to retrieve the list of unconfirmed transactions currently in the transaction pool.

### Example Use Cases

1. **Monitor Pending Transactions**: Developers can use this method to monitor and retrieve information about pending transactions in the transaction pool.

### Request Parameters

The `getPendingTransactions` method requires the following parameters:

- `max` (number, optional): Truncated number of transactions to display. If max = 0, returns all pending transactions.
- `format` (enum: json, msgpack, optional): Configures whether the response object is JSON or MessagePack encoded. If not provided, defaults to JSON.

### Return Object

The method returns a potentially truncated list of transactions currently in the node's transaction pool. This includes an array of signed transaction objects as they were submitted, along with the total number of transactions in the pool. 

You can compute whether or not the list is truncated if the number of elements in the `top-transactions` array is fewer than `total-transactions`. 

Please note that the structure of the returned object may vary depending on the Algorand RPC version.