# getbandwidthprices

### How to use it

{% code overflow="wrap" lineNumbers="true" %}
```typescript
// yarn add @tatumio/tatum

import { TatumSDK, Tron, Network } from '@tatumio/tatum'

const tatum = await TatumSDK.init<Tron>({network: Network.TRON})

const res = await tatum.rpc.getBandwidthPrices()

tatum.destroy() // Destroy Tatum SDK - needed for stopping background jobs
```
{% endcode %}

### Overview

The `getBandwidthPrices()` method is used to retrieve historical bandwidth unit prices on the TRON blockchain. Bandwidth is an essential resource in the TRON network used for performing transactions. This method will return all historical prices, where each unit price change is separated by a comma.

{% embed url="https://codepen.io/tatum-devrel/pen/xxQeMNy" %}

### Parameters

This method doesn't require any parameters.

### Return Object

* `prices`: A string that represents all historical bandwidth unit price information. Each unit price change is separated by a comma. Before the colon is the millisecond timestamp, and after the colon is the bandwidth unit price in sun.

### HTTP Request Example

```shell
{}
```

### HTTP Response Example

```json
{
  "prices": "1613713487000:100,1613799887000:200,1613886287000:150"
}
```

In this example, the first bandwidth unit price change was at timestamp `1613713487000` with a price of `100` sun, the second at timestamp `1613799887000` with a price of `200` sun, and so on.
