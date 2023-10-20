# getGenesis

### How to use it

```typescript
// Import necessary libraries and modules
import { TatumSDK, Ethereum, Network } from '@tatumio/tatum'

// Initialize the Tatum SDK with Ethereum-specific parameters
const tatum = await TatumSDK.init<Ethereum>({ network: Network.ETHEREUM_HOLESKY })

// Retrieve the Ethereum Beacon Chain genesis information
const response = await tatum.rpc.getGenesis()

// Destroy Tatum SDK - needed for stopping background jobs
tatum.destroy()
```

### Overview

The `getGenesis` endpoint allows you to retrieve critical information about the genesis state of the Ethereum Beacon Chain.

### Example use cases:

1. **Validator Setup:** 
   Validators joining the Ethereum Beacon Chain network need the genesis information to initialize their nodes correctly.
   
2. **Network Monitoring:** 
   Network administrators and developers use this data to monitor and analyze the Ethereum 2.0 network's health and progress.

### Request Parameters

The `getGenesis` endpoint does not require any additional parameters. You can simply make a GET request to the endpoint to retrieve the genesis information.

### Return Object

The response from the `getGenesis` endpoint typically includes the following information:

- `execution_optimistic` (boolean, optional):
  - Example: `false`
  - `true` if the response references an unverified execution payload. Optimistic information may be invalidated at a later time. If the field is not present, assume the `false` value.

- `finalized` (boolean, optional):
  - Example: `false`
  - `true` if the response references the finalized history of the chain, as determined by fork choice. If the field is not present, additional calls are necessary to compare the epoch of the requested information with the finalized checkpoint.

- `data` (object):
  The `data` object contains the following properties:

  - `previous_version` (string, hex):
    - Example: `"0x00000000"`
    - The `previous_version` is a hexadecimal string representing the previous version of the fork. It follows the pattern: `^0x[a-fA-F0-9]{8}$`. It is a fork version number.

  - `current_version` (string, hex):
    - Example: `"0x00000000"`
    - The `current_version` is a hexadecimal string representing the current version of the fork. It follows the pattern: `^0x[a-fA-F0-9]{8}$`. It is a fork version number.

  - `epoch` (string):
    - Example: `"1"`
    - The `epoch` is a string representing the epoch at which the fork occurred.

Please note that the provided examples demonstrate the expected format of each field in the response. The actual values may vary.
