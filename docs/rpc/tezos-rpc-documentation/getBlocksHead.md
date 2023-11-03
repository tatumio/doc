# getBlocksHead

## How to Use

Enclose the following TypeScript code example in \```typescript code example \``` to use the `getBlocksHead` method.

```typescript
// Import required libraries and modules from Tatum SDK
import { TatumSDK, Tezos, Network } from '@tatumio/tatum';

// Initialize the Tatum SDK for Tezos
const tatum = await TatumSDK.init<Tezos>({ network: Network.TEZOS });

// Define the chain ID 
const chainId = { chainId : 'CHAIN_ID'};

// Fetch the details of the latest (head) block on the specified Tezos chain
const latestBlockDetails = await tatum.rpc.getBlocksHead(chainId);

// Log the latest block details
console.log('Latest Block Details:', latestBlockDetails);

// Always destroy the Tatum SDK instance when done to stop any background processes
tatum.destroy();
```

## Overview

The `getBlocksHead` method allows you to retrieve details about the latest (head) block on a specific Tezos chain. You can use this method to access key information about the most recent block, such as its hash, level, timestamp, and more.

## Example Use Cases

1. **Real-Time Data Display:**
   Developers can use this method to display real-time information about the latest block on a blockchain explorer or monitoring dashboard.

2. **Transaction Monitoring:**
   Applications monitoring the Tezos blockchain can utilize this method to keep track of incoming transactions and their details.

3. **Network Analytics:**
   Researchers and analysts can gather data from the latest block for network performance analysis and reporting.

## Request Parameters

The `getBlocksHead` method requires the following parameter:

- `chainId` (string, required):
  The identifier of the Tezos chain for which you want to retrieve the latest block details.

## Return Object

The `getBlocksHead` method returns an object with details of the latest (head) block:

- `protocol` (string): The protocol identifier, e.g., "PtNairobiyssHuh87hEhfVBGCVrK3WnS8Z2FT4ymB5tAa4r1nQf".
- `chain_id` (string): The chain's unique identifier, e.g., "NetXdQprcVkpaWU".
- `hash` (string): The hash of the latest block, e.g., "BLVRfBFc8Mb7s4PUacDfaeQTPj9HtzTNEArM1Ni1YbxRuK73htp".
- `level` (integer): The level (block number) of the latest block, e.g., 4456790.
- `proto` (integer): The protocol version, e.g., 17.
- `predecessor` (string): The hash of the block's predecessor.
- `timestamp` (string): The timestamp of the latest block, e.g., "2023-10-24T11:21:30Z".
- `validation_pass` (integer): The number of validation passes, e.g., 4.
- `operations_hash` (string): The hash of the operations included in the latest block.

(Note: There are additional fields in the response not covered in this list, such as `fitness`, `context`, and `signature` which provide further information about the block. The exact fields in the return object might vary based on the Tezos blockchain's implementation and version.)