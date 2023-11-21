# getHashOfTransaction

### How to use it

```typescript
// Import required libraries and modules from Tatum SDK
import { TatumSDK, CardanoRosetta, Network } from '@tatumio/tatum';

// Initialize the Tatum SDK for Cardano
const tatum = await TatumSDK.init<CardanoRosetta>({ network: Network.CARDANO_ROSETTA });

// Define the input parameters in a single object
const hashRequest = {
    networkIdentifier: {
        blockchain: 'CARDANO',   // Specify the blockchain identifier ('CARDANO' for Cardano).
        network: 'NETWORK_NAME', // Specify the network name.
        subNetworkIdentifier: {
            network: 'SUB_NETWORK_NAME', // Specify the sub-network name (optional).
            metadata: {
                // Optional metadata key-value pairs.
            },
        },
    },
    signedTransaction: 'SIGNED_TRANSACTION', // Specify the signed transaction blob.
};

// Calculate the hash of the transaction
const transactionHash = await tatum.rpc.getHashOfTransaction(hashRequest);

// Log the transaction hash
console.log('Transaction Hash:', transactionHash);

// Always destroy the Tatum SDK instance when done to stop any background processes
await tatum.destroy();
```

### Overview

The `getHashOfTransaction` method allows you to calculate the unique transaction hash (ID) for a signed transaction. The transaction hash represents the unique identifier for a transaction on the Cardano blockchain.

### Example Use Cases

1. **Transaction Hash Calculation**: Developers can use this method to calculate the transaction hash for a signed transaction, which can be useful for tracking and verifying transactions on the Cardano network.

### Request Parameters

The `getHashOfTransaction` method requires the following parameters in the request body:

- `networkIdentifier` (object, required): An object containing information about the blockchain network.
  - `blockchain` (string, required): The blockchain identifier, which should be set to `CARDANO` for Cardano.
  - `network` (string, required): The network name for Cardano.
  - `subNetworkIdentifier` (object, optional): An optional sub-network identifier object.
    - `network` (string, required): The name of the sub-network within Cardano.
    - `metadata` (object, optional): Metadata associated with the sub-network.
- `signedTransaction` (string, required): The signed transaction blob for which you want to calculate the transaction hash.

### Return Object

The method returns a string representing the transaction hash (ID) of the provided signed transaction.

Structure and behavior of this method may vary with different versions of the Cardano service. Always refer to the documentation specific to the version you are using for the most accurate information.