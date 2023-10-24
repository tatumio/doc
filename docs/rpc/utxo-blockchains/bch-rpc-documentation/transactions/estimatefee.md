# estimatefee

### How to use it

```typescript
import { TatumSDK, BitcoinCash, Network } from '@tatumio/tatum';

// Initialize Tatum SDK for Bitcoin Cash
const tatum = await TatumSDK.init<BitcoinCash>({ network: Network.BITCOIN_CASH });

// Call the estimatefee method
const estimatedFee = await tatum.rpc.estimateFee();

console.log('Estimated fee:', estimatedFee.result);

// Destroy Tatum SDK - needed for stopping background jobs
tatum.destroy();
```

### Overview

The `estimatefee` method is used to estimate the transaction fee for a Bitcoin transaction. It calculates the fee based on the current network conditions.

### Example use cases:

1. **Transaction Fee Calculation:** 
   This method is commonly used by wallet applications to calculate the appropriate transaction fee for a transaction based on the desired confirmation time.

2. **Custom Fee Estimation:** 
   Developers can use this method to implement custom fee estimation logic in their applications.

### Request Parameters

The `estimatefee` method does not require any parameters.

### Return Object

The `estimatefee` method returns an estimated transaction fee in currency unit. The fee is typically represented as a numeric value.
