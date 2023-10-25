# getContractBalance

### How to use it

```typescript
// Importing Tatum SDK for Tezos blockchain
import { TatumSDK, Network, Tezos } from '@tatumio/tatum';

// Initializing SDK for Tezos blockchain
const tatum = await TatumSDK.init<Tezos>({ network: Network.TEZOS });

// Define your chain ID and contract address
const params = { 
    chainId: 'YOUR_CHAIN_ID',           // Specify the chain ID (Network identifier)
    blockId: 'YOUR_BLOCK_ID',           // Optional: Specify the block ID 
    contractId: 'YOUR_CONTRACT_ID'      // Specify the contract ID
};

// Fetching contract balance
const contractBalance = await tatum.rpc.getContractBalance(params);
console.log(contractBalance);

// Cleaning up resources used by Tatum SDK
tatum.destroy();
```

### Overview

The `getContractBalance` method retrieves the balance of a specific smart contract on the Tezos blockchain.

### Parameters

- `chainId` (string, required): The ID of the chain where the smart contract is deployed.
- `blockId` (string, required): The unique identifier (hash) of the block.
- `contractAddress` (string, required): The address of the smart contract

### Return Object

The method returns an object containing the `balance` of the specified smart contract. The structure of the return object may include various fields depending on the contract's status and balance.

(Note: The exact fields in the return object might vary based on the Tezos blockchain's implementation and version.)