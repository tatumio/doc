# getburntrx

### How to use it

{% code overflow="wrap" lineNumbers="true" %}
```typescript
// yarn add @tatumio/tatum

import { TatumSDK, Tron, Network } from '@tatumio/tatum';

const tatum = await TatumSDK.init<Tron>({network: Network.TRON});

const res = await tatum.rpc.getBurnTRX();

tatum.destroy() // Destroy Tatum SDK - needed for stopping background jobs
```
{% endcode %}

### Overview

The `getBurnTRX()` RPC method allows to query the amount of TRX burned due to on-chain transaction fees since the No. 54 Committee Proposal took effect.

Before the No. 54 Committee Proposal takes effect, the destruction of transaction fees is completed by transferring to the black hole address TLsV52sRDL79HXGGm9yzwKibb6BeruhUzy. After the No. 54 committee proposal takes effect, it will no longer be transferred to the black hole address, but will be directly recorded in the node database.

Use cases of this method include monitoring the total amount of TRX burned due to transaction fees, which can be useful for data analysis and transparency purposes.

{% embed url="https://codepen.io/tatum-devrel/pen/VwVNgOO" %}

### Parameters

The `getBurnTRX()` RPC method does not require any parameters.

### Return Object

* `burnTrxAmount`: This is the amount of TRX burned due to on-chain transaction fees. The amount is returned in sun (1 TRX = 1,000,000 sun).

### HTTP Request Example

```bash
{}
```

### HTTP Response Example

```json
{
    "burnTrxAmount": 200
}
```

Note that the `burnTrxAmount` is returned as an integer in sun.

***
