# getContractBalanceAndFrozenBonds

### How to use it

```typescript
// Import required libraries and modules from Tatum SDK
import { TatumSDK, Tezos, Network } from '@tatumio/tatum';

// Initialize the Tatum SDK for Tezos
const tatum = await TatumSDK.init<Tezos>({ network: Network.TEZOS });

// Define the contract ID
const params = { 
    contractId: 'YOUR_CONTRACT_ID',     // Spoecify the contract ID
    chainId: 'YOUR_CHAIN_ID',           // Specify the chain ID (Network identifier)
    blockId: 'YOUR_BLOCK_ID',           // Optional: Specify the block ID
};

// Retrieve the sum of the spendable balance and frozen bonds for a specific Tezos smart contract
const contractBalance = await tatum.rpc.getContractBalanceAndFrozenBonds(params);

// Log the contract's balance
console.log(`Sum of Spendable Balance and Frozen Bonds for Contract ${contractId.contractId}:`, contractBalance);

// Always destroy the Tatum SDK instance when done to stop any background processes
tatum.destroy();
```

### Overview

The `getContractBalanceAndFrozenBonds` method is used to retrieve the sum of the spendable balance and frozen bonds associated with a specific Tezos smart contract. This sum is considered part of the contract's stake, and it represents the contract's stake value if the contract is not a delegate.

### Example Use Cases:

1. **Contract Financial Analysis:** Developers and users can use this method to obtain the sum of the spendable balance and frozen bonds of a Tezos smart contract. This information is essential for financial analysis and decision-making within decentralized applications.

2. **Audit and Verification:** Auditors and verifiers can review the financial status of a smart contract, including its stake value, to ensure that it has the required funds for operations.

### Request Parameters

The `getContractBalanceAndFrozenBonds` method requires the following parameter:

- `contractId` (string, required): A contract identifier encoded in b58check, representing the Tezos smart contract for which you want to retrieve the sum of spendable balance and frozen bonds.
- `chainId` (string, required): The ID of the chain where the block is located.
- `blockId` (string, required): The unique identifier (hash) of the block.

### Return Object

The method returns a string representing the sum of the spendable balance and frozen bonds of the specified Tezos smart contract. This sum is considered part of the contract's stake and can be used to assess the contract's financial health.

Users can use this information to understand the contract's stake value, which is particularly relevant when the contract is not a delegate.

(Note: The exact fields in the return object might vary based on the Tezos blockchain's implementation and version.)