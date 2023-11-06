# broadcastTxCommit

### How to use it

```typescript
// Importing Tatum SDK for Beacon Chain
import { TatumSDK, Network, Bnb } from '@tatumio/tatum';

// Initializing SDK for Beacon Chain network
const tatum = await TatumSDK.init<Bnb>({ network: Network.BNB });

// Defining the signed transaction string to broadcast
const signedTx = 'SIGNED_TRANSACTION_STRING';  // Replace with your signed transaction string

// Broadcasting the transaction and waiting for commit
const commitResponse = await tatum.rpc.broadcastTxCommit({ tx: signedTx });
console.log(commitResponse);

// Destroy Tatum SDK - needed for stopping background jobs
tatum.destroy();
```

### Overview

The `broadcastTxCommit` method is used to broadcast a signed transaction to the BNB beacon chain and wait for it to be included in a block (commit). This method provides information about the committed transaction, including its status, block height, and other relevant data.

### Parameters

- `tx` (string, required): The signed transaction string that you want to broadcast.

### Return Object

The method returns a response containing information about the committed transaction. The response includes the following fields:

- `height` (string): The block height at which the transaction was included.
  - Example: `7734637`
  
- `hash` (string): The hash of the committed transaction.
  - Example: `008EA3C57B15E34B045F69DCEB2A5589B979B2B58BA282C15DF2AEA8B441AB6B`

- `check_tx` (object): Additional information related to the check transaction phase.
  - Example: `{ }`

- `deliver_tx` (object): Additional information related to the deliver transaction phase.

(Note: The exact structure of the response may vary based on the BNB beacon chain's implementation and version.)