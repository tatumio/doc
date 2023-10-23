# getBlockAttestations

### How to ue it 

```typescript
// Import necessary libraries and modules
import { TatumSDK, Ethereum, Network } from '@tatumio/tatum';

// Initialize the Tatum SDK with Ethereum-specific parameters
const tatum = await TatumSDK.init<Ethereum>({ network: Network.ETHEREUM_HOLESKY });

// Specify the block ID in camel case
const blockId = '0xabcdef1234567890';

// Retrieve attestations for the specified block using the tatum.rpc.bacon.v1.getBlockAttestations method
const attestations = await tatum.rpc.bacon.v1.getBlockAttestations(blockId);

// Destroy Tatum SDK - needed for stopping background jobs
tatum.destroy();
```

### Overview

The `getBlockAttestations` endpoint allows you to retrieve attestations associated with a specific Ethereum 2.0 Beacon Chain block.

### Example use cases:

1. **Attestation Analysis:** 
   Researchers and validators can use this endpoint to analyze attestations made for a specific block.

2. **Validator Operations:** 
   Validators may need to retrieve attestations to check if their attestations have been included in a block.

### Request Parameters

The `getBlockAttestations` endpoint requires the following parameter:

- `blockId` (string, required):
  - Description: The unique block ID of the Ethereum 2.0 Beacon Chain block for which you want to retrieve attestations.
  - Example: `"0xabcdef1234567890"`

### Return Object

The response from the `getBlockAttestations` endpoint typically includes the following information:

- `execution_optimistic` (boolean, optional):
  - Example: `false`
  - `true` if the response references an unverified execution payload. Optimistic information may be invalidated at a later time. If the field is not present, assume the `false` value.

- `finalized` (boolean, optional):
  - Example: `false`
  - `true` if the response references the finalized history of the chain, as determined by fork choice. If the field is not present, additional calls are necessary to compare the epoch of the requested information with the finalized checkpoint.

- `data` (array of objects):
  The `data` array contains information about attestations. Each attestation object in the array includes details related to attester aggregation bits, BLS aggregate signature, and attestation data.