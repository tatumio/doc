# getAccountTrades

### How to use it

```typescript
// Import required libraries and modules from Tatum SDK
import { TatumSDK, Stellar, Network } from "@tatumio/tatum";

// Initialize the Tatum SDK for Stellar
const tatum = await TatumSDK.init<Stellar>({ network: Network.STELLAR });

// Define input parameters as an object (Replace placeholders with actual values and remove redundant)
const params = {
  accountId: "YOUR_ACCOUNT_ID",
  cursor: "YOUR_CURSOR",
  order: "asc",
  limit: 10,
};

// Retrieve all trades for a specific account
const trades = await tatum.rpc.getTradesByAccountId(params);

// Log the list of trades
console.log("Trades:", trades);

// Always destroy the Tatum SDK instance when done to stop any background processes
await tatum.destroy();
```

### Overview

The `getAccountTrades` method allows you to retrieve all trades associated with a specific account on the Stellar blockchain. You can use this endpoint in streaming mode to listen for new trades as they are added to the Stellar ledger. When used in streaming mode, it starts at the earliest known trade unless a cursor is set, in which case it starts from that cursor. You can also set the cursor value to 'now' to stream trades created since your request time.

### Request Parameters

The `getAccountTrades` method accepts the following request parameters:

- `accountId` (string, required):
  The unique identifier (account ID) of the account for which you want to retrieve trades.

- `cursor` (string, optional):
  A cursor value that determines the starting point for pagination. Use this parameter to retrieve trades from a specific point in the trade list.

- `order` (string, optional):
  A designation of the order in which records should appear. Options include 'asc' (ascending) or 'desc' (descending). If this argument isn’t set, it defaults to 'asc'.

- `limit` (number, optional):
  The maximum number of records returned. It defines the number of trades to fetch in a single request.

### Return Object

The `getAccountTrades` method returns a JSON object containing the list of trades associated with the specified account. Each trade is represented as an object with various properties describing its details.

(Note: The exact fields in the return object might vary based on the Stellar blockchain's implementation and version.)

```json
{
  "value": {
    "_links": {
      "self": {
        "href": "https://horizon.stellar.org/accounts/GD3CJYUTZAY6JQF4CEI6Z7VW5O6VNGKZTBYUECTOJPEDTB7I2HZSPI2K/trades?cursor=&limit=3&order=asc"
      },
      "next": {
        "href": "https://horizon.stellar.org/accounts/GD3CJYUTZAY6JQF4CEI6Z7VW5O6VNGKZTBYUECTOJPEDTB7I2HZSPI2K/trades?cursor=107449584845914113-0&limit=3&order=asc"
      },
      "prev": {
        "href": "https://horizon.stellar.org/accounts/GD3CJYUTZAY6JQF4CEI6Z7VW5O6VNGKZTBYUECTOJPEDTB7I2HZSPI2K/trades?cursor=107449468881756161-0&limit=3&order=desc"
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
          "trade_type": "orderbook",
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
            "d": "10"
          }
        },
        {
          "_links": {
            "self": {
              "href": ""
            },
            "base": {
              "href": "https://horizon.stellar.org/accounts/GCQDOTIILRG634IRWAODTUS6H6Q7VUUNKZINBDJOXGJFR7YZ57FGYV7B"
            },
            "counter": {
              "href": "https://horizon.stellar.org/accounts/GD3CJYUTZAY6JQF4CEI6Z7VW5O6VNGKZTBYUECTOJPEDTB7I2HZSPI2K"
            },
            "operation": {
              "href": "https://horizon.stellar.org/operations/107449486061649921"
            }
          }
        }
      ]
    }
  }
}
```
