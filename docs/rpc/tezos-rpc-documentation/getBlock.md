# getBlock

### How to use it 

```typescript
// Import required libraries and modules from Tatum SDK
import { TatumSDK, Tezos, Network } from '@tatumio/tatum';

// Initialize the Tatum SDK for Tezos
const tatum = await TatumSDK.init<Tezos>({ network: Network.TEZOS });

// Define the chain ID and block ID (Replace placeholders with actual values)
const params = { 
    chainId: 'YOUR_CHAIN_ID',           // Specify the chain ID (Network identifier)
    blockId: 'YOUR_BLOCK_ID',           // Optional: Specify the block ID (hash)
};

// Fetch details of a specific block by its ID
const blockDetails = await tatum.rpc.getBlock(params);

// Log the block details
console.log('Block Details:', blockDetails);

// Always destroy the Tatum SDK instance when done to stop any background processes
await tatum.destroy();
```

### Overview

The `getBlock` method allows you to retrieve detailed information about a specific block within a Tezos chain. By providing the chain ID and block ID as parameters, you can access various data associated with the chosen block, including its hash, timestamp, operations, and more.

### Example use cases:

1. **Block Inspection:**
   Developers and analysts can use this method to inspect and verify the details of a specific block on the Tezos blockchain. This can be useful for auditing purposes.

2. **Transaction Confirmation:**
   Applications built on Tezos may use this method to confirm the inclusion of specific transactions in a block, ensuring their execution.

3. **Historical Data Retrieval:**
   Researchers may need to retrieve historical data from specific blocks for data analysis, historical record-keeping, or statistical analysis.

### Request Parameters

The `getBlock` method requires the following parameters:

- `chainId` (string, required): 
  The identifier of the Tezos chain from which to retrieve the block.

- `blockId` (string, required): 
  The unique identifier (hash) of the block for which you want to retrieve details.

### Return Object

The `getBlock` method returns an object containing various details about the requested block:

- `protocol` (string): The protocol identifier, e.g., "PtNairobiyssHuh87hEhfVBGCVrK3WnS8Z2FT4ymB5tAa4r1nQf".
- `chain_id` (string): The chain's unique identifier, e.g., "NetXdQprcVkpaWU".
- `hash` (string): The hash of the block, e.g., "BLVRfBFc8Mb7s4PUacDfaeQTPj9HtzTNEArM1Ni1YbxRuK73htp".
- `level` (integer): The level (block number) of the block, e.g., 4456790.
- `proto` (integer): The protocol version, e.g., 17.
- `predecessor` (string): The hash of the block's predecessor.
- `timestamp` (string): The block's timestamp, e.g., "2023-10-24T11:21:30Z".
- `validation_pass` (integer): The number of validation passes, e.g., 4.
- `operations_hash` (string): The hash of the operations included in this block.

(Note: There are additional fields in the response not covered in this list, such as `fitness`, `context`, and `signature` which provide further information about the block.)
