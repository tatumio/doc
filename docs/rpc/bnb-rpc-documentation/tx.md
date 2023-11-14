# tx

### How to use it

```typescript
// Importing Tatum SDK for Beacon Chain
import { TatumSDK, Network, Bnb } from '@tatumio/tatum';

// Initializing SDK for Beacon Chain network
const tatum = await TatumSDK.init<Bnb>({ network: Network.BNB });

// Defining the transaction hash parameter for the query
const txParams = {
  hash: 'YOUR_TRANSACTION_HASH',  // e.g., "0x1234abcd..."
};

// Fetching transaction information by hash
const txData = await tatum.rpc.tx(txParams);
console.log(txData);

// Destroy Tatum SDK - needed for stopping background jobs
await tatum.destroy();
```

### Overview

The `tx` method is used to retrieve detailed information about a specific transaction on the BNB Beacon Chain using the transaction's hash.

### Parameters

- `hash` (string, required): The hash of the transaction you want to retrieve information about.

### Return Object

This method returns an object containing detailed information about the specified transaction, including the transaction's hash, block height, and other relevant data.

(Note: The exact fields in the return object might vary based on the BNB Beacon Chain's implementation and version.)
