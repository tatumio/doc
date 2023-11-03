# getContractEntrypoints

### How to use it

```typescript
// Import required libraries and modules from Tatum SDK
import { TatumSDK, Tezos, Network } from '@tatumio/tatum';

// Initialize the Tatum SDK for Tezos
const tatum = await TatumSDK.init<Tezos>({ network: Network.TEZOS });

const params = {
    contractId: 'YOUR_CONTRACT_ID',     // Specify the contract ID
    chainId: 'YOUR_CHAIN_ID',           // Specify the chain ID (Network identifier)
    blockId: 'YOUR_BLOCK_ID',           // Optional: Specify the block ID if needed
    normalizeTypes: false               // Optional: Set to true if you want to normalize types
};

// Retrieve the list of entrypoints of the Tezos smart contract
const entrypoints = await tatum.rpc.getContractEntrypoints(params);

// Log the list of entrypoints
console.log(`Entry Points of Contract ${params.contractId}:`, entrypoints);

// Always destroy the Tatum SDK instance when done to stop any background processes
tatum.destroy();
```

### Overview

The `getContractEntrypoints` method is used to return the list of entrypoints available in a specific Tezos smart contract. Entrypoints represent the callable functions or methods that can be invoked on the contract.

### Example Use Cases:

1. **Contract Interaction:** Developers and users can use this method to discover the available entrypoints of a smart contract. This information is essential for interacting with and invoking specific contract functions.

2. **Contract Analysis:** Analysts and auditors may use this method to examine the contract's exposed functions and ensure that they align with the intended functionality.

### Request Parameters

The `getContractEntrypoints` method requires the following parameters:

- `contract_id` (string, required): A contract identifier encoded in b58check, representing the Tezos smart contract for which you want to retrieve the list of entrypoints.
- `chainId` (string, required): The ID of the chain where the block is located.
- `blockId` (string, required): The unique identifier (hash) of the block.
- `normalize_types` (boolean, optional): Indicates whether types should be normalized. If set to `true`, types will be normalized (annotations removed, combs flattened); if set to `false`, types will be kept as they appeared in the original script.

### Return Object

The method returns an object containing the following properties:

- `unreachable` (array of objects): An array of unreachable entrypoints. Each object in the array contains a `path` property, which is an array of Michelson primitives.

- `entrypoints` (object): An object containing the available entrypoints of the contract. Each entrypoint is represented as a property, and its value is a Micheline expression describing the entrypoint's type.

Users can use this information to understand the contract's callable functions and types.

Please note that the `normalize_types` parameter can affect the structure of the returned entrypoints based on whether types are normalized or kept as they appeared in the original script.

(Note: The exact fields in the return object might vary based on the Tezos blockchain's implementation and version.)