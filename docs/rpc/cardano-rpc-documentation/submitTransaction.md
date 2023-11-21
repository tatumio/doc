# submitTransaction

### How to use it

```typescript
// Import required libraries and modules from Tatum SDK
import { TatumSDK, CardanoRosetta, Network } from '@tatumio/tatum';

// Initialize the Tatum SDK for Cardano
const tatum = await TatumSDK.init<CardanoRosetta>({ network: Network.CARDANO_ROSETTA });

// Define the input parameters in a single object
const submitRequest = {
    networkIdentifier: {
        blockchain: 'CARDANO',   // Specify the blockchain identifier ('CARDANO' for Cardano).
        network: 'NETWORK_NAME', // Specify the network name.
        subNetworkIdentifier: {
            network: 'SUB_NETWORK_NAME', // Specify the sub-network name (optional).
            metadata: {
                // Optional metadata.
            },
        },
    },
    signedTransaction: 'SIGNED_TRANSACTION', // Specify the signed transaction to submit.
};

// Submit the signed transaction to the network
const transactionResponse = await tatum.rpc.submitTransaction(submitRequest);

// Log the transaction response
console.log('Transaction Response:', transactionResponse);

// Always destroy the Tatum SDK instance when done to stop any background processes
await tatum.destroy();
```

### Overview

The `submitTransaction` method allows you to submit a signed transaction to the Cardano network for processing. After successfully constructing and signing a transaction, you can use this method to broadcast it to the network.

### Example Use Cases

1. **Transaction Submission**: Developers can use this method to submit a signed Cardano transaction to the network for execution. This is the final step in the transaction lifecycle.

### Request Parameters

The `submitTransaction` method requires the following parameters in the request body:

- `networkIdentifier` (object, required): An object containing information about the blockchain network.
  - `blockchain` (string, required): The blockchain identifier, which should be set to 'CARDANO' for Cardano.
  - `network` (string, required): The network name for Cardano.
  - `subNetworkIdentifier` (object, optional): An optional sub-network identifier object.
    - `network` (string, required): The name of the sub-network within Cardano.
    - `metadata` (object, optional): Metadata associated with the sub-network.
- `signedTransaction` (string, required): The signed transaction blob that you want to submit to the Cardano network.

### Return Object

The method returns an object representing the response from the Cardano network after submitting the signed transaction. This response may include details about the transaction's acceptance by the network.

Structure and behavior of this method may vary with different versions of the Cardano service. Always refer to the documentation specific to the version you are using for the most accurate information.