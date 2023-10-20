# getBlockHeaders

### How to use it 

```typescript
// Import necessary libraries and modules
import { TatumSDK, Ethereum, Network } from '@tatumio/tatum';

// Initialize the Tatum SDK with Ethereum-specific parameters
const tatum = await TatumSDK.init<Ethereum>({ network: Network.ETHEREUM_HOLESKY });

// Retrieve beacon block headers using the getBlockHeaders method
const beaconHeaders = await tatum.rpc.getBlockHeaders();

// Destroy Tatum SDK - needed for stopping background jobs
tatum.destroy();
```

### Overview

The `getBlockHeaders` endpoint allows you to retrieve beacon block headers from the Ethereum 2.0 Beacon Chain. These headers contain important information about the chain's progress and state.

### Example use cases:

1. **Chain Monitoring:** 
   Developers and network administrators can use this endpoint to monitor the progress and health of the Ethereum 2.0 Beacon Chain.

2. **Validator Operations:** 
   Validators can retrieve beacon block headers to perform various operations, such as proposing and attesting to blocks.

### Request Parameters

The `getBlockHeaders` endpoint accepts the following parameters:

- `slot` (string, optional):
  - Description: The slot number to fetch beacon block headers for.
  - Example: `"12345"`

- `parent_root` (string, optional):
  - Description: The root hash of the parent beacon block header. Fetches beacon block headers for the given parent root.
  - Example: `"0xcf8e0d4e9587369b2301d0790347320302cc0943d5a1884560367e8208d920f2"`

### Return Object

The response from the `/eth/v1/beacon/headers` endpoint typically includes the following information:

- `execution_optimistic` (boolean, optional):
  - Example: `false`
  - `true` if the response references an unverified execution payload. Optimistic information may be invalidated at a later time. If the field is not present, assume the `false` value.

- `finalized` (boolean, optional):
  - Example: `false`
  - `true` if the response references the finalized history of the chain, as determined by fork choice. If the field is not present, additional calls are necessary to compare the epoch of the requested information with the finalized checkpoint.

- `data` (array):
  The `data` array contains a list of beacon block headers, where each header has the following structure:

  - `root` (string, hex):
    - Example: `"0xcf8e0d4e9587369b2301d0790347320302cc0943d5a1884560367e8208d920f2"`
    - The `root` is a hexadecimal string representing the root hash of the beacon block header. It follows the pattern: `^0x[a-fA-F0-9]{64}$`.

  - `canonical` (boolean):
    - Example: `true`
    - `true` if the block header is considered canonical, indicating it's part of the main chain.

  - `header` (object):
    The `header` object contains detailed information about the beacon block header.

Please note that the provided examples demonstrate the expected format of each field in the response. The actual values may vary.

