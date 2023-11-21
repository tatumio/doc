# constructionMetadata

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
    options: {
        // Optional object
    },
    publicKeys: [
        {
        hexBytes: 'PUBLIC_KEY_HEX_BYTES', // Required: Specifies the hexadecimal representation of the staking credential .
        curveType: 'SECP256K1', // Required: Specifies the curve type for the staking credential .]
    },
    ]
};

// Retrieve metadata for transaction construction on the Cardano network
const metadata = await tatum.rpc.constructionMetadata(params);

// Log the metadata
console.log('Cardano Transaction Construction Metadata:', metadata);

// Always destroy the Tatum SDK instance when done to stop any background processes
await tatum.destroy();
```

### Overview

The `constructionMetadata` method allows you to retrieve metadata required to construct a transaction for a specific network.

### Example Use Cases

1. **Metadata Retrieval**: Developers can use this method along with the `constructionPreprocess` endpoint to retrieve metadata required for transaction construction in an offline environment.

### Request Parameters

The `constructionMetadata` method requires the following parameters:

- `networkIdentifier` (object, required): An object containing information about the blockchain network.
  - `blockchain` (string, required): The blockchain identifier, which should be set to `CARDANO` for Cardano.
  - `network` (string, required): The network name for Cardano.
  - `subNetworkIdentifier` (object, optional): An optional sub-network identifier object.
    - `network` (string, required): The name of the sub-network within Cardano.
    - `metadata` (object, optional): Metadata associated with the sub-network.
- `options` (object, optional): Some blockchains require different metadata for different types of transaction construction (ex: delegation versus a transfer). Instead of requiring a blockchain node to return all possible types of metadata for construction (which may require multiple node fetches), the client can populate an options object to limit the metadata returned to only the subset required.
- `publicKey` (object, required): PublicKey contains a public key byte array for a particular CurveType encoded in hex. Note that there is no PrivateKey struct as this is NEVER the concern of an implementation.
    - `hexBytes` (string, required): The hexadecimal representation of the public key.
    - `curveType` (string, enum, required): The type of cryptographic curve associated with the public key (Choose from: secp256k1, secp256k1_bip340, secp256r1, edwards25519, tweedle, pallas).


### Return Object

The method returns an object representing the metadata required to construct a transaction for a specific network.

Structure and behavior of this method may vary with different versions of the Cardano service. Always refer to the documentation specific to the version you are using for the most accurate information.