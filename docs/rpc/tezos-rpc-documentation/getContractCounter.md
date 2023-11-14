# getContractCounter

### How to use it

```typescript
// Import required libraries and modules from Tatum SDK
import { TatumSDK, Tezos, Network } from '@tatumio/tatum';

// Initialize the Tatum SDK for Tezos
const tatum = await TatumSDK.init<Tezos>({ network: Network.TEZOS });

// Define the contract ID
const params = { 
    contractId: 'YOUR_CONTRACT_ID',     // Specify tthe contract ID 
    chainId: 'YOUR_CHAIN_ID',           // Specify the chain ID (Network identifier)
    blockId: 'YOUR_BLOCK_ID',           // Optional: Specify the block ID (hash)
};

// Retrieve the contract's counter value
const contractCounter = await tatum.rpc.getContractCounter(params);

// Log the contract's counter value
console.log(`Contract Counter Value for Contract ${contractId.contractId}:`, contractCounter);

// Always destroy the Tatum SDK instance when done to stop any background processes
await tatum.destroy();
```

### Overview

The `getContractCounter` method is used to retrieve the current counter value of a specific Tezos smart contract. The counter value represents the number of transactions or operations that have been performed on the contract.

### Example Use Cases:

1. **Transaction Verification:** Developers and users can use this method to verify the current counter value of a contract before initiating a transaction. This can help prevent accidental double-spending or ensure transaction order.

2. **Contract Interaction:** When interacting with a Tezos smart contract, it's important to be aware of the contract's counter value to ensure proper sequencing and prevent conflicts.

### Request Parameters

The `getContractCounter` method requires the following parameter:

- `contractId` (string, required): A contract identifier encoded in b58check, representing the Tezos smart contract for which you want to retrieve the counter value.
- `chainId` (string, required): The ID of the chain where the block is located.
- `blockId` (string, required): The unique identifier (hash) of the block.

### Return Object

The method returns an positive big number string representing the current counter value of the specified Tezos smart contract. This counter value reflects the number of transactions or operations that have been performed on the contract.

(Note: The exact fields in the return object might vary based on the Tezos blockchain's implementation and version.)