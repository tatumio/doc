# deriveAccount

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
    publicKeys: {
        hexBytes: 'PUBLIC_KEY_HEX_BYTES', // string, required
        curveType: 'secp256k1', // CurveType, required (Choose from: secp256k1, secp256k1_bip340, secp256r1, edwards25519, tweedle, pallas)
    },
    metadata: {
        // metadata is optional object
    }, 
};

// Derive the account identifier from the public key
const accountIdentifier = await tatum.rpc.deriveAccount(params);

// Log the account identifier
console.log('Account Identifier:', accountIdentifier);

// Always destroy the Tatum SDK instance when done to stop any background processes
await tatum.destroy();
```

### Overview

The `deriveAccount` method allows you to derive an account identifier (AccountIdentifier) from a public key.

### Example Use Cases

1. **Account Identification**: Developers can use this method to derive the account identifier associated with a public key.

### Request Parameters

The `deriveAccount` method requires the following parameter:

- `networkIdentifier` (object, required): An object containing information about the blockchain network.
  - `blockchain` (string, required): The blockchain identifier, which should be set to `CARDANO` for Cardano.
  - `network` (string, required): The network name for Cardano.
  - `subNetworkIdentifier` (object, optional): An optional sub-network identifier object.
    - `network` (string, required): The name of the sub-network within Cardano.
    - `metadata` (object, optional): Metadata associated with the sub-network.
- `publicKey` (object, required): PublicKey contains a public key byte array for a particular CurveType encoded in hex. Note that there is no PrivateKey struct as this is NEVER the concern of an implementation.
    - `hexBytes` (string, required): The hexadecimal representation of the public key.
    - `curveType` (string, enum, required): The type of cryptographic curve associated with the public key (Choose from: secp256k1, secp256k1_bip340, secp256r1, edwards25519, tweedle, pallas).
- `metadata` (object, optional): An optional metadata object.

### Return Object

The method returns an object representing the derived account identifier (AccountIdentifier) associated with the specified public key.

Structure and behavior of this method may vary with different versions of the Cardano service. Always refer to the documentation specific to the version you are using for the most accurate information.