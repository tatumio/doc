# getBigMapValue

### How to use it

```typescript
// Import required libraries and modules from Tatum SDK
import { TatumSDK, Tezos, Network } from '@tatumio/tatum';

// Initialize the Tatum SDK for Tezos
const tatum = await TatumSDK.init<Tezos>({ network: Network.TEZOS });

// Define the contract ID
const contractId = { contractId: 'YOUR_CONTRACT_ID' };

// Retrieve the value from a big map associated with a Tezos smart contract
const bigMapValue = await tatum.rpc.getBigMapValue(contractId);

// Log the value from the big map
console.log(`Value from Big Map for Contract ${contractId.contractId}:`, bigMapValue);

// Always destroy the Tatum SDK instance when done to stop any background processes
await tatum.destroy();
```

### Overview

The `getBigMapValue` method is used to retrieve the value associated with a specific key from a big map associated with a Tezos smart contract. Big maps are used to store and retrieve key-value pairs within smart contracts.

### Example Use Cases:

1. **Data Retrieval:** Developers and users can use this method to query and retrieve specific data stored in a big map within a Tezos smart contract. This is particularly useful for accessing relevant information within decentralized applications.

2. **Contract Interaction:** Smart contracts may use big maps to store and manage data. Developers interacting with such contracts can use this method to access the data they need for contract interactions.

### Request Parameters

The `getBigMapValue` method requires the following parameter:

- `contractId` (string, required): A contract identifier encoded in b58check, representing the Tezos smart contract that contains the big map.

### Return Object

The method returns an object containing the following properties:

- `key` (string): The key used to query the big map and retrieve the associated value.

- `type` (string): The type of the value associated with the specified key in the big map.

Users can use this method to access and utilize data stored within big maps in Tezos smart contracts.

(Note: The exact fields in the return object might vary based on the Tezos blockchain's implementation and version.)