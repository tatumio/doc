# getNetworkStatus

### How to use it

```typescript
// Import required libraries and modules from Tatum SDK
import { TatumSDK, CardanoRosetta, Network } from '@tatumio/tatum';

// Initialize the Tatum SDK for Cardano
const tatum = await TatumSDK.init<CardanoRosetta>({ network: Network.CARDANO_ROSETTA });

// Define the input parameters in a single object
const params = {
    network_identifier: {
        blockchain: 'CARDANO',  // string, required
        network: 'NETWORK_NAME',  // string, required
        sub_network_identifier: {
            network: 'SUB_NETWORK_NAME',  // string (optional)
            metadata: {
                [key: string]: any,  // object (optional)
            },
        },
    },
    metadata: {
                [key: string]: any,  // object (optional)
            }, 
};

// Retrieve the status of the Cardano network
const getNetworkStatus = await tatum.rpc.getNetworkStatus(params);

// Log the network status
console.log('Cardano Network Status:', getNetworkStatus);

// Always destroy the Tatum SDK instance when done to stop any background processes
await tatum.destroy();
```

### Overview

The `getNetworkStatus` method allows you to retrieve the current status of a Cardano network.

### Example Use Cases

1. **Network Information**: Developers can use this method to retrieve the current status and information of a Cardano network, including details about the network itself and its status.

### Request Parameters

The `getNetworkStatus` method requires the following parameters:

- `networkIdentifier` (object, required): An object containing information about the blockchain network.
  - `blockchain` (string, required): The blockchain identifier, which should be set to `CARDANO` for Cardano.
  - `network` (string, required): The network name for Cardano.
  - `subNetworkIdentifier` (object, optional): An optional sub-network identifier object.
    - `network` (string, required): The name of the sub-network within Cardano.
    - `metadata` (object, optional): Metadata associated with the sub-network.
- `metadata` (object, optional): Metadata associated with the network status.

### Return Object

The method returns an object representing the current status of the Cardano network.

Structure and behavior of this method may vary with different versions of the Cardano service. Always refer to the documentation specific to the version you are using for the most accurate information.