# getOperation

### How to use it

```typescript
// Import required libraries and modules from Tatum SDK
import { TatumSDK, Stellar, Network } from '@tatumio/tatum';

// Initialize the Tatum SDK for Stellar
const tatum = await TatumSDK.init<Stellar>({ network: Network.STELLAR });

// Define parameters (Replace placeholders with actual values and remove redundant)
const params = {
    operationId: 'OPERATION_ID',
    join: ''
};

// Retrieve information about a specific operation
const operationInfo = await tatum.rpc.getOperation(params);

// Always destroy the Tatum SDK instance when done to stop any background processes
await tatum.destroy();
```

### Overview

The `getOperation` method allows you to retrieve detailed information about a specific operation on the Stellar blockchain by providing the operation's unique identifier.

## Example use cases:

1. **Operation Information Retrieval:**
   Developers and applications can use this method to retrieve detailed information about a specific operation on the Stellar network.

2. **Operation Verification:**
   Users can verify the details of an operation, including its type, source account, destination account, and other relevant information.

### Request Parameters

The `getOperation` method accepts the following parameters:

- `operationId` (string, required):
  The unique identifier of the operation for which you want to retrieve information.

- `join` (string, optional): 
  Set this parameter to "transactions" in the query to include the transactions which created each of the operations in the response. It is not required and is used to enrich the response with transaction details pertinent to the operations.

### Return Object

The `getOperation` method returns detailed information about the specified operation on the Stellar blockchain. The response includes data such as the operation ID, source account, destination account, type of operation, and more.

(Note: The exact fields in the return object might vary based on the Stellar blockchain's implementation and version.)
