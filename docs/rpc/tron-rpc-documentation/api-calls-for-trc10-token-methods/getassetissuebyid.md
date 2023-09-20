# getassetissuebyid

### How to use it

{% code overflow="wrap" lineNumbers="true" %}
```typescript
// yarn add @tatumio/tatum

import { TatumSDK, Tron, Network } from '@tatumio/tatum'

const tatum = await TatumSDK.init<Tron>({network: Network.TRON})

const res = await tatum.rpc.getAssetIssueById(1002357)

tatum.destroy() // Destroy Tatum SDK - needed for stopping background jobs
```
{% endcode %}

### Overview

This method is used to query a token by its token id in the TRON blockchain. Since TRON allows for duplicate token names (TRC10 tokens), tokens are identifiable by a unique Token ID. The function `getAssetIssueById` takes this Token ID and returns the token object, which includes the token name.

### Parameters

* `value` (string): The address of the TRON account.

### Return Object

The function returns a promise that resolves to an object of type `AssetIssueCapsule`. This object contains the following properties:



* `id`: (integer) Token ID.
* `owner_address`: (string) Issuer address.
* `name`: (string) Token name.
* `abbr`: (string) Token abbreviation.
* `total_supply`: (integer) Total supply of tokens.
* `frozen_supply`: (FrozenSupply\[]) The number of tokens to be frozen as specified by the issuer when it was issued.
* `trx_num`: (integer) Defines the price by the ratio of trx\_num/num. The unit of 'trx\_num' is SUN.
* `precision`: (integer) Precision of the token.
* `num`: (integer) Defines the price by the ratio of trx\_num/num. The unit of 'trx\_num' is SUN.
* `start_time`: (integer) ICO start time.
* `end_time`: (integer) ICO end time.
* `description`: (string) Token description.
* `url`: (string) Token's official website URL, default hexString.
* `free_asset_net_limit`: (integer) Token's free asset net limit.
* `public_free_asset_net_limit`: (integer) Token's public free asset net limit for an account.
* `public_free_asset_net_usage`: (integer) The total number of token free bandwidth used by all token owner.
* `public_latest_free_net_time`: (integer) The timestamp of the last consumption of this token's free bandwidth.

### HTTP Request Example

```json
{
    "value":1000001
}
```

### HTTP Response Example

```json
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
}
```
