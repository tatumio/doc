# getOfferTrades

### How to use it

```typescript
// Import required libraries and modules from Tatum SDK
import { TatumSDK, Stellar, Network } from '@tatumio/tatum';

// Initialize the Tatum SDK for Stellar
const tatum = await TatumSDK.init<Stellar>({ network: Network.STELLAR });

// Define parameters (Replace placeholders with actual values and remove redundant)
const params = {
    offerId = 'OFFER_ID';
    cursor = 'YOUR_CURSOR';
    order = 'asc';
    limit = 10;
}

// Retrieve trades for a specific offer
const offerTrades = await tatum.rpc.getOfferTrades(params);

// Always destroy the Tatum SDK instance when done to stop any background processes
await tatum.destroy();
```

### Overview

The `getOfferTrades` method allows you to retrieve all trades associated with a specific offer by providing the offer's unique identifier.

### Example use cases:

1. **Trade Analysis:**
   Developers and applications can use this method to analyze and retrieve information about trades related to a specific offer on the Stellar network.

2. **Trade Monitoring:**
   Platform administrators can monitor and track trades associated with offers for auditing and management purposes.

3. **Streaming Trades:**
   Users can use streaming mode to listen for new trades related to the offer as they are added to the Stellar ledger.

### Request Parameters

The `getOfferTrades` method accepts the following optional parameters:

- `offerId` (string, required):
  The unique identifier of the offer for which you want to retrieve trades.

- `cursor` (string, optional):
  An optional cursor to start listing trades from a specific point.

- `order` (string, optional):
  An optional parameter to specify the order of listing (asc or desc). If not provided, it defaults to 'asc'.

- `limit` (number, optional):
  An optional parameter to specify the maximum number of trades to return. The limit can range from 1 to 200.

### Return Object

The `getOfferTrades` method returns an array of trades related to the specified offer on the Stellar blockchain. Each trade object contains information such as the trade ID, seller, buyer, price, and more.

(Note: The exact fields in the return object might vary based on the Stellar blockchain's implementation and version.)

```json
{
  "value": {
    "_links": {
      "self": {
        "href": "https://horizon.stellar.org/offers/104078276/trades?cursor=&limit=3&order=asc"
      },
      "next": {
        "href": "https://horizon.stellar.org/offers/104078276/trades?cursor=107449584845914113-0&limit=3&order=asc"
      },
      "prev": {
        "href": "https://horizon.stellar.org/offers/104078276/trades?cursor=107449468881756161-0&limit=3&order=desc"
      }
    },
    "_embedded": {
      "records": [
        {
          "_links": {
            "self": {
              "href": ""
            },
            "base": {
              "href": "https://horizon.stellar.org/accounts/GCO7OW5P2PP7WDN6YUDXUUOPAR4ZHJSDDCZTIAQRTRZHKQWV45WUPBWX"
            },
            "counter": {
              "href": "https://horizon.stellar.org/accounts/GD3CJYUTZAY6JQF4CEI6Z7VW5O6VNGKZTBYUECTOJPEDTB7I2HZSPI2K"
            },
            "operation": {
              "href": "https://horizon.stellar.org/operations/107449468881756161"
            }
          },
          "id": "107449468881756161-0",
          "paging_token": "107449468881756161-0",
          "ledger_close_time": "2019-07-26T09:17:02Z",
          "offer_id": "104078276",
          "base_offer_id": "104078276",
          "base_account": "GCO7OW5P2PP7WDN6YUDXUUOPAR4ZHJSDDCZTIAQRTRZHKQWV45WUPBWX",
          "base_amount": "4433.2000000",
          "base_asset_type": "native",
          "counter_offer_id": "4719135487309144065",
          "counter_account": "GD3CJYUTZAY6JQF4CEI6Z7VW5O6VNGKZTBYUECTOJPEDTB7I2HZSPI2K",
          "counter_amount": "443.3200000",
          "counter_asset_type": "credit_alphanum4",
          "counter_asset_code": "BB1",
          "counter_asset_issuer": "GD5J6HLF5666X4AZLTFTXLY46J5SW7EXRKBLEYPJP33S33MXZGV6CWFN",
          "base_is_seller": true,
          "price": {
            "n": "1",
            "d": 10
          }
        }
      ]
    }
  }
}
```
