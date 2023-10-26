# getassetissuebyaccount

### How to use it

{% code overflow="wrap" lineNumbers="true" %}
```typescript
// yarn add @tatumio/tatum

import { TatumSDK, Tron, Network } from '@tatumio/tatum'

const tatum = await TatumSDK.init<Tron>({network: Network.TRON})

const res = await tatum.rpc.getAssetIssueByAccount('TTzC9cm1vbsyBzhC8n4z3k6eAVkryDyKU8', {
visible: true,
})

tatum.destroy() // Destroy Tatum SDK - needed for stopping background jobs
```
{% endcode %}

### Overview

The `getAssetIssueByAccount` method queries the TRC10 token information issued by a specified account. The main use case for this method is to gather information about tokens issued by a certain address on the TRON blockchain.

### Parameters

* `address` (string): This is the address of the Token Issuer account.
* `options` (object, optional): This optional parameter contains the following properties:
  * `visible` (boolean, optional): Whether the address is in base58 format.

### Return Object

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

### HTTP Request Example

```json
{
  "address": "TZ4UXDV5ZhNW7fb2AMSbgfAEZ7hWsnYS2g",
  "visible": true
}
```

### HTTP Response Example

```json
{
  "assetIssue": [
    {
      "id": 1,
      "owner_address": "TZ4UXDV5ZhNW7fb2AMSbgfAEZ7hWsnYS2g",
      "name": "TokenName",
      "abbr": "TKN",
      "total_supply": 1000000,
      "frozen_supply": [],
      "trx_num": 1,
      "precision": 6,
      "num": 1,
      "start_time": 1622376000000,
      "end_time": 1622462400000,
      "description": "This is a test token",
      "url": "https://tokenwebsite.com",
      "free_asset_net_limit": 5000,
      "public_free_asset_net_limit": 10000,
      "public_free_asset_net_usage": 0,
      "public_latest_free_net_time": 0
    }
  ]
}
```

***
