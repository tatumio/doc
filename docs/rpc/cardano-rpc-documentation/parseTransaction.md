# transactionParse

### How to use it

```typescript
// Import required libraries and modules from Tatum SDK
import { TatumSDK, CardanoRosetta, Network } from '@tatumio/tatum';

// Initialize the Tatum SDK for Cardano
const tatum = await TatumSDK.init<CardanoRosetta>({ network: Network.CARDANO_ROSETTA });

// Define the input parameters in a single object
const parseRequest = {
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
    signed: true,                // Specify whether the transaction is signed (boolean).
    transaction: 'TRANSACTION',  // Specify the transaction blob (either unsigned or signed).
};

// Parse the transaction
const parsedTransaction = await tatum.rpc.transactionParse(parseRequest);

// Log the parsed transaction
console.log('Parsed Transaction:', parsedTransaction);

// Always destroy the Tatum SDK instance when done to stop any background processes
await tatum.destroy();
```

### Overview

The `transactionParse` method allows you to parse either an unsigned or signed transaction and retrieve information about the transaction. It is used to examine the details of a transaction without submitting it to the blockchain.

### Example Use Cases

1. **Transaction Inspection**: Developers can use this method to inspect and verify the details of a transaction before submitting it to the Cardano network.

### Request Parameters

The `transactionParse` method requires the following parameters in the request body:

- `networkIdentifier` (object, required): An object containing information about the blockchain network.
  - `blockchain` (string, required): The blockchain identifier, which should be set to `CARDANO` for Cardano.
  - `network` (string, required): The network name for Cardano.
  - `subNetworkIdentifier` (object, optional): An optional sub-network identifier object.
    - `network` (string, required): The name of the sub-network within Cardano.
    - `metadata` (object, optional): Metadata associated with the sub-network.
- `signed` (boolean, required): A boolean indicating whether the transaction is signed. Set to `true` for a signed transaction and `false` for an unsigned transaction.
- `transaction` (string, required): The transaction blob, which must be either the unsigned transaction blob returned by `constructionPayloads` or the signed transaction blob returned by `constructionCombine`.

### Return Object

The method returns an object containing parsed information about the transaction, such as transaction inputs, outputs, and other details.

Structure and behavior of this method may vary with different versions of the Cardano service. Always refer to the documentation specific to the version you are using for the most accurate information.
