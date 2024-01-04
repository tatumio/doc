# getLedger

### How to use it

```typescript
// Import required libraries and modules from Tatum SDK
import { TatumSDK, Stellar, Network } from '@tatumio/tatum';

// Initialize the Tatum SDK for Stellar
const tatum = await TatumSDK.init<Stellar>({ network: Network.STELLAR });

// Define the sequence number of the ledger to retrieve (Replace placeholders with actual values and remove redundant)
const sequenceNumber = 'YOUR_SEQUENCE_NUMBER';

// Retrieve information about a specific ledger using its sequence number
const ledgerInfo = await tatum.rpc.getLedger(sequenceNumber);

// Log the ledger information
console.log('Ledger Info:', ledgerInfo);

// Always destroy the Tatum SDK instance when done to stop any background processes
await tatum.destroy();
```

### Overview

The `getLedger` method allows you to retrieve information about a specific ledger on the Stellar blockchain. You can specify the ledger you want to retrieve by providing its sequence number as a parameter.

### Request Parameters

The `getLedger` method requires the following request parameter:

- `sequence` (string, required): 
  The sequence number of the ledger you want to retrieve. This uniquely identifies the ledger you're interested in.

### Return Object

The `getLedger` method returns a JSON object containing information about the specified ledger. The returned object includes various properties describing the ledger's characteristics, such as its sequence number, transaction count, and more.

(Note: The exact fields in the return object might vary based on the Stellar blockchain's implementation and version.)