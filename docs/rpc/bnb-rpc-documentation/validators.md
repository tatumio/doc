# Validators

### How to Use It

```typescript
// Importing Tatum SDK for Beacon Chain
import { TatumSDK, Network, Bnb } from '@tatumio/tatum';

// Initializing SDK for Beacon Chain network
const tatum = await TatumSDK.init<Bnb>({ network: Network.BNB });

// Optional parameters 
const params = {
    height : 'your-height',
    page : 'your-page',
    perPage : 'entries-per-page'
};
// Retrieve the current validator set
const validatorSet = await tatum.rpc.validators(params);
console.log(validatorSet);

// Destroy Tatum SDK - needed for stopping background jobs
tatum.destroy();
```

### Overview

The `validators` method is used to retrieve the current validator set on the BNB Beacon Chain.

### Parameters

- `height` (string, optional): Height to return. If no height is provided, it will fetch the validator set corresponding to the latest block.
- `page` (string, optional): Page number (1-based).
- `perPage` (string, optional): Number of entries per page (max: 100).

### Return Object (Required)

- `block_height` (string): Example: `55`
- `validators` (array): An array of validator objects representing the validators in the set. Example: `[]`

(Note: The exact structure of the validator objects and response may vary based on the BNB Beacon Chain's implementation and version.)