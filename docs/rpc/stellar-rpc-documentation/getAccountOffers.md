# getAccountOffers

### How to use it

```typescript
// Import required libraries and modules from Tatum SDK
import { TatumSDK, Stellar, Network } from "@tatumio/tatum";

// Initialize the Tatum SDK for Stellar
const tatum = await TatumSDK.init<Stellar>({ network: Network.STELLAR });

// Define input parameters as an object (Replace placeholders with actual values and remove redundant)
const params = {
  accountId: "YOUR_ACCOUNT_ID",
  cursor: "now",
  order: "asc",
  limit: 10,
};

// Retrieve all offers currently open for a given account
const offers = await tatum.rpc.getAccountOffers(params);

// Log the list of offers
console.log("Account Offers:", offers);

// Always destroy the Tatum SDK instance when done to stop any background processes
await tatum.destroy();
```

### Overview

The `getAccountOffers` method allows you to retrieve all offers that a specific account has currently open on the Stellar blockchain. You can use this endpoint in streaming mode to listen for new offers for the specified account as they are added to the Stellar ledger. When called in streaming mode, Horizon will start at the earliest known offer unless a cursor is set, in which case it will start from that cursor. Setting the cursor value to 'now' allows you to stream offers created since your request time.

### Request Parameters

The `getAccountOffers` method accepts the following request parameters:

- `accountId` (string, required):
  The unique identifier (account ID) of the account for which you want to retrieve offers.

- `cursor` (string, optional):
  A cursor value that determines the starting point for retrieving offers. Set it to 'now' to stream offers created since your request time.

- `order` (string, optional):
  A designation of the order in which records should appear. Options include 'asc' (ascending) or 'desc' (descending). If this argument isn’t set, it defaults to 'asc'.

- `limit` (number, optional):
  The maximum number of records returned. It defines the number of offers to fetch in a single request.

### Return Object

The `getAccountOffers` method returns a JSON object containing the list of offers associated with the specified account. Each offer represents an open order on the Stellar network, such as a trade offer to exchange one asset for another.

(Note: The exact fields in the return object might vary based on the Stellar blockchain's implementation and version.)

```json
{
  "value": {
    "_links": {
      "self": {
        "href": "https://horizon.stellar.org/accounts/GD3CJYUTZAY6JQF4CEI6Z7VW5O6VNGKZTBYUECTOJPEDTB7I2HZSPI2K/offers?cursor=&limit=10&order=asc"
      },
      "next": {
        "href": "https://horizon.stellar.org/accounts/GD3CJYUTZAY6JQF4CEI6Z7VW5O6VNGKZTBYUECTOJPEDTB7I2HZSPI2K/offers?cursor=164943216&limit=10&order=asc"
      },
      "prev": {
        "href": "https://horizon.stellar.org/accounts/GD3CJYUTZAY6JQF4CEI6Z7VW5O6VNGKZTBYUECTOJPEDTB7I2HZSPI2K/offers?cursor=164555927&limit=10&order=desc"
      }
    },
    "_embedded": {
      "records": [
        {
          "_links": {
            "self": {
              "href": "https://horizon.stellar.org/offers/164555927"
            },
            "offer_maker": {
              "href": "https://horizon.stellar.org/accounts/GD3CJYUTZAY6JQF4CEI6Z7VW5O6VNGKZTBYUECTOJPEDTB7I2HZSPI2K"
            }
          },
          "id": 164555927,
          "paging_token": "164555927",
          "seller": "GD3CJYUTZAY6JQF4CEI6Z7VW5O6VNGKZTBYUECTOJPEDTB7I2HZSPI2K",
          "selling": {
            "asset_type": "native"
          },
          "buying": {
            "asset_type": "credit_alphanum4",
            "asset_code": "BB1",
            "asset_issuer": "GD5J6HLF5666X4AZLTFTXLY46J5SW7EXRKBLEYPJP33S33MXZGV6CWFN"
          },
          "amount": "214.9999939",
          "price_r": {
            "n": 10000000,
            "d": 86000001
          },
          "price": "0.1162791",
          "last_modified_ledger": 28383147,
          "last_modified_time": "2020-02-24T22:58:38Z"
        },
        {
          "_links": {
            "self": {
              "href": "https://horizon.stellar.org/offers/164943216"
            },
            "offer_maker": {
              "href": "https://horizon.stellar.org/accounts/GD3CJYUTZAY6JQF4CEI6Z7VW5O6VNGKZTBYUECTOJPEDTB7I2HZSPI2K"
            }
          },
          "id": 164943216,
          "paging_token": "164943216",
          "seller": "GD3CJYUTZAY6JQF4CEI6Z7VW5O6VNGKZTBYUECTOJPEDTB7I2HZSPI2K",
          "selling": {
            "asset_type": "credit_alphanum4",
            "asset_code": "BB1",
            "asset_issuer": "GD5J6HLF5666X4AZLTFTXLY46J5SW7EXRKBLEYPJP33S33MXZGV6CWFN"
          },
          "buying": {
            "asset_type": "native"
          },
          "amount": "24.9999990",
          "price_r": {
            "n": 32224991,
            "d": 2500000
          },
          "price": "12.8899964",
          "last_modified_ledger": 28394149,
          "last_modified_time": "2020-02-25T15:49:57Z"
        }
      ]
    }
  }
}
```
