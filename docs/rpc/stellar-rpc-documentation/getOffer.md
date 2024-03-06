# getOffer

### How to use it

```typescript
// Import required libraries and modules from Tatum SDK
import { TatumSDK, Stellar, Network } from "@tatumio/tatum";

// Initialize the Tatum SDK for Stellar
const tatum = await TatumSDK.init<Stellar>({ network: Network.STELLAR });

// Define parameters (Replace placeholders with actual values and remove redundant)
const offerId = "OFFER_ID";

// Retrieve information on a specific offer
const offerInfo = await tatum.rpc.getOffer(offerId);

// Always destroy the Tatum SDK instance when done to stop any background processes
await tatum.destroy();
```

### Overview

The `getOffer` method allows you to retrieve information on a specific offer by providing the offer's unique identifier.

### Example use cases:

1. **Offer Information Retrieval:**
   Developers and applications can use this method to retrieve detailed information about a specific offer on the Stellar network.

2. **Offer Verification:**
   Users can verify the details of an offer, including the asset types, issuer, code, and other relevant information.

### Request Parameters

The `getOffer` method accepts the following parameter:

- `offerId` (string, required):
  The unique identifier of the offer for which you want to retrieve information.

### Return Object

The `getOffer` method returns detailed information about the specified offer on the Stellar blockchain. The response includes data such as the offer ID, sponsor, seller, buying asset, selling asset, and more.

(Note: The exact fields in the return object might vary based on the Stellar blockchain's implementation and version.)
