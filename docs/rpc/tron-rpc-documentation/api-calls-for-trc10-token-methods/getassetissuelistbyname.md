# getassetissuelistbyname

### How to use it

{% code overflow="wrap" lineNumbers="true" %}
```typescript
// yarn add @tatumio/tatum

import { TatumSDK, Tron, Network } from '@tatumio/tatum'

const tatum = await TatumSDK.init<Tron>({network: Network.TRON})

const res = await tatum.rpc.getAssetIssueListByName('62747474657374')

await tatum.destroy() // Destroy Tatum SDK - needed for stopping background jobs
```
{% endcode %}

### Overview

The `getAssetIssueListByName` method allows users to query the list of all the TRC10 tokens by a specific name. This can be useful in various scenarios, such as when one needs to quickly identify tokens with a specific name, or for tracking purposes, where knowing the associated tokens can provide valuable insights.

### Parameters

* `value` (string): Name of the TRC10 token to be queried. This parameter is required.

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
  "value": "49504653"
}
```

### HTTP Response Example

```json
{
    "assetIssue": [
        {
            "owner_address": "41d13433f53fdf88820c2e530da7828ce15d6585cb",
            "name": "49504653",
            "abbr": "49504653",
            "total_supply": 100000000000,
            "trx_num": 1000000,
            "num": 1,
            "start_time": 1529990700000,
            "end_time": 1537632000000,
            "description": "4950465320636f696e",
            "url": "687474703a2f2f",
            "id": "1000003"
        }
    ]
}
```
