# broadcastTxSync

### How to use it

```typescript
// Importing Tatum SDK for Beacon Chain
import { TatumSDK, Network, Bnb } from '@tatumio/tatum';

// Initializing SDK for Beacon Chain network
const tatum = await TatumSDK.init<Bnb>({ network: Network.BNB });

// Defining the signed transaction string to broadcast
const signedTx = 'SIGNED_TRANSACTION_STRING';  // Replace with your signed transaction string

// Broadcasting the transaction synchronously
const syncResponse = await tatum.rpc.broadcastTxSync({ tx: signedTx });
console.log(syncResponse);

// Destroy Tatum SDK - needed for stopping background jobs
await tatum.destroy();
```

### Overview

The `broadcastTxSync` method is used to broadcast a signed transaction to the BNB beacon chain synchronously.

### Parameters

- `tx` (string, required): The signed transaction string that you want to broadcast.

(Note: The `tx` parameter should contain the signed transaction in the appropriate format for the BNB beacon chain.)

### Return Object

This method returns a JSON-RPC response containing information about the broadcasted transaction. The response includes the following fields:

- `code` (string): The status code of the transaction.
- `data` (string): Additional data related to the transaction.
- `hash` (string): The hash of the broadcasted transaction.
- `log` (string): Transaction log information.

(Note: The exact structure of the response may vary based on the BNB beacon chain's implementation and version.)
