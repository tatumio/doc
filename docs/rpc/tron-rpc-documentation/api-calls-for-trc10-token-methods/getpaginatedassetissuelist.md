# getpaginatedassetissuelist

### How to use it

Use the Tatum SDK to access the TRON network as follows:

{% code overflow="wrap" lineNumbers="true" %}
```typescript
// yarn add @tatumio/tatum

import { TatumSDK, Tron, Network } from '@tatumio/tatum'

const tatum = await TatumSDK.init<Tron>({network: Network.TRON})

const res = await tatum.rpc.getPaginatedAssetIssueList(0, 20)

await tatum.destroy() // Destroy Tatum SDK - needed for stopping background jobs
```
{% endcode %}

### Overview

* `assetIssue`: (array)
  * `id`: (integer) token ID
  * `owner_address`: (string) issuer address
  * `name`: (string) token name
  * `abbr`: (string) token abbreviation
  * `total_supply`: (integer) total supply
  * `frozen_supply`: (Array) The number of tokens to be frozen is specified by the issuer of the token when it is issued
  * `trx_num`: (integer) Define the price by the ratio of trx\_num/num(The unit of 'trx\_num' is SUN)
  * `precision`: (integer) precision
  * `num`: (integer) Define the price by the ratio of trx\_num/num(The unit of 'trx\_num' is SUN)
  * `start_time`: (integer) ICO start time
  * `end_time`: (integer) ICO end time
  * `description`: (string) token description
  * `url`: (string) Token official website url, default hexString
  * `free_asset_net_limit`: (integer) Token free asset net limit
  * `public_free_asset_net_limit`: (integer) Token public free asset net limit for a account
  * `public_free_asset_net_usage`: (integer) The total number of token free bandwidth used by all token owner
  * `public_latest_free_net_time`: (integer) The timestamp of the last consumption of this token's free bandwidth

{% embed url="https://codepen.io/tatum-devrel/pen/abQxXea" %}

### Parameters

1. `offset` (integer) - The index of the start token. This parameter allows you to specify the starting point in the list of tokens.
2. `limit` (integer) - The amount of tokens per page. This parameter allows you to limit the number of tokens returned in a single request.

### Return Object

This method returns a promise that resolves to an array of `AssetIssueCapsule` objects. Each `AssetIssueCapsule` object represents a TRC10 token and includes detailed fields as described in the `GetAssetIssueByAccount` method.

### HTTP Request Example

A typical HTTP request using this method looks like this:

```json
{
  "offset": 0,
  "limit": 20
}
```

### HTTP Response Example

```json
{
  "assetIssue": [
    {
      "owner_address": "41f3642e1824d654fed5e71f850fd82d24ed8545ed",
      "name": "2e6874616363657373",
      "abbr": "74657374",
      "total_supply": 1000000000,
      "trx_num": 1,
      "precision": 6,
      "num": 1,
      "start_time": 1629878133455,
      "end_time": 1629978123454,
      "description": "74657374",
      "url": "68747470733a2f2f73757065726d61747269782e696f",
      "id": "1000942"
    },
    {
      "owner_address": "411fafb1e96dfe4f609e2259bfaf8c77b60c535b93",
      "name": "303734363537333734",
      "abbr": "36353738363136643730366336353631363236323732",
      "total_supply": 100000000,
      "frozen_supply": [
        {
          "frozen_amount": 1,
          "frozen_days": 2
        }
      ],
      "trx_num": 1,
      "num": 1,
      "start_time": 1576684800000,
      "end_time": 1576728000000,
      "description": "3635373836313664373036633635323036343635373336333732363937303734363936663665",
      "url": "373737373737326536353738363136643730366336353265363336663664",
      "free_asset_net_limit": 10000,
      "public_free_asset_net_limit": 10000,
      "id": "1000030"
    },
    {
      "owner_address": "414f10065476e61054dad85d1c9a32cf429a6bc8cd",
      "name": "3077426974636f696e",
      "abbr": "57425443",
      "total_supply": 100000000000000,
      "trx_num": 6000000,
      "precision": 4,
      "num": 10000,
      "start_time": 1609023600000,
      "end_time": 1609110000000,
      "description": "426974636f696e20546f6b656e",
      "url": "68747470733a2f2f7368617374612e74726f6e7363616e2e6f72672f232f",
      "id": "1000507"
    }
  ]
}
```
