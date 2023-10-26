# getStateRoot

### How to use it

```typescript
// Import necessary libraries and modules
import { TatumSDK, Ethereum, Network } from '@tatumio/tatum'

// Initialize the Tatum SDK with Ethereum-specific parameters
const tatum = await TatumSDK.init<Ethereum>({ network: Network.ETHEREUM })

// Specify the state ID
const StateId = 'your-state-id';

// Retrieve the state root using the getStateRoot method
const stateRoot = await tatum.rpc.beacon.v1.getStateRoot({stateId: StateId});

// Destroy Tatum SDK - needed for stopping background jobs
tatum.destroy()
```

### Overview

The `getStateRoot` endpoint allows you to retrieve the state root of a specific Ethereum Beacon Chain state.

### Example use cases:

1. **State Verification:** 
   Developers can verify the state of the Ethereum Beacon Chain at a specific state ID.
   
2. **Custom Queries:** 
   Network administrators and developers can use this data for custom queries and analysis of the Ethereum 2.0 network.

### Request Parameters

The `getStateRoot` endpoint requires the following parameter:

- `stateId` (string, required):
  The unique identifier for the Ethereum Beacon Chain state you want to retrieve the root for.

### Return Object

The response from the `getStateRoot` endpoint typically includes the following information:

- `execution_optimistic` (boolean):
  - Example: `false`
  - `true` if the response references an unverified execution payload. Optimistic information may be invalidated at a later time. If the field is not present, assume the `false` value.

- `finalized` (boolean):
  - Example: `false`
  - `true` if the response references the finalized history of the chain, as determined by fork choice. If the field is not present, additional calls are necessary to compare the epoch of the requested information with the finalized checkpoint.

- `data` (object):
  The `data` object contains the following property:

  - `root` (string, hex):
    - Example: `"0xcf8e0d4e9587369b2301d0790347320302cc0943d5a1884560367e8208d920f2"`
    - The `root` is a hexadecimal string representing the HashTreeRoot of the BeaconState object. It follows the pattern: `^0x[a-fA-F0-9]{64}$`.

Please note that the provided examples demonstrate the expected format of each field in the response. The actual values may vary.

