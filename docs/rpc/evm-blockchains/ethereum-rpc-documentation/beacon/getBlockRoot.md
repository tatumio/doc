# getBlockRoot

###

```typescript
// Import necessary libraries and modules
import { TatumSDK, Ethereum, Network } from '@tatumio/tatum';

// Initialize the Tatum SDK with Ethereum-specific parameters
const tatum = await TatumSDK.init<Ethereum>({ network: Network.ETHEREUM_HOLESKY });

// Specify the block ID
const blockId = {blockId: 'your-block-id'}; // Replace with the desired block ID

// Retrieve the root of the specified Ethereum Beacon Chain block or block header
const blockRoot = await tatum.rpc.beacon.v1.getBlockRoot(blockId);

// Destroy Tatum SDK - needed for stopping background jobs
tatum.destroy();
```

## Overview

The `getBlockRoot` endpoint allows you to retrieve the root of a specific Ethereum Beacon Chain block or block header.

## Request Parameters

The `getBlockRoot` endpoint requires the following parameter:

- `blockId` (string, path):
  - The identifier of the Ethereum Beacon Chain block or block header.

## Return Object

The response from the `getBlockRoot` endpoint typically includes the following information:

- `execution_optimistic` (boolean):
  - Example: `false`
  - `true` if the response references an unverified execution payload. Optimistic information may be invalidated at a later time. If the field is not present, assume the `false` value.

- `finalized` (boolean):
  - Example: `false`
  - `true` if the response references the finalized history of the chain, as determined by fork choice. If the field is not present, additional calls are necessary to compare the epoch of the requested information with the finalized checkpoint.

- `data` (object):
  - The `data` object contains the following property:

    - `root` (string, hex):
      - Example: `"0xcf8e0d4e9587369b2301d0790347320302cc0943d5a1884560367e8208d920f2"`
      - The `root` is a hexadecimal string representing the HashTreeRoot of the Ethereum Beacon Chain block or block header. It follows the pattern: `^0x[a-fA-F0-9]{64}$`.

Please note that the provided examples demonstrate the expected format of each field in the response. The actual values may vary depending on the Ethereum client or API provider.
