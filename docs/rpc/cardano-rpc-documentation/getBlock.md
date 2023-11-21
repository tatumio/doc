# getBlock

### How to use it

```typescript
// Import required libraries and modules from Tatum SDK
import { TatumSDK, CardanoRosetta, Network } from '@tatumio/tatum';

// Initialize the Tatum SDK for Cardano
const tatum = await TatumSDK.init<CardanoRosetta>({ network: Network.CARDANO_ROSETTA });

// Define the input parameters in a single object
const params = {
    networkIdentifier: {
        blockchain: 'CARDANO',  // string, required
        network: 'NETWORK_NAME',  // string, required
        subNetworkIdentifier: {
            network: 'SUB_NETWORK_NAME',  // string (optional)
            metadata: {
                [key: string]: any,  // object (optional)
            },
        },
    },
    blockIdentifier: {
        index: 1123941,  // number (int64), required
        hash: '0x1f2cc6c5027d2f201a5453ad1119574d2aed23a392654742ac3c78783c071f85',  // string (optional)
    },
};

// Call the getBlock
const block = await tatum.rpc.getBlock(params);

// Log the block details
console.log('Block:', block);

// Always destroy the Tatum SDK instance when done to stop any background processes
await tatum.destroy();
```

### Overview

The `getBlock` method allows you to retrieve information about a specific Cardano block based on the provided parameters.

### Request Body

The request body should contain the following parameters:

- `networkIdentifier` (object, required): An object containing information about the blockchain network.
  - `blockchain` (string, required): The blockchain identifier, which should be set to `CARDANO` for Cardano.
  - `network` (string, required): The network name for Cardano.
  - `subNetworkIdentifier` (object, optional): An optional sub-network identifier object.
    - `network` (string, required): The name of the sub-network within Cardano.
    - `metadata` (object, optional): Metadata associated with the sub-network.
- `blockIdentifier` (object): An object containing information about the block to retrieve.
  - `index` (number, required): The index of the block (Type: number, Format: int64).
  - `hash` (string): The hash of the block (optional).

### Response

The response will contain details about the specified Cardano block.

Structure and behavior of this method may vary with different versions of the Cardano service. Always refer to the documentation specific to the version you are using for the most accurate information.