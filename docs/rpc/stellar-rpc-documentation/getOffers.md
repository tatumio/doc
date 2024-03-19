# getOffers

### How to use it

```typescript
// Import required libraries and modules from Tatum SDK
import { TatumSDK, Stellar, Network } from "@tatumio/tatum";

// Initialize the Tatum SDK for Stellar
const tatum = await TatumSDK.init<Stellar>({ network: Network.STELLAR });

// Define parameters (Replace placeholders with actual values and remove redundant)
const params = {
  sponsor: "SPONSOR_ADDRESS",
  seller: "SELLER_ADDRESS",
  sellingAssetType: "ASSET_TYPE",
  sellingAssetIssuer: "ASSET_ISSUER",
  sellingAssetCode: "ASSET_CODE",
  buyingAssetType: "ASSET_TYPE",
  buyingAssetIssuer: "ASSET_ISSUER",
  buyingAssetCode: "ASSET_CODE",
  cursor: "YOUR_CURSOR",
  order: "asc",
  limit: 10,
};

// List all open offers
const allOffers = await tatum.rpc.getOffers(params);

// Always destroy the Tatum SDK instance when done to stop any background processes
await tatum.destroy();
```

### Overview

The `getOffers` method allows you to list all currently open offers on the Stellar blockchain.

### Example use cases:

1. **Offer Monitoring:**
   Developers and applications can use this method to monitor and retrieve information about all open offers on the Stellar network.

2. **Offer Filtering:**
   Platform administrators can filter and search for specific offers based on various criteria, such as asset type, issuer, code, seller, and more.

3. **Streaming Offers:**
   Users can use streaming mode to listen for new offers as they are added to the Stellar ledger.

### Request Parameters

The `getOffers` method accepts the following optional parameters:

- `sponsor` (string, optional):
  Filter by the sponsor of the offer.

- `seller` (string, optional):
  Filter by the seller of the offer.

- `sellingAssetType` (string, optional):
  Filter by the selling asset type.

- `sellingAssetIssuer` (string, optional):
  Filter by the selling asset issuer.

- `sellingAssetCode` (string, optional):
  Filter by the selling asset code.

- `buyingAssetType` (string, optional):
  Filter by the buying asset type.

- `buyingAssetIssuer` (string, optional):
  Filter by the buying asset issuer.

- `buyingAssetCode` (string, optional):
  Filter by the buying asset code.

- `cursor` (string, optional):
  An optional cursor to start listing offers from a specific point.

- `order` (string, optional):
  An optional parameter to specify the order of listing (asc or desc). If not provided, it defaults to 'asc'.

- `limit` (number, optional):
  An optional parameter to specify the maximum number of offers to return. The limit can range from 1 to 200.

### Return Object

The `getOffers` method returns an array of open offers on the Stellar blockchain. Each offer object contains information such as the offer ID, sponsor, seller, buying asset, selling asset, and more.

(Note: The exact fields in the return object might vary based on the Stellar blockchain's implementation and version.)

```json
{
  "_links": {
    "self": {
      "href": "https://01-vinthill-068-01.rpc.tatum.io/offers?cursor=&limit=10&order=asc"
    },
    "next": {
      "href": "https://01-vinthill-068-01.rpc.tatum.io/offers?cursor=1848&limit=10&order=asc"
    },
    "prev": {
      "href": "https://01-vinthill-068-01.rpc.tatum.io/offers?cursor=2&limit=10&order=desc"
    }
  },
  "_embedded": {
    "records": [
      {
        "_links": {
          "self": {
            "href": "https://01-vinthill-068-01.rpc.tatum.io/offers/2"
          },
          "offer_maker": {
            "href": "https://01-vinthill-068-01.rpc.tatum.io/accounts/GBPO4N6XOLOLW2EV6X2AEQMLKOBH3WF2IJCZEQU65SVVSN4JD44WORKD"
          }
        },
        "id": "2",
        "paging_token": "2",
        "seller": "GBPO4N6XOLOLW2EV6X2AEQMLKOBH3WF2IJCZEQU65SVVSN4JD44WORKD",
        "selling": {
          "asset_type": "credit_alphanum4",
          "asset_code": "CHP",
          "asset_issuer": "GDW3CNKSP5AOTDQ2YCKNGC6L65CE4JDX3JS5BV427OB54HCF2J4PUEVG"
        },
        "buying": {
          "asset_type": "credit_alphanum4",
          "asset_code": "BEER",
          "asset_issuer": "GDW3CNKSP5AOTDQ2YCKNGC6L65CE4JDX3JS5BV427OB54HCF2J4PUEVG"
        },
        "amount": "1.9991292",
        "price_r": {
          "n": 1903,
          "d": 20
        },
        "price": "95.1500000",
        "last_modified_ledger": 50044488,
        "last_modified_time": null
      }
    ]
  }
}
```
