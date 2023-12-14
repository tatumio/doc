# getLedgersOperations

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
    includeFailed: true,
    join: 'inner',
};

// Retrieve successful operations related to a specific ledger
const ledgerOperations = await tatum.rpc.getLedgersOperations(params);

// Always destroy the Tatum SDK instance when done to stop any background processes
await tatum.destroy();
```

### Overview

The `getLedgersOperations` method allows you to retrieve successful operations in a specific Stellar ledger.

### Example use cases:

1. **Transaction Analysis:**
   Developers and applications can use this method to analyze successful operations within a specific ledger, including operations like payments, account creation, and more.

2. **Transaction Tracking:**
   Tracking and monitoring successful operations made within a specific ledger for auditing or analysis purposes.

3. **Historical Data Retrieval:**
   Researchers and analysts can retrieve operation-related data for historical analysis and record-keeping.

### Request Parameters

The `getLedgersOperations` method requires the following parameters:

- `sequence` (string, required): 
  The sequence number of the ledger for which you want to retrieve successful operations.

- `cursor` (string, optional): 
  An optional cursor to start listing operations from a specific point within the ledger.

- `order` (string, optional): 
  An optional parameter to specify the order of listing (asc or desc). If not provided, it defaults to 'asc'.

- `limit` (number, optional): 
  An optional parameter to specify the maximum number of operations to return. The limit can range from 1 to 200.

- `includeFailed` (boolean, optional): 
  An optional parameter to include failed operations in the results (true or false). If not provided, it defaults to 'false'.

- `join` (string, optional): 
  An optional parameter to specify the join type (inner or left). If not provided, it defaults to 'inner'.

### Return Object

The `getLedgersOperations` method returns an array of successful operations within the specified ledger. Each operation includes details such as the source account, operation type, asset, amount, and more.

(Note: The exact fields in the return object might vary based on the Stellar blockchain's implementation and version.)