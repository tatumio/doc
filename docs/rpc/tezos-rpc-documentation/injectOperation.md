# injectOperation

### How to use it

```typescript code example
// Import required libraries and modules from Tatum SDK
import { TatumSDK, Tezos, Network } from '@tatumio/tatum';

// Initialize the Tatum SDK for Tezos
const tatum = await TatumSDK.init<Tezos>({ network: Network.TEZOS });

// Define the parameters for injecting an operation (Replace placeholders with actual values)
const params = {
    operationBytes: 'OUR_SIGNED_OPERATION_CONTENTS'     // Required: peration contents as a string
    async: false,                 // Optional: Set to 'true' for asynchronous injection
    chain: 'main'                // Optional: Specify the chain identifier (Replace with 'test' for test chain)
};

// Inject an operation into the node and broadcast it
const operationId = await tatum.rpc.injectOperation(params);

// Log the operation ID
console.log('Operation ID:', operationId);

// Always destroy the Tatum SDK instance when done to stop any background processes
await tatum.destroy();
```

### Overview

The `injectOperation` method allows you to inject an operation into the Tezos node and broadcast it. You should construct the `operationBytes` using contextual RPCs from the latest block and sign it with your client. The injection of the operation applies it to the current mempool context, which may change with each operation injection or reception from peers. By default, the RPC waits for the operation to be (pre-)validated before returning. However, setting `async` to 'true' makes the function return immediately. The optional `chain` parameter specifies whether to inject on the main chain or the test chain.

### Example Use Cases

1. **Broadcast Custom Operations:**
   Developers can use this method to inject custom operations, such as transactions or smart contract interactions, into the Tezos network.

2. **Transaction Signing and Injection:**
   When building applications that require transaction signing, this method allows you to sign and inject transactions seamlessly.

3. **Blockchain Integration:**
   Service providers and blockchain integrators can use this method to facilitate the broadcast of operations from external systems.

### Request Parameters

The `injectOperation` method accepts the following parameters:

- `async` (boolean, optional): 
  Set to 'true' to receive an asynchronous response. Default is 'false'.

- `chain` (string, optional): 
  The chain identifier, which can be a chain hash in Base58Check notation or one of the predefined aliases: 'main' or 'test'. Default is 'main'.

- `operationBytes` (string, required): 
  The signed operation contents as a string, constructed using contextual RPCs from the latest block and signed by the client.

### Request Body

The request body for `injectOperation` should be a string containing the signed operation contents.

### Return Object

The `injectOperation` method returns an object containing the ID of the injected operation:

- `operationId` (string): 
  A Tezos operation ID in Base58Check-encoded format.

(Note: The exact fields in the return object might vary based on the Tezos blockchain's implementation and version.)