# getLedgersEffects

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
};

// Retrieve effects related to a specific ledger
const ledgerEffects = await tatum.rpc.getLedgersEffects(params);

// Always destroy the Tatum SDK instance when done to stop any background processes
await tatum.destroy();
```

### Overview

The `getLedgersEffects` method allows you to retrieve the effects of a specific Stellar ledger.

### Example use cases:

1. **Transaction Analysis:**
   Developers and applications can use this method to analyze the effects related to transactions and operations within a specific ledger.

2. **Transaction Tracking:**
   Tracking and monitoring the effects of operations within a specific ledger for auditing or analysis purposes.

3. **Historical Data Retrieval:**
   Researchers and analysts can retrieve effect-related data for historical analysis and record-keeping.

### Request Parameters

The `getLedgersEffects` method requires the following parameters:

- `sequence` (string, required): 
  The sequence number of the ledger for which you want to retrieve effects.

- `cursor` (string, optional): 
  An optional cursor to start listing effects from a specific point within the ledger.

- `order` (string, optional): 
  An optional parameter to specify the order of listing (asc or desc). If not provided, it defaults to 'asc'.

- `limit` (number, optional): 
  An optional parameter to specify the maximum number of effects to return. The limit can range from 1 to 200.

### Return Object

The `getLedgersEffects` method returns an array of effects related to the specified ledger. Each effect includes details such as the type, account, operation, and more.

(Note: The exact fields in the return object might vary based on the Stellar blockchain's implementation and version.)