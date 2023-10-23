# getStateSyncCommittees

### How to us it 

```Typescript
// Import necessary libraries and modules
import { TatumSDK, Ethereum, Network } from '@tatumio/tatum';

// Initialize the Tatum SDK with Ethereum-specific parameters
const tatum = await TatumSDK.init<Ethereum>({ network: Network.ETHEREUM_HOLESKY });

// Specify request parameters as one object
const params = {
  stateId: 'your-state-id',
  epoch: 'your-epoch', // Optional: Replace with the desired epoch
};

// Retrieve sync committees for the specified state
const syncCommittees = await tatum.rpc.bacon.v1.getStateSyncCommittees(params);

// Destroy Tatum SDK - needed for stopping background jobs
tatum.destroy();
```

## Overview

The `getStateSyncCommittees` endpoint allows you to retrieve information about the sync committees of the Ethereum Beacon Chain for a specific state.

## Request Parameters

The `getStateSyncCommittees` endpoint requires the following parameters:

- `state_id` (string, path):
  - State identifier. Can be one of: "head" (canonical head in the node's view), "genesis," "finalized," "justified," or a specific `<slot>`. You can also use a `<hex encoded stateRoot>` with a 0x prefix. Example: `head`.

- `epoch` (string, query):
  - Optional parameter to fetch sync committees for a specific epoch.

## Return Object

The response from the `getStateSyncCommittees` endpoint typically includes the following information:

- `execution_optimistic` (boolean):
  - Example: `false`
  - `true` if the response references an unverified execution payload. Optimistic information may be invalidated at a later time. If the field is not present, assume the `false` value.

- `finalized` (boolean):
  - Example: `false`
  - `true` if the response references the finalized history of the chain, as determined by fork choice. If the field is not present, additional calls are necessary to compare the epoch of the requested information with the finalized checkpoint.

- `data` (object):
  - The `data` object contains information related to sync committees.

    - `validators` (array):
      - An array of validators participating in sync committees.

    - `validator_aggregates` (array):
      - An array of aggregated data from validators in sync committees.

Please note that the provided examples demonstrate the expected format of each field in the response. The actual values may vary.
