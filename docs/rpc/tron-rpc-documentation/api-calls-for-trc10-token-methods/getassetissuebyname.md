# getassetissuebyname

### How to use it

{% code overflow="wrap" lineNumbers="true" %}
```typescript
// yarn add @tatumio/tatum

import { TatumSDK, Tron, Network } from '@tatumio/tatum'

const tatum = await TatumSDK.init<Tron>({network: Network.TRON})

const res = await tatum.rpc.getAssetIssueByName('474d436f696e')

await tatum.destroy() // Destroy Tatum SDK - needed for stopping background jobs
```
{% endcode %}

### Overview

The `getAssetIssueByName` method allows you to query a token by name on the TRON blockchain. This method is useful when you need to get detailed information about a specific token, such as its total supply, issuer address, precision, and other related details.

### Parameters

* `name` (string): The TRC 10 token name, default hexString.

### Return Object

* `id` (string): Token ID.
* `owner_address` (string): Issuer address.
* `name` (string): Token name.
* `abbr` (string): Token abbreviation.
* `total_supply` (integer): Total supply.
* `frozen_supply` (FrozenSupply\[]): The number of tokens to be frozen is specified by the issuer of the token when it is issued.
* `trx_num` (integer): Define the price by the ratio of trx\_num/num (The unit of 'trx\_num' is SUN).
* `precision` (integer): Precision.
* `num` (integer): Define the price by the ratio of trx\_num/num (The unit of 'trx\_num' is SUN).
* `start_time` (integer): ICO start time.
* `end_time` (integer): ICO end time.
* `description` (string): Token description.
* `url` (string): Token official website URL, default hexString.
* `free_asset_net_limit` (integer): Token free asset net limit.
* `public_free_asset_net_limit` (integer): Token public free asset net limit for an account.
* `public_free_asset_net_usage` (integer): The total number of token free bandwidth used by all token owners.
* `public_latest_free_net_time` (integer): The timestamp of the last consumption of this token's free bandwidth.

### HTTP Request Example

```json
{
       "value": "62747474657374"
}
```

### HTTP Response Example

```json
{
  "id": "1000011",
  "owner_address": "41e552f6487585c2b58bc2c9bb4492bc1f17132cd0",
  "name": "62747474657374",
  "abbr": "BTTS",
  "total_supply": 1000000000000000,
  "frozen_supply": [],
  "trx_num": 1,
  "num": 1,
  "precision": 6,
  "start_time": 1530894319000,
  "end_time": 1533472719000,
  "description": "BitTorrent Token",
  "url": "https://www.bittorrent.com/",
  "free_asset_net_limit": 0,
  "public_free_asset_net_limit": 0,
  "public_free_asset_net_usage": 0,
  "public_latest_free_net_time": 0
}
```
