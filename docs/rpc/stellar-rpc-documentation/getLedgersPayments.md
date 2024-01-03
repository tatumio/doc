# getLedgersPayments

### How to use it

```typescript
// Import required libraries and modules from Tatum SDK
import { TatumSDK, Stellar, Network } from '@tatumio/tatum';

// Initialize the Tatum SDK for Stellar
const tatum = await TatumSDK.init<Stellar>({ network: Network.STELLAR });

// Define the ledger sequence number and optional parameters (Replace placeholders with actual values)
const params = {
    sequence: 'YOUR_LEDGER_SEQUENCE',
    cursor: 'YOUR_CURSOR',
    order: 'asc',
    limit: 10,
    includeFailed: true
    join: 'inner',
};

// Retrieve payments related to a specific ledger
const ledgerPayments = await tatum.rpc.getLedgersPayments(params);

// Always destroy the Tatum SDK instance when done to stop any background processes
await tatum.destroy();
```


### Overview

The `getLedgersPayments` method allows you to retrieve all payment-related operations in a specific Stellar ledger. This includes operations such as `create_account`, `payment`, `path_payment`, and `account_merge`.

### Example use cases:

1. **Payment Analysis:**
   Developers and applications can use this method to analyze payment-related operations within a specific ledger.

2. **Transaction Tracking:**
   Tracking and monitoring payments made within a specific ledger for auditing or analysis purposes.

3. **Historical Data Retrieval:**
   Researchers and analysts can retrieve payment-related data for historical analysis and record-keeping.

### Request Parameters

The `getLedgersPayments` method requires the following parameters:

- `sequence` (string, required): 
  The sequence number of the ledger for which you want to retrieve payment-related operations.

- `cursor` (string, optional): 
  An optional cursor to start listing payments from a specific point within the ledger.

- `order` (string, optional): 
  An optional parameter to specify the order of listing (asc or desc). If not provided, it defaults to 'asc'.

- `limit` (number, optional): 
  An optional parameter to specify the maximum number of payments to return. The limit can range from 1 to 200.

- `includeFailed` (boolean, optional): 
  An optional parameter to include failed payments in the results (true or false). If not provided, it defaults to 'false'.

- `join` (string, optional): 
  An optional parameter to specify the join type (inner or left). If not provided, it defaults to 'inner'.

### Return Object

The `getLedgersPayments` method returns an array of payment-related operations within the specified ledger. Each operation includes details such as the sender, receiver, asset, amount, and more.

(Note: The exact fields in the return object might vary based on the Stellar blockchain's implementation and version.)