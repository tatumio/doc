# getBlockHeader

### How to use it

```typescript
// Import necessary libraries and modules
import { TatumSDK, Ethereum, Network } from '@tatumio/tatum';

// Initialize the Tatum SDK with Ethereum-specific parameters
const tatum = await TatumSDK.init<Ethereum>({ network: Network.ETHEREUM_HOLESKY });

// Specify the block ID
const BlockId = '0xabcdef1234567890';

// Retrieve the beacon block header using the getBlockHeader method
const beaconHeader = await tatum.rpc.bacon.v1.getBlockHeader({blockId: BlockId});

// Destroy Tatum SDK - needed for stopping background jobs
tatum.destroy();
```

### Overview

The `getBlockHeader` endpoint allows you to retrieve a specific beacon block header from the Ethereum 2.0 Beacon Chain based on its unique block ID.

### Example use cases:

1. **Header Retrieval:** 
   Developers and network administrators can use this endpoint to fetch the header of a specific beacon block for analysis or verification purposes.

2. **Validator Operations:** 
   Validators may need to retrieve specific beacon block headers for proposing and attesting to blocks.

### Request Parameters

The `getBlockHeader` endpoint requires the following parameter:

- `blockId` (string, required):
  - Description: The unique block ID of the beacon block header you want to retrieve. It can be one of: head (canonical head in node's view), genesis, finalized, justified, slot and blockRoot {hex encoded blockRoot with 0x prefix}
  - Example: `"0xabcdef1234567890"`

### Return Object

The response from the `getBlockHeader` endpoint typically includes the following information:

- `execution_optimistic` (boolean, optional):
  - Example: `false`
  - `true` if the response references an unverified execution payload. Optimistic information may be invalidated at a later time. If the field is not present, assume the `false` value.

- `finalized` (boolean, optional):
  - Example: `false`
  - `true` if the response references the finalized history of the chain, as determined by fork choice. If the field is not present, additional calls are necessary to compare the epoch of the requested information with the finalized checkpoint.

- `data` (object):
  The `data` object contains the following properties:

  - `root` (string, hex):
    - Example: `"0xcf8e0d4e9587369b2301d0790347320302cc0943d5a1884560367e8208d920f2"`
    - The `root` is a hexadecimal string representing the root hash of the beacon block header. It follows the pattern: `^0x[a-fA-F0-9]{64}$`.

  - `canonical` (boolean):
    - Example: `true`
    - `true` if the block header is considered canonical, indicating it's part of the main chain.

  - `header` (object):
    The `header` object contains detailed information about the beacon block header.

Please note that the provided examples demonstrate the expected format of each field in the response. The actual values may vary.
