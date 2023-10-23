# getStateCommittees

### How to us it 

```Typescript
// Import necessary libraries and modules
import { TatumSDK, Ethereum, Network } from '@tatumio/tatum'

// Initialize the Tatum SDK with Ethereum-specific parameters
const tatum = await TatumSDK.init<Ethereum>({ network: Network.ETHEREUM_HOLESKY })

// Define the parameters object
const params = {
  stateId: 'your-state-id', // Replace with the actual state ID you want to use
  epoch: '1',   // Optional: Fetch committees for a specific epoch
  index: '1',   // Optional: Restrict returned values to a specific committee index
  slot: '1',    // Optional: Restrict returned values to a specific slot
};

// Retrieve committees information using the getStateCommittees method
const committees = await tatum.ethereum.getStateCommittees(params);

// Destroy Tatum SDK - needed for stopping background jobs
tatum.destroy()
```

### Overview

The `getStateCommittees` endpoint allows you to retrieve information about committees associated with a specific Ethereum 2.0 Beacon Chain state.

### Example use cases:

1. **Committee Analysis:** 
   Researchers and validators can use this endpoint to analyze committees for a specific state, including validator indices and shard assignments.

2. **Validator Operations:** 
   Validators may need to retrieve committee information to participate in shard or crosslink proposals.

### Request Parameters

The `getStateCommittees` endpoint supports the following optional request parameters:

- `state_id` (string, required):
  - Description: State identifier. It can be one of: "head" (canonical head in the node's view), "genesis," "finalized," "justified," `<slot>`, or `<hex encoded stateRoot with 0x prefix>`.
  - Example: `"head"`

- `epoch` (string, query, optional):
  - Description: Fetch committees for the given epoch. If not present, the committees for the epoch of the state will be obtained.
  - Example: `"1"`

- `index` (string, query, optional):
  - Description: Restrict returned values to those matching the supplied committee index.
  - Example: `"1"`

- `slot` (string, query, optional):
  - Description: Restrict returned values to those matching the supplied slot.
  - Example: `"1"`

### Return Object

The response from the `getStateCommittees` endpoint typically includes the following information:

- `execution_optimistic` (boolean, optional):
  - Example: `false`
  - `true` if the response references an unverified execution payload. Optimistic information may be invalidated at a later time. If the field is not present, assume the `false` value.

- `finalized` (boolean, optional):
  - Example: `false`
  - `true` if the response references the finalized history of the chain, as determined by fork choice. If the field is not present, additional calls are necessary to compare the epoch of the requested information with the finalized checkpoint.

- `data` (array of objects):
  - Summary: The `data` array contains information about committees. Each committee object in the array includes details related to the committee index, slot, and an array of validators assigned to attest at a specific slot with the same committee index.

Please note that the actual structure of the committee information returned may vary. 