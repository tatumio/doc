# getContractDelegate

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
    blockId: 'YOUR_BLOCK_ID'            // Optional: Specify the block ID 
    };

// Retrieve the delegate of a Tezos smart contract, if any
const contractDelegate = await tatum.rpc.getContractDelegate(params);

// Log the contract's delegate, if available
console.log(`Delegate of Contract ${contractId.contractId}:`, contractDelegate);

// Always destroy the Tatum SDK instance when done to stop any background processes
await tatum.destroy();
```

### Overview

The `getContractDelegate` method is used to access the delegate, if any, associated with a specific Tezos smart contract. In Tezos, a delegate is an entity that can participate in the consensus mechanism and represent other stakeholders' interests.

### Example Use Cases:

1. **Delegate Information:** Developers and users can use this method to retrieve information about the delegate associated with a smart contract. This information may include the delegate's public key hash and other relevant details.

2. **Stakeholder Interactions:** When interacting with Tezos smart contracts, it's important to know if a contract has a delegate, as delegates can influence various aspects of the network.

### Request Parameters

The `getContractDelegate` method requires the following parameter:

- `contract_id` (string, required): A contract identifier encoded in b58check, representing the Tezos smart contract for which you want to retrieve the delegate, if any.
- `chainId` (string, required): The ID of the chain where the block is located.
- `blockId` (string, required): The unique identifier (hash) of the block.

### Return Object

The method returns a string representing the delegate associated with the specified Tezos smart contract, if a delegate exists. The delegate is represented as an Ed25519, Secp256k1, P256, or BLS public key hash encoded in Base58Check format.

If the contract does not have a delegate, the method returns `null`. Users can check for the presence of a delegate by examining the response value.

This information can be useful for understanding the role and influence of delegates in the Tezos network.
