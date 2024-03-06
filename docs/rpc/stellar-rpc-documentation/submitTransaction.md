# submitTransaction

### How to use it

```typescript
// Import required libraries and modules from Tatum SDK
import { TatumSDK, Stellar, Network } from "@tatumio/tatum";

// Initialize the Tatum SDK for Stellar
const tatum = await TatumSDK.init<Stellar>({ network: Network.STELLAR });

// Define parameters (Replace placeholders with actual values and remove redundant)
const tx = "BASE64_ENCODED_TRANSACTION_XDR";

// Submit a transaction
const result = await tatum.rpc.submitTransaction(tx);

// Always destroy the Tatum SDK instance when done to stop any background processes
await tatum.destroy();
```

### Overview

The `submitTransaction` method allows you to submit a transaction to the Stellar network. It takes a single, required parameter, which is the base64-encoded XDR of the transaction. If you submit a transaction that has already been included in a ledger, this endpoint will return the same response as would have been returned for the original transaction submission. This allows for safe resubmission of transactions in error scenarios, as highlighted in the error-handling guide.

### Example use cases:

1. **Transaction Submission:**
   Developers and applications can use this method to submit transactions to the Stellar network.

### Request Parameters

The `submitTransaction` method accepts the following parameters:

- `tx` (string, required):
  The base64-encoded XDR of the transaction to be submitted.

### Response Object

The `submitTransaction` method returns the result of the transaction submission. The exact response object may vary based on the Stellar blockchain's implementation and version.
