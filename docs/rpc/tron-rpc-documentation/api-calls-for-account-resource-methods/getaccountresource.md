# getaccountresource

### How to use it

{% code overflow="wrap" lineNumbers="true" %}
```typescript
// yarn add @tatumio/tatum

import { TatumSDK, Tron, Network, VisibleOption } from '@tatumio/tatum'

const tatum = await TatumSDK.init<Tron>({network: Network.TRON})

const address = 'TZ4UXDV5ZhNW7fb2AMSbgfAEZ7hWsnYS2g'

const res = await tatum.rpc.getAccountResources(address, {
  visible: true,
})

tatum.destroy() // Destroy Tatum SDK - needed for stopping background jobs
```
{% endcode %}

### Overview

The `getAccountResources` method is used to query resource information (such as bandwidth, energy) of a specific account on the TRON network. This method can be useful for assessing an account's remaining computational and storage capacity.

{% embed url="https://codepen.io/tatum-devrel/pen/rNQbPvG" %}

### Parameters

* `address` (string): The address of the account whose resources are to be queried.
* `options` (object, optional): This optional parameter contains the following properties:
  * `visible` (boolean, optional): Optional parameter to specify whether the address is in base58 format.

### Return Object

* `freeNetUsed` (integer): Free bandwidth used.
* `freeNetLimit` (integer): Total free bandwidth.
* `NetUsed` (integer): Used amount of bandwidth obtained by staking.
* `NetLimit` (integer): Total bandwidth obtained by staking.
* `TotalNetLimit` (integer): Total bandwidth can be obtained by staking by the whole network.
* `TotalNetWeight` (integer): Total TRX staked for bandwidth by the whole network.
* `totalTronPowerWeight` (integer): The total amount of voting rights obtained by the whole network.
* `tronPowerLimit` (integer): TRON Power (vote).
* `tronPowerUsed` (integer): TRON Power (vote) used.
* `EnergyUsed` (integer): Energy used.
* `EnergyLimit` (integer): Total energy obtained by staking.
* `TotalEnergyLimit` (integer): Total energy can be obtained by staking by the whole network.
* `TotalEnergyWeight` (integer): Total TRX staked for energy by the whole network.
* `assetNetUsed` (map\<string, integer>): The amount of free bandwidth of each TRC10 asset used by the account.
* `assetNetLimit` (map\<string, integer>): The amount of free bandwidth for each TRC10 asset in the account.

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
  "freeNetLimit": 1500,
  "TotalNetLimit": 43200000000,
  "TotalNetWeight": 84593524300,
  "TotalEnergyLimit": 50000000000000,
  "TotalEnergyWeight": 12189370443
}
```
