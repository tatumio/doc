# getenergyprices

### How to use it

{% code overflow="wrap" lineNumbers="true" %}
```typescript
// yarn add @tatumio/tatum

import { TatumSDK, Tron, Network } from '@tatumio/tatum';

const tatum = await TatumSDK.init<Tron>({network: Network.TRON});

const res = await tatum.rpc.getEnergyPrices();

await tatum.destroy() // Destroy Tatum SDK - needed for stopping background jobs
```
{% endcode %}

### Overview

The `getEnergyPrices` method is used to query historical energy unit price on the TRON network. The energy unit price is the cost of performing operations on the TRON network, measured in "sun" units. The historical data can be useful in various situations like estimating future energy costs based on historical data or analysing network activity over time.

{% embed url="https://codepen.io/tatum-devrel/pen/KKrYJLm" %}

### Parameters

This method does not require any parameters.

### Return Object

* `prices` - string: All historical energy unit price information. Each unit price change is separated by a comma. Before the colon is the millisecond timestamp, and after the colon is the energy unit price in sun.

### HTTP Request Example

```bash
{}
```

### HTTP Response Example

```json
{
    "prices": "1614227200000:15,1614313600000:20,1614400000000:25"
}
```

In this example response, three price changes are listed: on the timestamp `1614227200000`, the price was `15` sun; on `1614313600000`, the price changed to `20` sun; and on `1614400000000`, the price was `25` sun.
