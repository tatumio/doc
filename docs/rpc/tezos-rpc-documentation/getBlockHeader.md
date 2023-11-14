# getBlockHeader

### How to use it 

```typescript
// Import required libraries and modules from Tatum SDK
import { TatumSDK, Tezos, Network } from '@tatumio/tatum';

// Initialize the Tatum SDK for Tezos
const tatum = await TatumSDK.init<Tezos>({ network: Network.TEZOS });

// Define the chain ID (For this example, we use "NetXdQprcVkpaWU" as a placeholder)
const params = {
    chainId: 'YOUR_CHAIN_ID', // Specify the chain ID (Network identifier)
    blockId: 'YOUR_BLOCK_ID', // Optional: Specify the block ID (hash)
};

// Fetch the header of a specific block by its ID
const blockHeader = await tatum.rpc.getBlockHeader(params);

// Log the block header details
console.log('Block Header:', blockHeader);

// Always destroy the Tatum SDK instance when done to stop any background processes
await tatum.destroy();
```

### Overview

The `getBlockHeader` method allows you to retrieve the header of a specific block within a Tezos chain. You can use this method to fetch essential information about a particular block, such as its hash, timestamp, and other metadata.

### Example use cases:

1. **Block Analysis:**
   Researchers and analysts can use this method to access detailed information about a specific block, enabling them to perform in-depth analysis and investigation.

2. **Transaction Confirmation:**
   Developers building applications on Tezos may need to confirm the details of a specific block to ensure the validity of transactions or smart contract interactions.

3. **Historical Data Retrieval:**
   This method is valuable for retrieving historical block data for auditing, compliance, or historical record-keeping purposes.

### Request Parameters

The `getBlockHeader` method requires the following parameters:

- `chainId` (string, required): 
  The identifier of the Tezos chain from which to retrieve the block header.

- `blockId` (string, required): 
  The unique identifier (hash) of the block for which you want to retrieve the header.

### Return Object

The `getBlockHeader` method returns an object with details of the block's header:

- `protocol` (string): The protocol identifier, e.g., "PtNairobiyssHuh87hEhfVBGCVrK3WnS8Z2FT4ymB5tAa4r1nQf".
- `chain_id` (string): The chain's unique identifier, e.g., "NetXdQprcVkpaWU".
- `hash` (string): The hash of the block, e.g., "BLVRfBFc8Mb7s4PUacDfaeQTPj9HtzTNEArM1Ni1YbxRuK73htp".
- `level` (integer): The level (block number) of the block, e.g., 4456790.
- `proto` (integer): The protocol version, e.g., 17.
- `predecessor` (string): The hash of the block's predecessor.
- `timestamp` (string): The block's timestamp, e.g., "2023-10-24T11:21:30Z".
- `validation_pass` (integer): The number of validation passes, e.g., 4.
- `operations_hash` (string): The hash of the operations included in this block.

(Note: There are additional fields in the response not covered in this list, such as `fitness`, `context`, and `signature` which provide further information about the block. The exact fields in the return object might vary based on the Tezos blockchain's implementation and version.)