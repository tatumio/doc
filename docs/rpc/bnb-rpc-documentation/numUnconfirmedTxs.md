# numUnconfirmedTxs

### How to Use It

```typescript
// Importing Tatum SDK for BNB Beacon Chain
import { TatumSDK, Network, Bnb } from '@tatumio/tatum';

// Initializing SDK for BNB Beacon Chain network
const tatum = await TatumSDK.init<Bnb>({ network: Network.BNB });

// Retrieve the number of unconfirmed transactions
const numUnconfirmedTxs = await tatum.rpc.numUnconfirmedTxs();
console.log(numUnconfirmedTxs);

// Destroy Tatum SDK - needed for stopping background jobs
await tatum.destroy();
```

### Overview

The `numUnconfirmedTxs` method is used to retrieve the number of unconfirmed transactions in the BNB Beacon Chain.

### Parameters

This method does not require any parameters.

### Return Object

The method returns a Promise that resolves to a JSON-RPC response containing the following fields:

- `n_txs` (string): The number of unconfirmed transactions. Example: `0`
- `total` (string): The total value associated with unconfirmed transactions. Example: `0`
- `total_bytes` (string): The total size in bytes of unconfirmed transactions. Example: `0`

(Note: The exact fields in the return object might vary based on the BNB Beacon Chain's implementation and version.)