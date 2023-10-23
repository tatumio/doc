# getStateValidator

### How to use it

```typescript
// Import necessary libraries and modules
import { TatumSDK, Ethereum, Network } from '@tatumio/tatum';

// Initialize the Tatum SDK with Ethereum-specific parameters
const tatum = await TatumSDK.init<Ethereum>({ network: Network.ETHEREUM_HOLESKY });

// Specify the state ID and validator ID
const params = {
  stateId: 'your-state-id',
  validatorId: 'validator-1',
};

// Retrieve information about a specific validator using the getStateValidator method
const validator = await tatum.rpc.getStateValidator(params);

// Destroy Tatum SDK - needed for stopping background jobs
tatum.destroy();
```

### Overview

The `getStateValidator` endpoint allows you to retrieve detailed information about a specific validator in the Ethereum Beacon Chain. This information is valuable for anyone interested in understanding the status and details of a particular validator.

### Request Parameters

- `stateId` (string, path) *:
  State identifier. It can be one of the following: "head" (canonical head in the node's view), "genesis," "finalized," "justified," or a specific <slot>. You can also use a <hex encoded stateRoot> with a 0x prefix. Example: head.

- `validatorId` (string, path) *:
  Either a hex-encoded public key (any bytes48 with a 0x prefix) or a validator index.

### Return Object

The response from the `getStateValidator` endpoint typically includes the following information:

- `execution_optimistic` (boolean):
  Example: false
  True if the response references an unverified execution payload. Optimistic information may be invalidated at a later time. If the field is not present, assume the false value.

- `finalized` (boolean):
  Example: false
  True if the response references the finalized history of the chain, as determined by fork choice. If the field is not present, additional calls are necessary to compare the epoch of the requested information with the finalized checkpoint.

- `data` (object):
  The `data` object contains the following properties:

  - `index` (string):
    Example: 1
    Index of the validator in the validator registry.

  - `balance` (string):
    Example: 1
    Current validator balance in gwei.

  - `status` (string):
    Example: active_ongoing
    Validator status.

  - `validator` (object):
    Validator details.
