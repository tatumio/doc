# getStateValidatorBalances

### How to use it

```typescript
// Import necessary libraries and modules
import { TatumSDK, Ethereum, Network } from '@tatumio/tatum'

// Initialize the Tatum SDK with Ethereum-specific parameters
const tatum = await TatumSDK.init<Ethereum>({ network: Network.ETHEREUM_HOLESKY })

// Specify the state ID and optional array of validator IDs
const params = {
  state_id: 'your-state-id',
  id: ['validator-1', 'validator-2'], // Optional
}

// Retrieve validator balances using the getStateValidatorBalances method
const validatorBalances = await tatum.rpc.bacon.v1.getStateValidatorBalances(params);

// Destroy Tatum SDK - needed for stopping background jobs
tatum.destroy()
```

## Overview

The `getStateValidatorBalances` endpoint allows you to retrieve the balances of specific validators within the Ethereum Beacon Chain state.

## Request Parameters

The `getStateValidatorBalances` endpoint requires the following parameters:

- `stateId` (string, path, required):
  State identifier. It can be one of the following: "head" (canonical head in the node's view), "genesis," "finalized," "justified," or a specific `<slot>`. You can also use a `<hex encoded stateRoot>` with a 0x prefix. Example: head.

- `id` (array of strings, query, optional):
  An optional parameter to specify the IDs of validators for which you want to retrieve balances. You can provide an array of hex-encoded public keys (any bytes48 with a 0x prefix) or validator indices.

## Return Object

The response from the `getStateValidatorBalances` endpoint typically includes the following information:

- `execution_optimistic` (boolean):
  Example: `false`
  `true` if the response references an unverified execution payload. Optimistic information may be invalidated at a later time. If the field is not present, assume the `false` value.

- `finalized` (boolean):
  Example: `false`
  `true` if the response references the finalized history of the chain, as determined by fork choice. If the field is not present, additional calls are necessary to compare the epoch of the requested information with the finalized checkpoint.

- `data` (array of objects):
  An array of objects containing the following properties:

  - `index` (string):
    Example: `1`
    Index of the validator in the validator registry.

  - `balance` (string):
    Example: `1`
    Current validator balance in gwei.

Please note that the `id` parameter is optional, and if not provided, the method will retrieve balances for all validators in the specified state.