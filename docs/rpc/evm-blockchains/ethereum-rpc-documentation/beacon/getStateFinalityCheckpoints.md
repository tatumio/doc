# getStateFinalityCheckpoints

### How to use it

```typescript
// Import necessary libraries and modules
import { TatumSDK, Ethereum, Network } from '@tatumio/tatum';

// Initialize the Tatum SDK with Ethereum-specific parameters
const tatum = await TatumSDK.init<Ethereum>({ network: Network.ETHEREUM_HOLESKY });

// Specify the state ID
const StateId = 'your-state-id';

// Retrieve the finality checkpoints using the getStateFinalityCheckpoints method
const finalityCheckpoints = await tatum.rpc.bacon.v1.getStateFinalityCheckpoints({stateId: StateId});

// Destroy Tatum SDK - needed for stopping background jobs
tatum.destroy();
```

### Overview

The `getStateFinalityCheckpoints` endpoint allows you to retrieve the finality checkpoints associated with a specific `stateId`.

### Example use cases:

1. **Finality Assessment:** 
   Developers can use finality checkpoints to assess the level of finality reached by the Ethereum Beacon Chain. By examining the `previous_justified`, `current_justified`, and `finalized` checkpoints, they can determine the state of consensus and the security of the network.

2. **Validator Monitoring:** 
   Validators in the Ethereum 2.0 network can use finality checkpoints to monitor the progress and stability of the network. They can track changes in the `previous_justified` and `current_justified` checkpoints to ensure they are participating in a secure and finalized chain.

3. **Network Stability Analysis:** 
   Network administrators and developers can monitor the network's finality checkpoints to assess its stability. Sudden changes or deviations in the `previous_justified`, `current_justified`, and `finalized` checkpoints may indicate issues or attacks on the network, prompting immediate action.

### Request Parameters

The `getStateFinalityCheckpoints` endpoint requires the following parameter:

- `stateId` (string, required):
  The unique identifier for the Ethereum Beacon Chain state for which you want to retrieve finality checkpoints.

### Return Object

The response from the `getStateFinalityCheckpoints` endpoint typically includes the following information:

- `execution_optimistic` (boolean, optional):
  - Example: `false`
  - `true` if the response references an unverified execution payload. Optimistic information may be invalidated at a later time. If the field is not present, assume the `false` value.

- `finalized` (boolean, optional):
  - Example: `false`
  - `true` if the response references the finalized history of the chain, as determined by fork choice. If the field is not present, additional calls are necessary to compare the epoch of the requested information with the finalized checkpoint.

- `data` (object):
  The `data` object contains the finality checkpoints with the following structure:

  - `previous_justified` (object):
    The `previous_justified` object provides information about the previous justified beacon block.

  - `current_justified` (object):
    The `current_justified` object provides information about the current justified beacon block.

  - `finalized` (object):
    The `finalized` object provides information about the finalized beacon block.

Please note that the provided examples demonstrate the expected structure of the `data` object. The actual values within each object may vary.

