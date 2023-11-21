# createNetworkTransaction

### How to use it

```typescript
// Import required libraries and modules from Tatum SDK
import { TatumSDK, CardanoRosetta, Network } from '@tatumio/tatum';

// Initialize the Tatum SDK for Cardano
const tatum = await TatumSDK.init<CardanoRosetta>({ network: Network.CARDANO_ROSETTA });

// Define the input parameters in a single object
const params = {
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
    unsignedTransaction: 'UNSIGNED_TRANSACTION', // Specify the unsigned transaction blob.
    signatures: [
        {
            signing_payload: {
                address: 'ADDRESS',        // [DEPRECATED] Network-specific address (optional).
                accountIdentifier: {
                    address: 'ADDRESS',    // Account address.
                    subAccount: {
                        address: 'ADDRESS', // Sub-account address (optional).
                        metadata: {
                            // Sub-account metadata (optional).
                        },
                    },
                    metadata: {
                        // Account metadata (optional).
                    },
                },
                hexBytes: 'PAYLOAD_HEX',   // Hex-encoded payload bytes.
                signatureType: 'ecdsa',     // Signature type (ecdsa, ecdsa_recovery, ed25519, schnorr_1, schnorr_bip340, schnorr_poseidon).
            },
            publicKeys: [
                {
                    hexBytes: 'PUBLIC_KEY_HEX',  // Hexadecimal representation of the public key.
                    curveType: 'secp256k1',     // Curve type (secp256k1, secp256k1_bip340, secp256r1, edwards25519, tweedle, pallas).
                },
            ],
            signatureType: 'ecdsa',           // Signature type (ecdsa, ecdsa_recovery, ed25519, schnorr_1, schnorr_bip340, schnorr_poseidon).
            hexBytes: 'SIGNATURE_HEX',         // Hex-encoded signature.
        },
    ],
};

// Create network transaction from signatures
const networkTransaction = await tatum.rpc.createNetworkTransaction(params);

// Log the network transaction
console.log('Network Transaction:', networkTransaction);

// Always destroy the Tatum SDK instance when done to stop any background processes
await tatum.destroy();
```

### Overview

The `createNetworkTransaction` method allows you to create a network-specific transaction from an unsigned transaction and an array of provided signatures. The signed transaction returned from this method will be sent to the `/construction/submit` endpoint by the caller.

### Example Use Cases

1. **Transaction Construction**: Developers can use this method to combine an unsigned Cardano transaction with the corresponding signatures, resulting in a fully signed network transaction ready to be submitted to the Cardano network.

### Request Parameters

The `createNetworkTransaction` method requires the following parameters in the request body:

- `networkIdentifier` (object, required): An object containing information about the blockchain network.
  - `blockchain` (string, required): The blockchain identifier, which should be set to `CARDANO` for Cardano.
  - `network` (string, required): The network name for Cardano.
  - `subNetworkIdentifier` (object, optional): An optional sub-network identifier object.
    - `network` (string, required): The name of the sub-network within Cardano.
    - `metadata` (object, optional): Metadata associated with the sub-network.
- `unsignedTransaction` (string, required): Contains the unsigned transaction blob returned by the `constructionPayloads` endpoint. The unsigned transaction represents the basic structure and details of the transaction before it is signed.
- `signatures` (array of objects, required): This parameter is an array of signatures. Each signature is represented by a Signature object. Signatures are required to create a network transaction by combining them with the unsigned transaction.
  - `signing_payload` (object, required): The payload that was signed.
    - `address` (string, optional): [DEPRECATED] The network-specific address of the account that should sign the payload.
    - `accountIdentifier` (object, optional): An object containing information about the account.
      - `address` (string, required): The Cardano account address associated with the operation.
      - `sub_account` (object, optional): An optional sub-account object.
        - `address` (string, optional): The sub-account address.
        - `metadata` (object, optional): An optional metadata object for the sub-account. If the SubAccount address is not sufficient to uniquely specify a SubAccount, any other identifying information can be stored here. It is important to note that two SubAccounts with identical addresses but differing metadata will not be considered equal by clients.
      - `metadata` (object, optional): An optional metadata object for the account. Blockchains that utilize a username model (where the address is not a derivative of a cryptographic public key) should specify the public key(s) owned by the address in metadata.
    - `hex_bytes` (string, required): Hex-encoded string of the payload bytes.
    - `signatureType` (string, enum, optional): Signature type (Choose from: ecdsa, ecdsa_recovery, ed25519, schnorr_1, schnorr_bip340, schnorr_poseidon).
  - `publicKey` (object, required): PublicKey contains a public key byte array for a particular CurveType encoded in hex. Note that there is no PrivateKey struct as this is NEVER the concern of an implementation.
    - `hexBytes` (string, required): The hexadecimal representation of the public key.
    - `curveType` (string, enum, required): The type of cryptographic curve associated with the public key (Choose from: secp256k1, secp256k1_bip340, secp256r1, edwards25519, tweedle, pallas).
  - `signatureType` (string, enum, required): Signature type (Choose from: ecdsa, ecdsa_recovery, ed25519, schnorr_1, schnorr_bip340, schnorr_poseidon).
  - `hexBytes` (string, required): Hex-encoded string representing the signature.

### Return Object

The method returns an object representing the network transaction created from the unsigned transaction and provided signatures.

Structure and behavior of this method may vary with different versions of the Cardano service. Always refer to the documentation specific to the version you are using for the most accurate information.