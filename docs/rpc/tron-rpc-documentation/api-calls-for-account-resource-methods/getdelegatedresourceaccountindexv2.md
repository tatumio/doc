# getdelegatedresourceaccountindexv2

## TRON RPC Method: getDelegatedResourceAccountIndexV2

### How to use it

{% code overflow="wrap" lineNumbers="true" %}
```typescript
// yarn add @tatumio/tatum

import { TatumSDK, Tron, Network } from '@tatumio/tatum'

const tatum = await TatumSDK.init<Tron>({network: Network.TRON})

const result = await tatum.rpc.getDelegatedResourceAccountIndexV2('TPswDDCAWhJAZGdHPidFg5nEf8TkNToDX1', {
visible: true,
})

await tatum.destroy() // Destroy Tatum SDK - needed for stopping background jobs
```
{% endcode %}

### Overview

`getDelegatedResourceAccountIndexV2` is an RPC method provided by TRON's API. It is used in the context of TRON's Stake2.0 system to query the resource delegation index by an account. It returns two lists: one is the list of addresses the account has delegated its resources to (`toAccounts`), and the other is the list of addresses that have delegated resources to the account (`fromAccounts`).

Some potential use cases include:

1. Checking the status of resource delegations for a specific account.
2. Understanding the delegation relationships of an account.

{% embed url="https://codepen.io/tatum-devrel/pen/poQBGxe" %}

### Parameters

* `value:` (string): The account address. By default, it is in hexString format.
* `options` (object, optional): This optional parameter contains the following properties:
  * `visible` (boolean, optional): Optional parameter to specify whether the address is in base58 format.

### Return Object

The returned object includes the following fields:

* `account` - The account address.
* `fromAccounts` - The list of addresses that have delegated resources to the account.
* `toAccounts` - The list of addresses the account has delegated its resources to.

### HTTP Request Example

```json
{
  "value": "TPswDDCAWhJAZGdHPidFg5nEf8TkNToDX1",
  "visible": true
}
```

### HTTP Response Example

```json
{
  "account": "TPswDDCAWhJAZGdHPidFg5nEf8TkNToDX1"
}
```
