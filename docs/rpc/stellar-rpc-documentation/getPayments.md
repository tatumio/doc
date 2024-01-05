# listAllPayments

### How to use it

```typescript
// Import required libraries and modules from Tatum SDK
import { TatumSDK, Stellar, Network } from '@tatumio/tatum';

// Initialize the Tatum SDK for Stellar
const tatum = await TatumSDK.init<Stellar>({ network: Network.STELLAR });

// Define parameters (Replace placeholders with actual values and remove redundant)
const params = {
    cursor: 'YOUR_CURSOR',
    order: 'asc',
    limit: 10,
    includeFailed: true,
    join: ''
};

// List all successful payment-related operations
const allPayments = await tatum.rpc.listAllPayments(params);

// Always destroy the Tatum SDK instance when done to stop any background processes
await tatum.destroy();
```

### Overview

The `listAllPayments` method allows you to list all successful payment-related operations on the Stellar blockchain.

## Example use cases:

1. **Payment Monitoring:**
   Developers and applications can use this method to monitor and retrieve information about all successful payment-related operations on the Stellar network.

2. **Payment Filtering:**
   Platform administrators can filter and search for specific payments based on various criteria, such as cursor, order, and more.

3. **Streaming Payments:**
   Users can use streaming mode to listen for new payments as they are added to the Stellar ledger.

### Request Parameters

The `listAllPayments` method accepts a single `params` object with the following properties:

- `cursor` (string, optional):
  An optional cursor to start listing payments from a specific point.

- `order` (string, optional):
  An optional parameter to specify the order of listing (asc or desc). If not provided, it defaults to 'asc'.

- `limit` (number, optional):
  An optional parameter to specify the maximum number of payments to return. The limit can range from 1 to 200.

- `includeFailed` (boolean, optional):
  An optional parameter to include failed payments. If set to true, failed payments will be included in the results. Defaults to false.

- `join` (string, optional): 
  Set this parameter to "transactions" in the query to include the transactions which created each of the operations in the response. It is not required and is used to enrich the response with transaction details pertinent to the operations.

### Return Object

The `listAllPayments` method returns an array of successful payment-related operations on the Stellar blockchain. Each operation object corresponds to a payment operation, and it contains information such as the operation ID, source account, destination account, amount, asset, and more.

(Note: The exact fields in the return object might vary based on the Stellar blockchain's implementation and version.)
