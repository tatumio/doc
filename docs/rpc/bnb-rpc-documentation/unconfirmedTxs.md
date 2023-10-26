# unconfirmedTxs

### How to Use It

```typescript
// Importing Tatum SDK for Beacon Chain
import { TatumSDK, Network, Bnb } from '@tatumio/tatum';

// Initializing SDK for Beacon Chain network
const tatum = await TatumSDK.init<Bnb>({ network: Network.BNB });

// Define the limit for unconfirmed transactions
const limit = { limit : '10' }; 

// Retrieve unconfirmed transactions
const unconfirmedTxs = await tatum.rpc.unconfirmedTxs(limit);
console.log(unconfirmedTxs);

// Destroy Tatum SDK - needed for stopping background jobs
tatum.destroy();
```

### Overview

The `unconfirmedTxs` method is used to retrieve unconfirmed transactions from the BNB Beacon Chain.

### Parameters

- `limit` (string, optional): The maximum number of unconfirmed transactions to retrieve.

### Return Object (Required)

- `n_txs` (number): The number of unconfirmed transactions.
- `total` (number): The total value associated with unconfirmed transactions.
- `total_bytes` (number): The total size in bytes of unconfirmed transactions.
- `txs` (array): An array of unconfirmed transaction objects.

(Note: The exact structure of the transaction objects and response may vary based on the BNB beacon chain's implementation and version.)