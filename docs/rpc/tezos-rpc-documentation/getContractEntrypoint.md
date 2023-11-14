# getContractEntryPointType

### How to use it

```typescript
// Import required libraries and modules from Tatum SDK
import { TatumSDK, Tezos, Network } from '@tatumio/tatum';

// Initialize the Tatum SDK for Tezos
const tatum = await TatumSDK.init<Tezos>({ network: Network.TEZOS });

// Define the input params
const params = {
    contractId: 'YOUR_CONTRACT_ID',         // Specify the contract ID
    chainId: 'YOUR_CHAIN_ID',           // Specify the chain ID (Network identifier)
    blockId: 'YOUR_BLOCK_ID',            // Optional: Specify the block ID if needed
    entrypoint: 'YOUR_ENTRYPOINT_NAME',     // Specify the desired entrypoint name
    normalizeTypes: false                   // Optional: Set to true if you want to normalize types
};

const entrypoint = 'YOUR_ENTRYPOINT_NAME'; // Replace with the name of the desired entrypoint

// Retrieve the type of the specified entrypoint of the Tezos smart contract
const entrypointType = await tatum.rpc.getContractEntryPointType(params);

// Log the type of the specified entrypoint
console.log(`Type of Entrypoint ${entrypoint} in Contract ${contractId.contractId}:`, entrypointType);

// Always destroy the Tatum SDK instance when done to stop any background processes
await tatum.destroy();
```

### Overview

The `getContractEntryPointType` method is used to return the type of a specific entrypoint within a Tezos smart contract. An entrypoint represents a callable function or method exposed by the contract.

### Example Use Cases:

1. **Entrypoint Type Inquiry:** Developers and users can use this method to retrieve the type information of a specific entrypoint within a smart contract. This information is essential for understanding how to interact with and invoke the entrypoint.

2. **Contract Analysis:** Analysts and auditors may use this method to examine the types associated with contract entrypoints and ensure they align with the intended functionality.

### Request Parameters

The `getContractEntryPointType` method requires the following parameters:

- `contract_id` (string, required): A contract identifier encoded in b58check, representing the Tezos smart contract for which you want to retrieve the entrypoint type.
- `chainId` (string, required): The ID of the chain where the block is located.
- `blockId` (string, required): The unique identifier (hash) of the block.
- `entrypoint` (string, required): A Michelson entrypoint name (string of length < 32), specifying the entrypoint for which you want to retrieve the type.
- `normalize_types` (boolean, optional): Indicates whether types should be normalized. If set to `true`, types will be normalized (annotations removed, combs flattened); if set to `false`, types will be kept as they appeared in the original script.

### Return Object

The method returns a Micheline expression representing the type of the specified entrypoint within the contract. This type information describes the structure and expected data for interacting with the entrypoint.

Users can use this information to ensure proper data handling and validation when invoking contract entrypoints.

Please note that the `normalize_types` parameter can affect the structure of the returned type based on whether types are normalized or kept as they appeared in the original script.

(Note: The exact fields in the return object might vary based on the Tezos blockchain's implementation and version.)