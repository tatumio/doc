# getLiquidityPoolsTransactions

### How to use it

```typescript
// Import required libraries and modules from Tatum SDK
import { TatumSDK, Stellar, Network } from "@tatumio/tatum";

// Initialize the Tatum SDK for Stellar
const tatum = await TatumSDK.init<Stellar>({ network: Network.STELLAR });

// Define parameters (Replace placeholders with actual values and remove redundant)
const params = {
  liquidityPoolId: "YOUR_LIQUIDITY_POOL_ID",
  cursor: "YOUR_CURSOR",
  order: "asc",
  limit: 10,
  includeFailed: true,
};

// Retrieve transactions related to a liquidity pool
const liquidityPoolTransactions = await tatum.rpc.getLiquidityPoolsTransactions(
  params
);

// Always destroy the Tatum SDK instance when done to stop any background processes
await tatum.destroy();
```

### Overview

The `getLiquidityPoolsTransactions` method allows you to retrieve a list of transactions related to a specific liquidity pool on the Stellar blockchain.

### Example use cases:

1. **Liquidity Pool Transaction Analysis:**
   Developers and applications can use this method to analyze and retrieve information about transactions associated with a liquidity pool.
2. **Liquidity Pool Transaction Monitoring:**
   Platform administrators can monitor and track transactions related to liquidity pools for auditing and management purposes.

3. **Liquidity Pool Transaction Exploration:**
   Researchers and analysts can explore and analyze the characteristics of transactions involving liquidity pools on the Stellar network.

### Request Parameters

The `getLiquidityPoolsTransactions` method accepts the following optional parameters:

- `liquidityPoolId` (string, required):
  The unique identifier of the liquidity pool for which you want to retrieve transactions.

- `cursor` (string, optional):
  An optional cursor to start listing transactions from a specific point.

- `order` (string, optional):
  An optional parameter to specify the order of listing (asc or desc). If not provided, it defaults to 'asc'.

- `limit` (number, optional):
  An optional parameter to specify the maximum number of transactions to return. The limit can range from 1 to 200.

- `includeFailed` (boolean, optional):
  An optional parameter to include failed transactions. If set to true, failed transactions will be included in the results. Defaults to false.

### Return Object

The `getLiquidityPoolsTransactions` method returns an array of transactions related to the specified liquidity pool on the Stellar blockchain. Each transaction object contains information such as the transaction ID, source account, destination account, and more.

(Note: The exact fields in the return object might vary based on the Stellar blockchain's implementation and version.)

```json
{
  "_links": {
    "self": {
      "href": "https://01-vinthill-068-01.rpc.tatum.io/liquidity_pools/0000a8198b5e25994c1ca5b0556faeb27325ac746296944144e0a7406d501e8a/transactions?cursor=&limit=10&order=asc"
    },
    "next": {
      "href": "https://01-vinthill-068-01.rpc.tatum.io/liquidity_pools/0000a8198b5e25994c1ca5b0556faeb27325ac746296944144e0a7406d501e8a/transactions?cursor=215379467295031296&limit=10&order=asc"
    },
    "prev": {
      "href": "https://01-vinthill-068-01.rpc.tatum.io/liquidity_pools/0000a8198b5e25994c1ca5b0556faeb27325ac746296944144e0a7406d501e8a/transactions?cursor=215280038803128320&limit=10&order=desc"
    }
  },
  "_embedded": {
    "records": [
      {
        "_links": {
          "self": {
            "href": "https://01-vinthill-068-01.rpc.tatum.io/transactions/91a59ae616f077b905d29841d7b053282862d3fade107163ea9256847588ef56"
          },
          "account": {
            "href": "https://01-vinthill-068-01.rpc.tatum.io/accounts/GA4OGQSH75L2BBUEBRI4R56BP7ONJIJPGPSZXZYFCKQGXICPOXWFAU4H"
          },
          "ledger": {
            "href": "https://01-vinthill-068-01.rpc.tatum.io/ledgers/50123790"
          },
          "operations": {
            "href": "https://01-vinthill-068-01.rpc.tatum.io/transactions/91a59ae616f077b905d29841d7b053282862d3fade107163ea9256847588ef56/operations{?cursor,limit,order}",
            "templated": true
          },
          "effects": {
            "href": "https://01-vinthill-068-01.rpc.tatum.io/transactions/91a59ae616f077b905d29841d7b053282862d3fade107163ea9256847588ef56/effects{?cursor,limit,order}",
            "templated": true
          },
          "precedes": {
            "href": "https://01-vinthill-068-01.rpc.tatum.io/transactions?order=asc&cursor=215280038803128320"
          },
          "succeeds": {
            "href": "https://01-vinthill-068-01.rpc.tatum.io/transactions?order=desc&cursor=215280038803128320"
          },
          "transaction": {
            "href": "https://01-vinthill-068-01.rpc.tatum.io/transactions/91a59ae616f077b905d29841d7b053282862d3fade107163ea9256847588ef56"
          }
        },
        "id": "91a59ae616f077b905d29841d7b053282862d3fade107163ea9256847588ef56",
        "paging_token": "215280038803128320",
        "successful": true,
        "hash": "91a59ae616f077b905d29841d7b053282862d3fade107163ea9256847588ef56",
        "ledger": 50123790,
        "created_at": "2024-01-28T17:10:34Z",
        "source_account": "GA4OGQSH75L2BBUEBRI4R56BP7ONJIJPGPSZXZYFCKQGXICPOXWFAU4H",
        "account_muxed": "MA4OGQSH75L2BBUEBRI4R56BP7ONJIJPGPSZXZYFCKQGXICPOXWFAAAACJ4MHP7NAT4JQ",
        "account_muxed_id": "20309889510660",
        "source_account_sequence": "169911040828572928",
        "fee_account": "GA5Q3UHRKBBZFUQBFF3CEEPY322UIEALGUA7KS7LKGMAK7WJ4NF3W742",
        "fee_charged": "200",
        "max_fee": "2000",
        "operation_count": 1,
        "envelope_xdr": "",
        "result_xdr": "",
        "result_meta_xdr": "",
        "memo_type": "none",
        "signatures": [
          "qJxrEWQTd6cpHZyTgN4Ms+OwcE2rg+AqDlhUP5a450NlP8R4Vd6mgIxHR7ituxy9GS2W7Rl1XmqpgNCVup0kCw=="
        ],
        "valid_after": "1970-01-01T00:00:00Z",
        "preconditions": {
          "timebounds": {
            "min_time": "0"
          }
        },
        "fee_bump_transaction": {
          "hash": "91a59ae616f077b905d29841d7b053282862d3fade107163ea9256847588ef56",
          "signatures": [
            "qJxrEWQTd6cpHZyTgN4Ms+OwcE2rg+AqDlhUP5a450NlP8R4Vd6mgIxHR7ituxy9GS2W7Rl1XmqpgNCVup0kCw=="
          ]
        },
        "inner_transaction": {
          "hash": "a87a96da677ed8c7e079ac7e920399c864bfc811299d351fc4cf7b5588b1ddbd",
          "signatures": [
            "EK3OcLKkmFFHZaM75DkXF2OrSB3hc57kmUvqTA85yVKCu4WWAjQuDXSUJUczBiwKj3XMOTBUrDAJt+tYiB/YAA==",
            "Qu/5Py1qmxLO3zo1qB0kFfTithuGiv+mGfiVh1/IkN1PAuHNZPJkLMpzxgYiAYHj9vJnsgqG7IIfU5+23E1kCA=="
          ],
          "max_fee": "500"
        }
      }
    ]
  }
}
```
