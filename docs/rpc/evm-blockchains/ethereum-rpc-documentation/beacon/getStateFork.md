# getStateFork

### How to use it 

```typescript
// Import necessary libraries and modules
import { TatumSDK, Ethereum, Network } from '@tatumio/tatum'

// Initialize the Tatum SDK with Ethereum-specific parameters
const tatum = await TatumSDK.init<Ethereum>({ network: Network.ETHEREUM_HOLESKY })

// Specify the state ID
const StateId = 'your-state-id';

// Retrieve the state fork using the getStateFork method
const stateFork = await tatum.rpc.bacon.v1.getStateFork({stateId: StateId});

// Destroy Tatum SDK - needed for stopping background jobs
tatum.destroy()
```

### Overview

The `getStateFork` endpoint allows you to retrieve information about the fork associated with a specific Ethereum Beacon Chain state.

### Example use cases:

1. **Fork Analysis:** 
   Developers can analyze and track forks in the Ethereum Beacon Chain to make informed decisions.

2. **Network Monitoring:** 
   Network administrators and developers use this data to monitor the Ethereum 2.0 network and its forks.

### Request Parameters

The `getStateFork` endpoint requires the following parameter:

- `state_id` (string, required):
  The unique identifier for the Ethereum Beacon Chain state for which you want to retrieve fork information.

### Return Object

The response from the `getStateFork` endpoint typically includes the following information:

- `fork_version` (string, hex):
  - Example: `"0x12345678"`
  - The `fork_version` is a hexadecimal string representing the version of the fork associated with the specified state. It follows the pattern: `^0x[a-fA-F0-9]{8}$`.

- `fork_epoch` (number, integer):
  - Example: `12345`
  - The `fork_epoch` is an integer representing the epoch at which the fork occurred.

- `fork_root` (string, hex):
  - Example: `"0xabcdef0123456789"`
  - The `fork_root` is a hexadecimal string representing the root hash of the state associated with the fork. It follows the pattern: `^0x[a-fA-F0-9]{16}$`.

Please note that the provided examples demonstrate the expected format of each field in the response. The actual values may vary.
