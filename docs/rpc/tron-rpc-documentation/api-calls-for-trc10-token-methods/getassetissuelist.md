# getassetissuelist

### How to use It

{% code overflow="wrap" lineNumbers="true" %}
```typescript
// yarn add @tatumio/tatum

import { TatumSDK, Tron, Network } from '@tatumio/tatum'

const tatum = await TatumSDK.init<Tron>({network: Network.TRON})

const res = await tatum.rpc.getAssetIssueList()

await tatum.destroy() // Destroy Tatum SDK - needed for stopping background jobs
```
{% endcode %}

### Overview

The `getAssetIssueList` RPC method allows you to query the list of all the TRC10 tokens on the TRON network.

{% embed url="https://codepen.io/tatum-devrel/pen/XWyQOLq" %}

### Parameters

This RPC method doesn't require any parameters.

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

Below is an example of how to use the `getAssetIssueList` RPC method with a curl HTTP request:

```shell
curl --request GET \
     --url https://api.tatum.io/v3/blockchain/node/tron-testnet/wallet/getassetissuelist
```

### HTTP Response Example

```json
{
  "assetIssue": [
    {
      "owner_address": "412e1934759faf93497d6742208e2e521f7043e2ff",
      "name": "62747474657374",
      "abbr": "62747474657374",
      "total_supply": 1000000000000000,
      "trx_num": 1000000,
      "precision": 6,
      "num": 1000000,
      "start_time": 1575648000000,
      "end_time": 1575734400000,
      "description": "62747474657374",
      "url": "68747470733a2f2f62746673736f7465722e726561646d652e696f2f646f63732f686f772d746f2d6765742d737461727465642d776974682d736f746572",
      "id": "1000001"
    },
    {
      "owner_address": "411e260aeff8bd61d42590d256b671c8062926ef20",
      "name": "6f756363746f6b656e",
      "abbr": "4f554343",
      "total_supply": 10000000000,
      "trx_num": 1000000,
      "num": 1,
      "start_time": 1575648000000,
      "end_time": 1640275200000,
      "description": "74657374",
      "url": "687474703a2f2f7777772e62616964752e636f6d",
      "id": "1000002"
    }
  ]
}
```

